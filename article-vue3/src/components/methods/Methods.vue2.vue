<template>
  <button @click="onShowAlert()"> Click me </button>
</template>

<script>
export default {
    data () {
        return {
            message: 'Hello world since vue 2'
        }
  },
    methods: { 
        onShowAlert() {
            alert(this.message)
        }
    }
}
</script>