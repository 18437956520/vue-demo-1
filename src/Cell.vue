<template>
    <div>
        <div class="cell" v-on:click="onClickSelf">
            <template v-if="a">
                <div v-if="X" class="X">
                    <div class="x1"></div>
                    <div class="x2"></div>
                </div>
                <div v-if="O" class="O"></div>
            </template>
            <template v-else></template>
        </div>
    </div>
</template>

<script>
    export default {
        props: ["n"],
        data() {
            return {
                a: false,
                text:""
            }
        },
        methods: {
            onClickSelf() {
                if(this.text!==""){
                    return
                }
                this.a = true;
                if (this.n % 2 === 0) {
                    this.X = true
                    this.O = false
                    this.text = "X"
                } else {
                    this.X = false
                    this.O = true
                    this.text = "O"
                }
                this.$emit("click",this.text);
            }
        }
    }
</script>

<style>
    .O {
        width: 50px;
        height: 50px;
        border-radius: 50%;
        border: 5px solid rgb(255, 0, 0);
    }

    .x1 {
        border: 5px solid black;
        background-color: black;
        width: 50px;
        transform: rotate(45deg);
        position: absolute;
    }

    .x2 {
        border: 5px solid black;
        background-color: black;
        width: 50px;
        transform: rotate(135deg);
    }

    .cell {
        border: 3px solid black;
        width: 80px;
        height: 80px;
        display: flex;
        flex-wrap: nowrap;
        justify-content: center;
        align-items: center;
        margin: 0px 0px -3px -3px;
    }
</style>