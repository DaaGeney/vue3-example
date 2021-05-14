<template>
    <Child :msg="message" @updateMsg="onUpdateValue" />
</template>

<script>
import Child from '../childs/Child.vue2.vue';
export default {
    name: 'ParentVue2',
    components: {
        Child
    },
    data () {
        return {
            message: 'Hello world from vue 2'
        }
    },
    methods: { 
        onUpdateValue(newMessage) {
            this.message = newMessage
        }
    }
}
</script>