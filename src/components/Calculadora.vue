<template>
    <div class="min-h-screen bg-gray-400 flex items-center justify-center">

        <div class="bg-black border-2 border-gray-900 shadow-2xl rounded-lg">
            <!-- form goes here -->
            <!-- <form class="border-b-2 border-gray-900">
            <input type="number" class="bg-transparent p-8 rounded-t-lg outline-none focus:bg-gray-700 text-3xl text-right text-white font-mono" value = {{current}} >
            </form> -->

            <form class="border-b-2 border-black">
                <div class="bg-transparent p-8 rounded-t-lg outline-none focus:bg-black text-3xl text-right text-white font-mono"> {{current || '0'}}</div>
            </form>

            <div class="p-6 text-gray-800 grid grid-cols-4 gap-4 text-xl">
                <button @click="clear()" class="font-mono col-span-3 bg-gray-400 hover:bg-gray-300 rounded-full">C</button>
                <button @click="divide()" class="font-mono text-white bg-yellow-500 hover:bg-white  hover:text-yellow-500 h-16 w-16 rounded-full">&divide;</button>

                <button @click="append('7')" class="font-mono text-white bg-gray-800 hover:bg-gray-700 h-16 w-16 rounded-full">7</button>
                <button @click="append('8')" class="font-mono text-white bg-gray-800 hover:bg-gray-700 h-16 w-16 rounded-full">8</button>
                <button @click="append('9')" class="font-mono text-white bg-gray-800 hover:bg-gray-700 h-16 w-16 rounded-full">9</button>
                <button @click="times()" class="font-mono text-white bg-yellow-500 hover:bg-white  hover:text-yellow-500 h-16 w-16 rounded-full">&times;</button>

                <button @click="append('4')" class="font-mono text-white bg-gray-800 hover:bg-gray-700 h-16 w-16 rounded-full">4</button>
                <button @click="append('5')" class="font-mono text-white bg-gray-800 hover:bg-gray-700 h-16 w-16 rounded-full">5</button>
                <button @click="append('6')" class="font-mono text-white bg-gray-800 hover:bg-gray-700 h-16 w-16 rounded-full">6</button>
                <button @click="minus()" class="font-mono text-white bg-yellow-500 hover:bg-white  hover:text-yellow-500 h-16 w-16 rounded-full">&minus;</button>

                <button @click="append('1')" class="font-mono text-white bg-gray-800 hover:bg-gray-700 h-16 w-16 rounded-full">1</button>
                <button @click="append('2')" class="font-mono text-white bg-gray-800 hover:bg-gray-700 h-16 w-16 rounded-full">2</button>
                <button @click="append('3')" class="font-mono text-white bg-gray-800 hover:bg-gray-700 h-16 w-16 rounded-full">3</button>
                <button @click="add()" class="font-mono text-white bg-yellow-500 hover:bg-white  hover:text-yellow-500 h-16 w-16 rounded-full">&plus;</button>

                <button @click="append('0')" class="font-mono col-span-2 text-white bg-gray-800 hover:bg-gray-700 rounded-full p-5">0</button>
                <button @click="dot()" class="font-mono text-white bg-gray-800 hover:bg-gray-700 h-16 w-16 rounded-full">.</button>
                <button @click="equal()" class="font-mono text-white bg-yellow-500 hover:bg-white  hover:text-yellow-500 h-16 w-16 rounded-full">&equals;</button>
            </div>
        </div>

    </div>
</template>

<script>
export default {
    name: 'Calculadora',
    data(){
        return{
            previous: null,
            current: '',
            operator: null, 
            operatorClicked: false,
        }
    },
    methods:{
        clear() {
            this.current = '';
        },
        append(number) {
            if (this.operatorClicked) {
                this.current = '';
                this.operatorClicked = false;
            }
            this.current = `${this.current}${number}`;
        },
        dot() {
            if (this.current.indexOf('.') === -1) {
                this.append('.');
            }
        },
        setPrevious() {
            this.previous = this.current;
            this.operatorClicked = true;
        },
        divide() {
            this.operator = (a, b) => b / a;
            this.setPrevious();
        },
        times() {
            this.operator = (a, b) => a * b;
            this.setPrevious();
        },
        minus() {
            this.operator = (a, b) => b - a;
            this.setPrevious();
        },
        add() {
            this.operator = (a, b) => a + b;
            this.setPrevious();
        },
        equal() {
            this.current = `${this.operator(
                parseFloat(this.current), 
                parseFloat(this.previous)
            )}`;
            this.previous = null;
        }
    }
}
</script>
