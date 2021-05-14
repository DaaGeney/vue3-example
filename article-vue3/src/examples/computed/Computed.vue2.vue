<template>
    <div>
        <h1>{{ message }}</h1>
        <button @click="onUpdateValue()"> Click me</button>
    </div>
</template>

<script>
export default {
  data () {
    return {
      part1: 'Hello world',
      part2: 'from vue 2'
    }
  },
  computed: {
      message: function () {
        return `${this.part1} ${this.part2}`;
      }
    },
    methods: {
        onUpdateValue() {
            this.part2 = 'the second part was update from vue 2'
        }
    }
}
</script>
