<template>
        <li>
            <input type="checkbox" @click="$emit('toggle')" v-model="todoitem.seen"/>
            <!--<input type="checkbox" @click="$emit('toggle')" v-bind:value="todoitem.seen" v-on:input="todoitem.seen = $event.target.value"/>-->
            <span v-if="todoitem.seen">{{ todoitem.text }}</span>
        </li>
</template>

<script>
    export default {
        name: 'Todoitem',
        props: ['todoitem'], // propriétés de l'instance du composant
        data() { // data doit être une fonction afin que chaque instance puisse conserver une copie indépendante de l'objet retourné
            return {
                seen: true
            }
        }
    }

</script>

<style scoped>

</style>