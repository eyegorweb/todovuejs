<template>
        <li>
            <input type="checkbox" v-model="_isFinished">
            <input type="text" v-if="todoitem.isEditing" v-model="_text"  v-on:keyup.enter="todoitem.isEditing = false">
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
        },
        methods: {
            changeTodo(partialTodo){
                this.$emit('update', {
                    ...this.todoitem,
                    ...partialTodo
                })
            }
        },
        computed: {
            // https://vuejs.org/v2/guide/computed.html#Computed-Setter
            _isFinished: {
                get() {
                    return this.todoitem.isFinished;
                },
                set(isFinished) {
                    this.changeTodo({ isFinished })
                }
            },
            _text: {
                get(){
                    return this.todoitem.text;
                },
                set(text){
                    // console.log('change text', this.todoitem.text)
                    // console.log('change text', { text })
                    this.changeTodo({ text });
                }
            }
        }
    }

</script>

<style scoped>

</style>