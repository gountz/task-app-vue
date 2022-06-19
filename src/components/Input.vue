<script setup>
    import '../assets/styles/input.css';
    
    const props =  defineProps({name: { type: String, default: '' }})
    const emits = defineEmits({
        catchTask: String,
    })
</script>

<template>
    <div class="input-container">
        <input type="text" v-model="name" class="input-form" placeholder="Insert task here"/>
        <button type="button" class="btn" @click="emits('catchTask', props.name)">AÑADIR</button>
    </div>
</template>