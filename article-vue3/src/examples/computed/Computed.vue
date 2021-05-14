<template>
    <h1>{{ message }}</h1>
    <button @click="onUpdateValue()"> Click me</button>
</template>

<script>
import { ref, computed } from 'vue';
export default {
    setup() {
        const part1 = ref("Hello World");
        const part2 = ref("from vue 3");
        const message = computed(() => `${part1.value} ${part2.value}`);
        const onUpdateValue = () => {
            part2.value = "the second part was update from vue 3";
        }
        return { message, onUpdateValue }
    },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
