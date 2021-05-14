<template>
    <div>
        <p> {{ msg }}</p>
        <input v-model="dataInput" />
        <button @click="onUpdateValue()"> change value </button>
    </div>
</template>

<script>
export default {
    name: 'ChildVue3',
    props: {
        msg: {
            type: String,
            required: true
        }
    },
    data () {
        return {
            dataInput: ''
        }
    },
    methods: {
        onUpdateValue() {
            this.$emit("updateMsg", this.dataInput)
            alert('The text has been updated by child')
        }
    }
}
</script>