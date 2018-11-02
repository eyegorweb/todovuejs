<template>
        <li>
            <input type="checkbox" v-bind:checked="todoitem.isFinished" v-on:input="$event.target.checked = todoitem.isFinished">
            <input type="text" v-if="todoitem.isEditing" v-model="todoitem.text"  v-on:keyup.enter="todoitem.isEditing = false">
            <span v-else @dblclick="todoitem.isEditing = true">{{ todoitem.text }}</span>
            <button @click="$emit('remove')">X</button>
        </li>
</template>

<script>
    export default {
        name: 'Todoitem',
        props: ['todoitem'], // propriétés de l'instance du composant
        data() { // data doit être une fonction afin que chaque instance puisse conserver une copie indépendante de l'objet retourné
            return {
                // toto: true
            }
        }
    }

</script>

<style scoped>

</style>