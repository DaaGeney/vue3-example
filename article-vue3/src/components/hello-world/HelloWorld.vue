<template>
  <h1>{{ message }}</h1>
</template>

<script>
import { ref } from 'vue';
export default {
    setup() {
        const message = ref("Hello World since vue 3")
        return { message }
    },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
