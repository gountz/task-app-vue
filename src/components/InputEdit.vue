<script setup>
    import { ref} from 'vue';
    import '../assets/styles/input.css';
    
    const props =  defineProps({name: { type: String, required: true, default: '' }});
    const title = ref(props.name);
    const emits = defineEmits({
        editTask: String,
    });
</script>

<template>
    <div class="input-container">
        <input type="text" v-model="title" class="input-form" placeholder="Insert task here"/>
        <button class="btn-input btn-check" @click="emits('editTask', {original: props.name, title})"><i class='bx bx-check'></i></button>
        <button class="btn-input btn-input-delete" @click="title = ''"><i class='bx bx-x'></i></button>
    </div>
</template>