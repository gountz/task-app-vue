<script setup>
    import '../assets/styles/todo.css';
    import Checkbox from './Checkbox.vue';
    import { ref } from 'vue';
    import Input from './Input.vue';
    import InputEdit from './InputEdit.vue';
    import '../assets/styles/todo.css';

    const props = defineProps({todos: { typeof: Object, required: true}});
    const emits = defineEmits({newStatus: Object, deleteTask: Object, editTle: Object });

    const dn = ref('');
    const changeStatus = ($event) => {
        emits('newStatus', $event);
    }
    const editTitle = ($event, todo) => {
        todo.edit = false;
        emits('editTle', $event);
    }
    const formatDate = (date) => {
        return new Intl.DateTimeFormat('en-US', { dateStyle: 'short' }).format(new Date(date))
    }
</script>

<template>
    <article class="table-container">
        <table v-if="props.todos.length > 0">
            <tr>
                <th>Completed</th>
                <th>Title</th>
                <th>Delete</th>
                <th class="flex-center">Edit</th>
                <th>Created</th>
            </tr>
            <tr v-for="(todo, index) in props.todos" :key="index">
                <td><Checkbox :title="todo.title" :done="todo.done" @changeStatus="changeStatus" /></td>
                <td>
                    <span v-if="!todo.edit" class="title-todo" :class="{ 'todo-completed': todo.done }">{{todo.title.toUpperCase()}}</span>
                    <InputEdit v-else :name="todo.title" :key="todo.title" @editTask="editTitle($event, todo)"/>
                </td>
                <td><button type="button" class="btn-delete" @click="emits('deleteTask', todo);"><i class='bx bxs-trash'></i></button></td>
                <td><button type="button" class="btn-edit" @click="todo.edit = !todo.edit"><i class='bx bxs-edit' ></i></button></td>
                <td class="format-date">{{formatDate(todo.createdAt)}}</td>
            </tr>
        </table>
        <div v-else>No hay tareas agregadas</div>
    </article>
</template>