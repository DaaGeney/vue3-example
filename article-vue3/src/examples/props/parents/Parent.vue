<template>
    <Child :msg="message" @updateMsg="onUpdateValue" />
</template>

<script>
import Child from '../childs/Child.vue2.vue';
import { ref } from 'vue';
export default {
    name: 'ParentVue3',
    components: {
        Child
    },
    setup() {
        const message = ref("Hello World from vue 3")
        const onUpdateValue = (newMessage) => {
            message.value = newMessage
        }
        return { onUpdateValue, message }
    }
}
</script>

<style scoped />
