<template>
  <div class="calculator">
    <div class="display key">{{current || '0'}}</div>
    <div @click="clear()" class="clear key">C</div>
    <div @click="sign()" class="operator key">+/-</div>
    <div @click="percent()" class="operator key">%</div>
    <div @click="pi()" class="operator key">&pi;</div>
    <div @click="inverse()" class="operator key">1/x</div>
    <div @click="squared()" class="operator key">x<sup>2</sup></div>
    <div @click="sqrt()" class="operator key">&radic;<span style="padding-top: 1px; text-decoration:overline;">x</span></div>
    <div @click="divide()" class="operator key">&divide;</div>
    <div @click="append('7')" class="key">7</div>
    <div @click="append('8')" class="key">8</div>
    <div @click="append('9')" class="key">9</div>
    <div @click="multiply()" class="operator key">*</div>
    <div @click="append('4')" class="key">4</div>
    <div @click="append('5')" class="key">5</div>
    <div @click="append('6')" class="key">6</div>
    <div @click="subtract()" class="operator key">-</div>
    <div @click="append('1')" class="key">1</div>
    <div @click="append('2')" class="key">2</div>
    <div @click="append('3')" class="key">3</div>
    <div @click="add()" class="operator key">+</div>
    <div @click="append('0')" class="zero key">0</div>
    <div @click="dot()" class="dot key">.</div>
    <div @click="equals()" class="operator key">=</div>
  </div>
</template>

<script>
export default {
    data() {
        return {
            current: '',
            previous: '',
            operator: null,
            operatorClicked: false
        }
    },
    methods: {
        clear() {
            this.current = '';
        },

        savePrevious() {
            this.previous = this.current;
            this.operatorClicked = true;
        },

        resetPrevious() {
            this.previous = '';
            this.operatorClicked = false;
        },

        add() {
            if (this.operatorClicked) {
                this.current = String(this.operator(parseFloat(this.previous), parseFloat(this.current)));
                this.resetPrevious;
            } else {
                this.operator = (a, b) => a + b;
                this.savePrevious();
            }
        },

        subtract() {
            if (this.operatorClicked) {
                this.current = String(this.operator(parseFloat(this.previous), parseFloat(this.current)));
                this.resetPrevious;
            } else {
                this.operator = (a, b) => a - b;
                this.savePrevious();
            }
        },

        divide() {
            if (this.operatorClicked) {
                this.current = String(this.operator(parseFloat(this.previous), parseFloat(this.current)));
                this.resetPrevious;
            } else {
                this.operator = (a, b) => a / b;
                this.savePrevious();
            }
        },

        multiply() {
            if (this.operatorClicked) {
                this.current = String(this.operator(parseFloat(this.previous), parseFloat(this.current)));
                this.resetPrevious;
            } else {
                this.operator = (a, b) => a * b;
                this.savePrevious();
            }
        },

        dot() {
            if (this.current.indexOf('.') === -1) {
                this.append('.');
            }
        },

        equals() {
            this.current = String(this.operator(parseFloat(this.previous), parseFloat(this.current)));
            this.resetPrevious;
        },

        sign() {
            if (this.current.indexOf('-') === 0) {
                this.current = this.current.slice(1);
            } else {
                this.current = `-${this.current}`;
            }
        },

        percent() {
            this.current = String(parseFloat(this.current) / 100);
        },

        append(number) {
            if (this.operatorClicked) {
                this.current = '';
                this.operatorClicked = false;
            }
            this.current = `${this.current}${number}`;
        },

        sqrt() {
            this.current = String(Math.sqrt(parseFloat(this.current)));
        },

        squared() {
            this.current = String(parseFloat(this.current) * parseFloat(this.current));
        },

        pi() {
            this.current = "3.14159265359";
        },

        inverse() {
            this.current = String(1 / parseFloat(this.current));
        },
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .calculator {
        display: grid;
        font-size: 30px;
        font-weight: bold;
        grid-template-columns: repeat(4, 1fr);
        grid-template-rows: minmax(50px, auto);
        margin: 0 auto;
        width: 400px;
    }

    .clear {
        background-color: green;
        color:  white;
    }

    .display {
        grid-column: 1 / 5;
        padding-right: 5px;
        padding-top: 5px;
        text-align: right;
    }

    .key {
        border: 1px solid black;
    }

    .operator {
        background-color:  blue;
        color: white;
    }

    .zero {
        grid-column: 1 / 3;
    }

</style>
