<template>
    <div id="theme_toggler" class="position-absolute">
        <input
            @change="toggle_theme"
            ref="theme_toggler_btn"
            type="checkbox"
            id="theme_toggler_btn"
            class="checkbox opacity-0 position-absolute"
        />
        <label class="label" for="theme_toggler_btn">
            <ion-icon v-pre name="sunny" class="icon"></ion-icon>
            <ion-icon v-pre name="moon" class="icon"></ion-icon>
            <div class="ball"></div>
        </label>
    </div>
</template>

<script>
export default {
    name: "ThemeToggler",
    mounted() {
        if (localStorage.getItem("dark-theme") == "yes") {
            this.set_dark_mode()
            this.$refs.theme_toggler_btn.checked = !this.$refs.theme_toggler_btn.checked
        }
    },
    methods: {
        set_dark_mode() {
            localStorage.setItem("dark-theme", "yes")
            document.documentElement.setAttribute("theme", "dark")
        },
        toggle_theme() {
            if (document.documentElement.hasAttribute("theme")) {
                localStorage.setItem("dark-theme", "no")
                document.documentElement.removeAttribute("theme")
            } else this.set_dark_mode()
        }
    }
}
</script>

<style scoped>
#theme_toggler {
    opacity: 0.8;
    transition: 0.3s;
    color: var(--text-color);
}
#theme_toggler:hover {
    opacity: 1;
    color: var(--text-color);
}
#theme_toggler {
    top: 20px;
}
#theme_toggler {
    left: 20px;
}
.checkbox {
    opacity: 0;
    position: absolute;
}
.label {
    background-color: #343a40;
    border-radius: 50px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 5px;
    position: relative;
    height: 26px;
    width: 50px;
    transform: scale(1.5);
}
.label .ball {
    background-color: #fff;
    border-radius: 50%;
    position: absolute;
    top: 2px;
    left: 2px;
    height: 22px;
    width: 22px;
    transform: translateX(0);
    transition: transform 0.2s linear;
}
.checkbox:checked + .label .ball {
    transform: translateX(24px);
}
.icon {
    color: yellow;
}
</style>
