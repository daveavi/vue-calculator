<template>
    <div class="calculator"> 
        <div class="display">{{current || 0}}</div> 
        <div @click="clear" class="btn">C</div>
        <div @click="sign" class="btn">+/-</div>
        <div @click="percentage" class="btn">%</div>
        <div @click="divide" class="btn operator">/</div>
        <div @click="append('7')" class="btn">7</div>
        <div @click="append('8')" class="btn">8</div>
        <div @click="append('9')" class="btn">9</div>
        <div @click="multiply" class="btn operator">x</div>
        <div @click="append('4')" class="btn">4</div>
        <div @click="append('5')" class="btn">5</div>
        <div @click="append('6')" class="btn">6</div>
        <div @click="subtract" class="btn operator">-</div>
        <div @click="append('1')" class="btn">1</div>
        <div @click="append('2')" class="btn">2</div>
        <div @click="append('3')" class="btn">3</div>
        <div @click="add" class="btn operator">+</div>
        <div @click="append('0')" class="btn zero">0</div>
        <div @click="dot" class="btn">.</div>
        <div @click="equal" class="btn operator">=</div>
    </div>
</template>

<script> 
export default{
    data(){
        return{
            current: '',
            previous: '',
            multVal: '',
            divVal: '',
            operation: '',
            operationClicked: false
        }
    },
    methods: {
        clear: function(){
            this.current = '0';
            this.previous = '';
            this.operation = '';
            this.operation = false;
        },
        sign: function(){
            if(this.current !='0'){
                this.current = this.current.charAt(0) === '-' ? this.current.slice(1): `-${this.current}`;
            }
        },
        percentage: function(){
            this.current = `${parseFloat(this.current)/100}`;
        },
        append: function(number){
            if(this.current != '0' && !this.operationClicked){
                this.current = `${this.current}${number}`
            // }else if(this.operation != '/' || this.operation != 'x'){
            //     this.previous = this.current;
            //     this.current = `${number}`
            //     this.operationClicked = false;
            // }
            }else{
              this.previous = this.current;
              this.current = `${number}`
              this.operationClicked = false;  
            }
            console.log(this.current);
            console.log(this.previous);
            //this.current = `${this.current}${number}`
        },
        dot: function(){
            if(this.current.indexOf('.') === -1){
                this.append('.')
            }
        },

        divide: function(){
            if(this.previous == ''){
                this.previous = this.current
                console.log(this.previous)
            }else{
                if(this.operation == '/' ){
                    this.current = `${parseFloat(this.previous)/parseFloat(this.current)}`
                    this.previous = '';
                }else{
                    console.log("I am here");
                    
                    this.equal(); 
                }
            }
            this.operationClicked = true;
            this.operation = '/';

        },

        multiply: function(){
            if(this.previous == ''){
                this.previous = this.current
            }else{
                if(this.operation == 'x'){
                    this.current = `${parseFloat(this.previous)*parseFloat(this.current)}`
                    this.previous = '';
                }else{
                    console.log("I am here");
                    this.equal(); 
                }
            }
            this.operationClicked = true;
            this.operation = 'x';

        },


        subtract: function(){
            if(this.previous == ''){
                this.previous = this.current
                console.log(this.previous)
            }else{
                if(this.operation == '-' ){
                    this.current = `${parseFloat(this.previous) - parseFloat(this.current)}`
                    this.previous = '';
                }else{
                    console.log("I am here");
                    this.equal(); 
                }
            }
            this.operationClicked = true;
            this.operation = '-';

        },
        add: function(){
            if(this.previous == ''){
                this.previous = this.current
            }else{
                if(this.operation == '+' ){
                    this.current = `${parseFloat(this.current) + parseFloat(this.previous)}`
                    this.previous = '';
                }else{
                    this.equal(); 
                }
            }
            this.operationClicked = true;
            this.operation = '+';

        },
        equal: function(){
            if(this.previous != ''){
                switch(this.operation) {
                    case '+':
                        this.add();
                        break;
                    case '-':
                        this.subtract();
                        break;
                    case 'x':
                        this.multiply();
                        break;
                    case '/':
                        this.divide();
                        break;
                    
                    default:
                    }
            }
            
        }
    }

}
</script> 

<style scooped> 
.calculator {
    margin: 0 auto;
    font-size:40px;
    width: 400px;
    display: grid;  
    grid-template-columns: repeat(4,1fr);
    grid-auto-rows: minmax(50px, auto);
}
.display{
    grid-column: 1/5;
    background-color:teal;
}
.zero{
    grid-column: 1/3;
}
.btn{
    border:1px solid black;
    background-color: white
}
.operator{
    background-color: orange;
    color:white;
} 
</style>