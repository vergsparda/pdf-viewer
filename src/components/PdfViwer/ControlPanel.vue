<template >
    <div class="control-panel">
        <button class="button" @click="onZoomIn">Увеличить</button>
        <button class="button" @click="onZoomOut">Уменьшить</button>
        <button class="button" @click="rotate">Повернуть на 90</button>
    </div>
</template>
<script>
    export default {
        name: 'ControlPanel',

        props: ['onZoomIn', 'onZoomOut', 'onRotate'],

        data() {
            return {
                rotation: 0,
            }
        },

        methods: {
            rotate() {
                this.rotation === 270 ? this.rotation = 0 : this.rotation +=90
                this.onRotate({rotation: this.rotation})
            }
        }
    }
</script>
<style lang="scss">
    .control-panel {
        height: 30px;
        background-color: #bababf;
        position: fixed;
        display: flex;
        gap: 10px;
        width: 100%;
        z-index: 100;
        justify-content: center;
        align-items: center;
        border-bottom: 2px solid #000008;

        .button {
            background: #8071f3;
            color: #fff;
            border-radius: 40px;
            padding: 5px 8px;
            text-transform: uppercase;
            text-align: center;
            font-size: 10px;
            font-weight: 600;
            border: none;
            cursor: pointer;
        }
    }
</style>