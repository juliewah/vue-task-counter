<!-- <script>
export default{
    data(){
        return{
            num: 0,
        }
    },
    methods:{
        plus(){
            this.num ++
        },
        minus(){
            this.num--
        },
    }
}
</script> -->

<!-- <script>
// 取代data
import { ref } from "vue"
export default{
    setup(){
        const num = ref(100)

        const plus = () => {
            // ref回傳一個物件
            num.value++
        }

        const minus = () => {
            num.value--
        }

        return {
            num,
            plus,
            minus
        }
    }
}
</script> -->

<script setup>
import { ref, reactive, toRefs } from 'vue'

// ref 寫法
// const num = ref(0)

// const plus = () => {
//     // ref回傳一個物件
//     num.value++
// }

// const minus = () => {
//     num.value--
// }

// const twice = () =>{
//     num.value = num.value*2
// }

// reactive 寫法 裡面要放物件
const count = reactive({
    num: 0,
    plus: () => {
        count.num++
    },
    minus: () => {
        count.num--
    }
})

// reactive 解構
const { num, plus, minus } = toRefs(count)
</script>


<template>
    <div class="counter">
        <button @click="plus">+1</button>
        <p class="number">{{ num }}</p>
        <button @click="minus">-1</button>
        <!-- <p v-if="num == 0">小於零</p> -->
    </div>
</template>
<style>
.counter{
    display: flex;
}
.number, button{
    font-size: 24px;
    font-weight: 700;
    padding:0 30px;
}
button{
    border: 1px solid #333;
}
</style>