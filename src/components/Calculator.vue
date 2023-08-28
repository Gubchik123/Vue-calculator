<template>
    <div class="container mt-5 pt-5">
        <div class="row justify-content-center">
            <div class="col-md-6">
                <div class="calculator">
                    <div
                        v-show="expression_history" 
                        class="history text-muted"
                    >
                        {{ expression_history }} =
                    </div>
                    <div class="result">
                        {{ expression }}
                    </div>
                    <div class="row">
                        <button 
                            @click="expression_history = null, expression = '0'" 
                            id="clear"
                            class="col" 
                        >
                            C
                        </button>
                        <button @click="remove_last_char" class="col" id="backspace">
                            &#9003;
                        </button>
                        <button @click="add_operator('%')" class="col" id="modulo">%</button>
                        <button @click="add_operator('/')" class="col" id="divide">/</button>
                    </div>
                    <div class="row">
                        <button @click="add_number('7')" class="col" id="7">7</button>
                        <button @click="add_number('8')" class="col" id="8">8</button>
                        <button @click="add_number('9')" class="col" id="9">9</button>
                        <button @click="add_operator('*')" class="col" id="multiply">*</button>
                    </div>
                    <div class="row">
                        <button @click="add_number('4')" class="col" id="4">4</button>
                        <button @click="add_number('5')" class="col" id="5">5</button>
                        <button @click="add_number('6')" class="col" id="6">6</button>
                        <button @click="add_operator('-')" class="col" id="subtract">-</button>
                    </div>
                    <div class="row">
                        <button @click="add_number('1')" class="col" id="1">1</button>
                        <button @click="add_number('2')" class="col" id="2">2</button>
                        <button @click="add_number('3')" class="col" id="3">3</button>
                        <button @click="add_operator('+')" class="col" id="add">+</button>
                    </div>
                    <div class="row">
                        <button @click="add_number('0')" class="col-6" id="0">0</button>
                        <button @click="add_dot('.')" class="col" id="decimal">.</button>
                        <button @click="calculate" class="col" id="equals">=</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "Calculator",
    data() {
        return { expression: "0", expression_history: null }
    },
    computed: {
        calculate() {
            if (this.expression !== "0") {
                try {
                    this.expression_history = this.expression
                    this.expression = String(
                        Function("'use strict'; return (" + this.expression + ")")()
                    )
                } catch (error) {
                    alert(error.message)
                    this.expression = "0"
                }
            }
        },
        _is_ends_with_operator() {
            return ["+", "-", "*", "/"].includes(this.expression.slice(-1))
        },
        _get_last_number() {
            const parts = this.expression.split(/[-+*/]/)
            return parts[parts.length - 1]
        },
        _can_add_decimal() {
            const last_number = this._get_last_number
            return last_number && !this._get_last_number.includes(".")
        }
    },
    methods: {
        remove_last_char() {
            this.expression_history = null;
            if (this.expression.length === 1 && this.expression !== "0") this.expression = "0"
            else if (this.expression !== "0") this.expression = this.expression.slice(0, -1)
        },
        add_number(number) {
            this.expression_history = null;
            if (this.expression === "0" || this.expression === "Error") this.expression = number
            else this.expression += number
        },
        add_operator(operator) {
            this.expression_history = null;
            if (this._is_ends_with_operator)
                this.expression = this.expression.slice(0, -1) + operator
            else this.expression += operator
        },
        add_dot() {
            this.expression_history = null;
            if (this._can_add_decimal) this.expression += "."
        }
    }
}
</script>

<style scoped>
.calculator {
    max-width: 300px;
    margin: 0 auto;
    background-color: var(--panel-bg-color);
    border-radius: 8px;
    padding: 20px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}
.calculator .history,
.calculator .result {
    font-size: 1.5rem;
    text-align: right;
}
.calculator .result {
    margin-bottom: 15px;
}
.calculator button {
    width: 60px;
    height: 60px;
    font-size: 1rem;
    margin: 5px;
    background-color: var(--btn-bg-color);
    border: none;
    color: var(--text-color);
    border-radius: 8px;
    cursor: pointer;
}
.calculator button:hover {
    background-color: var(--btn-hover-bg-color);
}
</style>