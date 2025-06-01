<template>
    <div :data-theme="theme">
        <Theme @toggle-theme="toggleTheme" />
        <main>
            <div id="gen-advice" v-show="showAdvice">
                <blockquote>
                    <p>{{ advice }}</p>
                </blockquote>
            </div>
            <button type="button" class="gen-btn" @click="toggleAdvice">Generate Advice</button>
        </main>
    </div>
</template>

<script>
import "./assets/css/global.css";
import Theme from "./components/Theme";

export default {
    name: "App",
    data() {
        return {
            showAdvice: false,
            advice: "",
            theme: window.matchMedia("(prefers-color-scheme: dark)").matches ? "dark" : "light",
        };
    },
    methods: {
        toggleAdvice() {
            this.fetchAdvice();
        },

        async fetchAdvice() {
            try {
                const response = await fetch("https://api.adviceslip.com/advice");
                const data = await response.json();
                this.advice = data.slip.advice;
                this.showAdvice = true;
            } catch (error) {
                console.error("Error fetching data from API: ", error);
            }
        },

        toggleTheme() {
            this.theme = this.theme === "dark" ? "light" : "dark";
        },
    },
    components: {
        Theme,
    },
};
</script>

<style>
#app > div[data-theme="dark"] {
    height: 100svh;
    background-color: #111;
}

#app > div[data-theme] > * {
    font: inherit;
}

#app button {
    cursor: pointer;
}

main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 2rem;
    height: calc(100svh - 100px);
}

main > #gen-advice {
    font-size: 1.25em;
    align-content: center;
    text-align: center;
    min-height: 300px;
    max-width: 700px;
    width: 100%;
    padding: 1rem;
    border-radius: 8px;
    outline: 1px solid #1f1f1f;
    background-color: #161616;
}

main > .gen-btn {
    padding: 0.5rem 1.5rem;
    color: #fff;
    border: none;
    border-radius: 8px;
    background-color: rgb(0, 102, 255);
    box-shadow: 0 0 15px 0 rgb(0, 81, 203, 0.25), 0 5px 0px 0 rgb(0, 51, 171);
    transition: box-shadow 0.1s linear, scale 0.05s linear;
}

main > .gen-btn:active {
    scale: 0.95;
    box-shadow: 0 0 15px 0 rgb(0, 81, 203, 0.25), 0 0px 0px 0 rgb(0, 51, 171);
}

[data-theme="dark"] {
    color: #fff;
    background-color: #111;
}

[data-theme="light"] {
    color: #2c3e50;
    background-color: #fff !important;
}

[data-theme="light"] nav + hr {
    background: linear-gradient(to right, transparent, #f3f3f3, transparent) !important;
}

[data-theme="light"] nav strong {
    color: #353535;
}

[data-theme="light"] main > #gen-advice {
    color: #2c3e50;
    outline-color: #d3d3d3;
    background-color: #fff !important;
}
</style>
