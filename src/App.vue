<template>
    <div>
        <ThemeToggler />
        <Calculator />
    </div>
</template>

<script>
import ThemeToggler from "./components/ThemeToggler.vue"
import Calculator from "./components/Calculator.vue"

export default {
    name: "App",
    components: {
        ThemeToggler, Calculator
    }
}
</script>
