<template>
<div class="container ">
    <div class="row">
        <div class="col-md-6 mx-auto">
            <div class="card text-center">
                <div class="card-header bg-info">
                    <h1>To Do</h1>
                </div>
                <div class="card-body  ">
                    <form @submit.prevent="addTodo()" class="d-flex mb-2">
                        <input v-model="todoInput" type="text" class="form-control me-2">

                        <button type="submit" class="btn btn-success">
                            <i class="bi bi-plus-lg"></i>
                        </button>
                    </form>
                    <div class="input-group rounded mb-3">
                        <input v-if="isSearcch" v-model="searchQuery" type="search" class="form-control rounded" placeholder="Search" aria-label="Search" aria-describedby="search-addon" />
                        <button @click="showSearch" class="btn">
                            <i class="bi bi-search"></i>
                        </button>

                    </div>
                    <ul class="list-group">
                        <li v-for="(todo,index) in fiterTodos" :key="index" :style="{  backgroundColor: todo.isComplete ? 'Salmon' : 'PaleGreen' }" class="list-group-item d-flex justify-content-between mb-2">
                            <div>
                                <h3>{{ todo.value }}</h3>
                            </div>
                            <div>
                                <button @click="completeTask(todo)" class="btn  me-2"><i class="bi bi-check"></i></button>
                                <button @click="deleteTodo(index)" class="btn "><i class="bi bi-trash"></i></button>
                            </div>
                        </li>

                    </ul>

                </div>

            </div>
        </div>
    </div>
</div>
</template>

<script>
export default {
    name: 'HelloWorld',

    data() {
        return {
            todos: [],
            todoInput: null,
            isTaskComplete: false,
            isSearcch: false,
            searchQuery: ''
        }
    },
    computed:{
        fiterTodos(){
            if(!this.searchQuery){
                return this.todos;
            }
            return this.todos.filter(el=>{
                return el.value.toString().toLowerCase().includes(this.searchQuery.toString().toLowerCase());
            })
        }
    },
    methods: {
        addTodo() {
            this.todos.push({
                value: this.todoInput,
                isComplete: false
            });
            this.todoInput = null;
        },
        deleteTodo(index) {
            this.todos.splice(index, 1);
        },

        completeTask(todo) {
            todo.isComplete = true;
        },
        showSearch() {
            this.isSearcch = !this.isSearcch
        },

    },
    
 
}

</script>
