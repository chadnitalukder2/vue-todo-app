<template>
<div class="app-todo">
    <div class="container">
        <h1>My To-Do List</h1>

        <div class="search-box">
            <input v-model="todo" type="text" placeholder="Add you text...">
            <button @click="addTodo()">Add</button>
        </div>

        <ul>
            <li  v-for="(todo,index) in todos" :key="index">
                <div class="info">
                    <span>{{ todo.id }}.</span>
                    <p :class="todo.complete === 'yes' ? 'complete' : '' ">
                        {{ todo.title }}</p>
                    
                </div>

                <div class="action">
                    <input @click="todoUpdate(index)" type="checkbox">
                    <button @click="deleteTodo(index)">Delete</button>

                </div>
            </li>
        </ul>

    </div>
</div>
</template>

<script>
export default {
name:"A_MyTodo",
data(){
    return{
        todo: "",
        todos:JSON.parse(localStorage.getItem("todos")) || [],
    }
},
methods:{
    addTodo(){
        if (!this.todo) {
          return alert("Please enter your todo");
        }
        let data ={
              title: this.todo,
              id: this.todos.length + 1,
              complete: "no"
        };
        this.todos.push(data);
        this.saveToLocalStorage();
        this.todo =""
    },
    deleteTodo(index){
        this.todos = this.todos.filter((todo,toIndex) => toIndex != index )
        this.saveToLocalStorage();
    },
    todoUpdate(index){ 
        if(this.todos[index].complete === "no"){
            this.todos[index].complete = "yes"
        }
        else{
            this.todos[index].complete = "no"
        }
        this.saveToLocalStorage();
    },
    saveToLocalStorage() {
        localStorage.setItem("todos", JSON.stringify(this.todos));
      },
}

}
</script>

<style lang="scss" scoped>
*{
    margin: 0px;
    padding: 0px;
    font-family: 'Merriweather', sans-serif;
    box-sizing: border-box;
}
.app-todo{
    background: rgba(33, 37, 41, 0.07);
    padding: 50px;
    width: 100%;
    height: 100%;

}
.container{
    width: 100%;
    max-width: 600px;
    margin: 0 auto;
    background: #fff;
    text-align: center;
    border-radius: 8px;
    padding: 20px;
    h1{
        font-size: 30px;
        margin: 20px 0px 50px 0px;
        color: #333;
    }
    .search-box {
        border: 1px solid rgb(33 37 41 / 17%);
        margin-top: 40px;
        width: 100%;
        border-radius: 6px;
        margin-bottom: 40px;

        input {
            width: 82%;
            padding: 9px;
            border: none;
            outline: none;
            border-radius: 3px;
            &:focus-visible {
            outline: 0.5px solid rgb(151, 59, 236);
        }
         
        }

        button {
            width: 18%;
            padding: 10px;

            border: none;
            outline: none;
            background: rgb(33 37 41 / 17%);
        }

    }
    ul li {
    
        list-style: none;
        display: flex;
        justify-content: space-between;
        padding: 10px 0;
        border-bottom: 1px solid #0000002e;

        &:last-child {
          border-bottom: none;
        }
        .info {
            display: flex;
            gap: 20px;

            .complete {
                text-decoration: line-through;
            }
        }

        .action {
            display: flex;
            gap: 20px;

            input {
                padding: 10px;
            }

            button {
                border: 1px solid rgb(33 37 41 / 17%);
                outline: none;
                padding: 6px 8px;
                background: rgb(151, 59, 236);
                border-radius: 4px;
                color: white;
            }
        }

    }
}
</style>
