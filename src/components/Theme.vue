<template>
    <nav>
        <strong>Vue Advice Generator</strong>
        <button type="button" @click="toggleTheme" @mouseover="showTooltip">
            <i class="fa-solid fa-moon"></i>
            <Tooltip text="Toggle Theme" />
        </button>
    </nav>
    <hr />
</template>

<script>
import Tooltip from "./Tooltip.vue";

export default {
    emits: ["toggle-theme"],
    components: { Tooltip },
    methods: {
        toggleTheme() {
            this.$emit("toggle-theme");
        },
    },
};
</script>

<style scoped>
nav {
    height: 80px;
    padding: 0 4rem;
    display: flex;
    align-items: center;
}

nav > * {
    color: #2f2f2f;
}

nav > strong {
    color: #e4e4e4;
}

nav + hr {
    height: 1px;
    border: none;
    background: linear-gradient(to right, transparent, #171717, transparent);
}

button {
    width: 45px;
    height: 45px;
    margin-left: auto;
    font-size: 1.2rem;
    border: none;
    border-radius: 50%;
    background: none;
    position: relative;
    transition: 0.2s linear background, 0.2s linear color;
}

button:hover {
    color: #575757;
    background: rgba(46, 46, 46, 0.1);
}

button:hover > div {
    display: block;
    animation: tooltip-fade 0.3s ease-in-out;
}

@keyframes tooltip-fade {
    from {
        opacity: 0;
        top: 160%;
    }

    to {
        opacity: 1;
        top: 155%;
    }
}
</style>
