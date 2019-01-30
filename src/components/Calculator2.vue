<template>
    <div class="body">
    <h3>Calculator with VueJS, Bootstrap</h3>
        <b-container fluid class="calculator">
            <b-row align-h="center" class="display">
                {{ current || '0' }}
            </b-row>
            <b-row>
                <b-col @click="clear" cols="3" class="btn">AC</b-col>
                <b-col @click="sign" cols="3" class="btn">+/-</b-col>
                <b-col @click="percent" cols="3" class="btn">%</b-col>
                <b-col @click="divide" cols="3" class="btn operator">/</b-col>
            </b-row>
            <b-row>
                <b-col @click="append('7')" cols="3" class="btn">7</b-col>
                <b-col @click="append('8')" cols="3" class="btn">8</b-col>
                <b-col @click="append('9')" cols="3" class="btn">9</b-col>
                <b-col @click="times" cols="3" class="btn operator">x</b-col>
            </b-row>
            <b-row>
                <b-col @click="append('4')" cols="3" class="btn">4</b-col>
                <b-col @click="append('5')" cols="3" class="btn">5</b-col>
                <b-col @click="append('6')" cols="3" class="btn">6</b-col>
                <b-col @click="minus" cols="3" class="btn operator">-</b-col>
            </b-row>
            <b-row>
                <b-col @click="append('1')" cols="3" class="btn">1</b-col>
                <b-col @click="append('2')" cols="3" class="btn">2</b-col>
                <b-col @click="append('3')" cols="3" class="btn">3</b-col>
                <b-col @click="add" cols="3" class="btn operator">+</b-col>
            </b-row>
            <b-row>
                <b-col @click="append('0')" aria-colspan="" class="btn">0</b-col>
                <b-col @click="append('.')" cols="3" class="btn">.</b-col>
                <b-col @click="equal" cols="3" class="btn operator">=</b-col>
            </b-row>
        </b-container>
    </div>
</template>

<script>
export default {
    data() {
        return {
            previous: '',
            current: '',
            operator: null,
            isOperClicked: false,
        }
    },
    methods: {
        clear() {
            this.current = '';
            // console.log('clicked clear' + this.current);
        },
        sign() {
            // 개선해 보자
            this.current = -this.current;
        },
        append(num) {
            // 이렇게 작성하면 안되는 이유? 소수점 있어서 0도 append 시켜줘야 하거든..
            // this.current = this.current === '0' ? '' : this.current;
            // . 이 있어야 0 뒤에 0이 또 올 수 있음
            if(this.isOperClicked){
                this.current = '';
                this.isOperClicked = false;
            }
            this.current = `${this.current}${num}`;
            console.log('previous = ' + this.previous);
            console.log('current = ' +  this.current);
        },
        setPrevious() {
            this.isOperClicked = true;
            this.previous = this.current;
        },
        percent() {
            this.operator = (a, b) => a % b;
            this.setPrevious();
        },
        divide() {
            this.operator = (a, b) => a / b;
            this.setPrevious();
        },
        times() {
            this.operator = (a, b) => a * b;
            this.setPrevious();
        },
        minus() {
            this.operator = (a, b) => a - b;
            this.setPrevious();
        },
        add() {
            this.operator = (a, b) => a + b;
            this.setPrevious(); 
        },
        equal() {
            this.current = this.operator(parseFloat(`${this.previous}`),
            parseFloat(`${this.current}`));
        }
    }
}
</script>

<style scoped>
.body {
    font-family: -apple-system, Roboto, sans-serif;
    margin: 10px;
    text-align: center;
}
.calculator {
    font-size: 40px;
    display: grid;
}
.display {
    background : #605C5A;
    color: white;
    text-align: right;
}
.btn {
    font-size: 30px;
    background-color: #868380;
    color: white;
    border: outset 0.5px gray;
    border-radius: 0;
}
.btn:hover {
    background-color: #6F6D6B;
}
.operator {
    background-color: #F2A33B;
}
.operator:hover {
    background-color: #BF8230;
}
</style>
