<template>
    <h1>{{ message }}</h1>
    <input v-model="dataInput" />
    <button @click="onUpdateValue()"> Click me</button>
</template>

<script>
import { ref, watch } from 'vue';
export default {
    setup() {
        const part1 = ref("Hello World");
        const part2 = ref("since vue 3");
        const dataInput = ref("");
        const message = ref('Hello World since vue 3');
        const onUpdateValue = () => {
            part2.value = dataInput.value;
        }
        watch(part2,
            (value, oldValue) => {
            // side effect
            message.value = `${part1.value} ${value}`;
            console.log(oldValue, 'old value')
        })
        return { message, onUpdateValue, dataInput }
    },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
