<template>
    <div class="flex flex-col">
        <input type="text" class="outline outline-2 outline-black text-xl mb-4 mt-4 px-4 py-4 w-[50%] mx-auto"
            placeholder="Enter your item here" v-model="newTodo" @keyup.enter="addTodo">
        <div class="ml-52 p-2">
            <div v-for="(todo, index) in todos" :key="todo.id" class="text-xl mb-3 flex justify-between w-[68%]">
                <div class="flex gap-x-5">
                        <input type="checkbox" v-model="todo.completed">
                        <div v-if="!todo.editing" @dblclick="editTodo(todo)" :class="{'line-through text-gray-500' : todo.completed}">{{ todo.title }}</div>
                        <input type="text"  v-else class="outline outline-1 outline-gray-500 px-2 py-1" v-model="todo.title" @blur="doneEdit(todo)" @keyup.enter="doneEdit(todo)" @keyup.esc="cancelEdit(todo)" v-focus>
                </div>
                <div class="cursor-pointer" @click="removeTodo(index)">
                    &times;
                </div>
            </div>
        </div>
    </div>
    
</template>

<script>
export default {
    name: 'todo-list',
    data() {
        return {
            newTodo: '',
            beforeEditCache: '',
            idForTodo: 3,
            todos: [
                {
                    " id": 1,
                    "title": "Learn vue framework",
                    "completed": false,
                    "editing": false,
                    
                },
                {
                    "id": 2,
                    "title": "Read rich dad poor dad book",
                    "completed": false,
                    "editing": false,
                },
            ],
            
        }
    },
    directives:{
        focus: {
            inserted: function (el) {
                el.focus()       
            }
        }
    },
    methods: {
             addTodo(){
                 if (this.newTodo.trim().length === 0) {
                     return
                 }
                 this.todos.push({
                     id: this.idForTodo,
                     title: this.newTodo,
                     completed: false,
                 })

                 this.newTodo = ''
                 this.idForTodo++
             },
             doneEdit(todo){
                 if (todo.title.trim() == '') {
                     todo.title = this.beforeEditCache
                 }
                 todo.editing = false
             },
             editTodo(todo){
                 this.beforeEditCache = todo.title
                todo.editing = true
             },
             cancelEdit(todo){
                 todo.title = this.beforeEditCache
                 todo.editing = false
             },
             removeTodo(index){
                 this.todos.splice(index, 1)
             }   
            }

}
</script>

<style scoped></style>