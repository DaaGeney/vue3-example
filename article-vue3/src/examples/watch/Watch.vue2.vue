<template>
    <div>
        <h1>{{ message }}</h1>
        <input v-model="dataInput" />
        <button @click="onUpdateValue()"> Click me</button>
    </div>
</template>

<script>
export default {
    data () {
        return {
            part1: 'Hello world',
            part2: 'from vue 2',
            message: 'Hello from vue 2',
            dataInput: ''
        }
    },
    watch: {
        part2: function (val, oldValue) {
            this.message = `${this.part1} ${val}`;
            console.log(oldValue, 'the old value')
        }
    },
    methods: {
        onUpdateValue() {
            this.part2 =  this.dataInput
        }
}   
}
</script>
