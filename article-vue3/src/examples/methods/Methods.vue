<template>
   <button @click="onShowAlert()"> Click me </button>
</template>

<script>
import { ref } from 'vue';
export default {
    setup() {
        const message = ref("Hello World from vue 3")
        const onShowAlert = () => {
            alert(message.value)
        }
        return { onShowAlert }
    }
}
</script>

<style scoped />
