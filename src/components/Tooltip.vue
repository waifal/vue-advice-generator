<template>
    <div class="tooltip" v-text="text"></div>
</template>

<script>
    export default {
        props: ['text'],
    }
</script>

<style scoped>
    div {
        display: none;
        width: fit-content;
        height: 35px;
        padding: 0 0.8rem;
        color: #fff;
        align-content: center;
        font-size: 0.9rem;
        position: absolute;
        left: 50%;
        top: 155%;
        white-space: nowrap;
        transform: translate(-50%, -50%);
        border-radius: 8px;
        background-color: rgba(46, 46, 46, 0.5);
        transition: opacity 0.2s linear;
    }

    div::before {
        content: "";
        position: absolute;
        left: 50%;
        top: -33%;
        transform: translateX(-50%);
        border-width: 6px; 
        border-style: solid;
        border-color:  transparent transparent rgba(46, 46, 46, 0.5) transparent;
    }
</style>