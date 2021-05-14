<template>
    <p> {{ props.msg }}</p>
    <input v-model="dataInput" />
    <button @click="onUpdateValue()"> change value </button>
</template>

<script>
import { ref } from 'vue';
export default {
    name: 'ChildVue',
    props: {
        msg: {
            type: String,
            required: true
        }
    },
    emits: ['updateMsg'],
    setup(props, { emit }) {
        const dataInput = ref('');
        const onUpdateValue = () => {
            emit("updateMsg", dataInput.value)
            alert('The text has been updated by child')
        }
        return { dataInput, onUpdateValue }
    }
}
</script>

<style scoped />
