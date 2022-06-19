<script setup>
        import { ref } from 'vue';
        import '../assets/styles/checkbox.css';
        
    const props = defineProps({
        title: { type: String, required: true},
        done: { type: Boolean, required: true, default: false}
    });
    const emits = defineEmits({ 
        changeStatus: Object
    });
    const status = ref(props.done);
</script>

<template>
    <input class="input-checkbox" type="checkbox" v-model="status" @click="emits('changeStatus', {title: props.title, done: !status})"/>
</template>