<template>
    <h1>{{ message }}</h1>
    <input v-model="dataInput" />
    <button @click="onUpdateValue()"> Click me</button>
</template>

<script>
import { ref, watch, reactive } from 'vue'; //(Remember that reactive is for objects and ref is for primitive types)
export default {
    setup() {
        const part1 = ref("Hello World");
        const part2 = ref("from vue 3");
        const dataInput = ref("");
        const obj = reactive({
            data: ''
        })
        const message = ref('Hello World from vue 3');
        const onUpdateValue = () => {
            part2.value = dataInput.value;
        }
        watch(part2,
            (value, oldValue) => {
            message.value = `${part1.value} ${value}`;
            console.log(oldValue, 'old value')
        })
        // this is the form for use watch with reactive object 
        watch(() => obj.data, (current, old) => {
            console.log(current, old)
        }, { deep: true }); // deep: true is for reactivity at all levels

        return { message, onUpdateValue, dataInput }
    },
}
</script>

<style scoped>

</style>
