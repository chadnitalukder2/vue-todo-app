<template>
    <div id="app">
      <div class="container">
        <h1>Todo List App</h1>
        <div class="search-box">
          <input v-model="todo" type="text" placeholder="Add Todo" />
          <button type="submit" @click="addList()">Add</button>
        </div>
        <ol>
          <li v-for="(todo, index) in todos" :key="index">
            <div class="info">
              <span>{{ todo.id }}.</span>
              <p :class="todo.complete == 'yes' ? 'complete' : ''">
                {{ todo.title }}
              </p>
            </div>
            <div class="action">
              <input @click="todoUpdate(index)" type="checkbox" id="myCheckbox" />
  
              <button @click="deleteTodo(index)">Delete</button>
            </div>
          </li>
        </ol>
      </div>
    </div>
  </template>
  
  <script>
  import myTodos from "./data.js";
  export default {
    data() {
      return {
        todos: [],
        todo: "",
      };
    },
    methods: {
      addList() {
        if (!this.todo) {
          return alert("Please enter your todo");
        }
        let data = {
          id: this.todos.length + 1,
          title: this.todo,
          complete: "no",
        };
        this.todos.push(data);
        this.todo = "";
      },
      deleteTodo(index) {
        this.todos = this.todos.filter((todo, toIndex) => toIndex !== index);
      },
      todoUpdate(index) {
        if (this.todos[index].complete == "no") {
          this.todos[index].complete = "yes";
        } else {
          this.todos[index].complete = "no";
        }
      },
    },
  
    mounted() {
      this.todos = myTodos;
    },
  };
  </script>
  
  <style lang="scss">
  * {
    margin: 0;
    padding: 0;
    font-family: "popins", sans-serif;
    box-sizing: border-box;
  }
  #app {
    background: #4eadd4;
    padding: 50px;
    height: 100vh;
  }
  .container {
    width: 100%;
    max-width: 600px;
    margin: 0 auto;
    background: #fff;
    text-align: center;
    border-radius: 8px;
    padding: 20px;
  
    .search-box {
      padding-bottom: 50px;
      input {
        width: 500px;
        height: 40px;
        border: none;
        border: 1px solid #21252942;
        border-right: 0;
        padding-left: 20px;
        font-size: 16px;
        border-radius: 5px 0 0 5px;
        &:focus-visible {
          outline: 0.5px solid #4eadd4;
        }
      }
      button {
        height: 40px;
        font-size: 16px;
        width: 60px;
        border: none;
        border: 1px solid rgb(155 158 161 / 21%);
        border-left: 0;
        border-radius: 0 5px 5px 0;
        background: #4eadd4;
        color: #fff;
      }
    }
  
    h1 {
      font-size: 40px;
      font-weight: 700;
      padding-bottom: 30px;
      color: #333;
    }
  
    ol {
      li {
        display: flex;
        justify-content: space-between;
        padding: 10px 0;
        border-bottom: 1px solid #0000002e;
        .info {
          display: flex;
          gap: 30px;
          .complete {
            text-decoration: line-through;
          }
        }
        .action {
          display: flex;
          gap: 8px;
          align-items: center;
          input {
            width: 20px;
            height: 20px;
          }
          button {
            padding: 6px;
            font-size: 16px;
            color: #fff;
            background: red;
            border: 1px solid rgb(155 158 161 / 21%);
            border-radius: 5px;
          }
        }
        &:last-child {
          border-bottom: none;
        }
      }
    }
  }
  </style>
  