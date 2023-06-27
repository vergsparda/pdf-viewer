<template lang="">
    <div class="pdf-viewer">
        <control-panel :onZoomIn="onZoomIn" :onZoomOut="onZoomOut" :onRotate="onRotate"/>
        <div class="viewer-wrap">
            <pages-panel :pageCount="pageCount" :url="url" :scrollToPage="scrollToPage"/>
            <div class="pdf-wrap">
                <vue-pdf-embed ref="pdfRef" class="doc-view" :source="url" :rotation="rotation" :width="width" :height="height" @rendered="handleDocumentRender"/>
            </div>
        </div>
    </div>
</template>
<script>
import VuePdfEmbed from 'vue-pdf-embed/dist/vue2-pdf-embed'
import ControlPanel from './ControlPanel.vue'
import PagesPanel from './PagesPanel.vue'

export default {
    name: 'PdfViewer',
    props: ['url'],

    components: {
        VuePdfEmbed,
        ControlPanel,
        PagesPanel
    },

    data() {
        return {
            rotation: 0,
            width: null,
            height: null,
            pageCount: null,
            scale: 0,
        }
    },

    methods: {
        onZoomIn() {
            this.width += 50;
            this.height += 50;
            this.scale -= 1;
            let text = document.querySelectorAll('.textLayer');
            text.forEach(el => {
                this.scaleTextLayer(el);
            })
        },

        onZoomOut() {
            this.width -= 50;
            this.height -= 50;
            this.scale += 1;
            let text = document.querySelectorAll('.textLayer');
            text.forEach(el => {
                this.scaleTextLayer(el);
            })
        },

        onRotate(data) {
            if (data) {
                this.rotation = data.rotation;
            }
        },

        handleDocumentRender() {
            if (!this.width && !this.height) {
                let canvas = document.querySelector('canvas');
                this.width = canvas.offsetWidth;
                this.height = canvas.offsetHeight;
                this.pageCount = this.$refs.pdfRef.pageCount;
            }
        },

        scaleTextLayer(el) {
            el.style.width = this.width + "px";
            el.style.left = (this.scale * 25) + "px";
        },

        scrollToPage(page) {
            if (page) {
                const pages = document.querySelectorAll('.doc-view>div');
                this.scrollToElement(pages[page - 1]);
            }
        },

        scrollToElement(element) {
            if (element) {
                requestAnimationFrame(() => {
                    const yOffset = -document.querySelector('.control-panel').offsetHeight;
                    const y = element.getBoundingClientRect().top + window.pageYOffset + yOffset;

                    window.scrollTo({top: y, behavior: 'smooth'});
                });
            }
        },
    }

}
</script>
<style lang="scss">
    .pdf-viewer {
        width: 100%;
        position: relative;
        
        .viewer-wrap {
            width: 100%;
            display: flex;
        }

        .pdf-wrap {
            width: 85%;
            margin-left: 15%;
            padding-top: 30px;
            border-left: 2px solid #000008;
            overflow: hidden; 

            .doc-view > div {
                display: flex;
                align-items: center;
                justify-content: center;
            }
        }
    }
</style>