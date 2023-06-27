<template>
    <div class="panel-wrap">
        <div class="panel-page" v-for="page in pageCount" :key="page">
            <button class="page-button" :class="{active: page == activePage}" @click.prevent="handlePageButton(page)">
                <vue-pdf-embed ref="pdf" :source="url" :page="page" :disableAnnotationLayer="true" :disableTextLayer="true"/>
                <span class="page-num">{{ page }}</span>
            </button>
        </div>
    </div>
</template>
<script>
import VuePdfEmbed from 'vue-pdf-embed/dist/vue2-pdf-embed'

export default {
    name: 'PagesPanel',
    props: ['pageCount', 'url', 'scrollToPage'],
    data() {
        return {
            activePage: 1
        }
    },

    components: {
        VuePdfEmbed,
    },

    methods: {
        handlePageButton(page) {
            this.activePage = page;
            this.scrollToPage(page);
        }
    },

}
</script>
<style lang="scss">
.panel-wrap {
    position: fixed;
    z-index: 50;
    top: 0;
    bottom: 0;
    width: 15%;
    padding-top: 50px;
    overflow-y: scroll;
    overflow-x: hidden;

    .panel-page {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    .page-button {
        border: 2px solid #aaaaaa;
        width: 60%;
        margin:0 0 20px;
        cursor: pointer;
        padding: unset;
        background-color: unset;
        transition: all .2s ease-out;

        &.active {
            border: 3px solid #8071f3;
            overflow: hidden;
        }

        &:hover {
            box-shadow: 5px 10px 30px rgba(84,102,167,.3);
        }
    }

    .page-num {
        font-size: 14px;
        line-height: 29px;
    }
}
</style>