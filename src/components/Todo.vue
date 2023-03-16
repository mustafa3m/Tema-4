<template>
  <div class="todo">
    <h2>Add todo</h2>
    <div class="todo__add">
      <input v-model="todo" type="text" />
      <!-- modification of the template to pass the payload to addTodo -->
      <button @click="addTodo({ name: todo, done: false })">Add</button>
    </div>
    <div class="todo__liste">
      <p><span>todo list</span></p>
      <!-- display the length of the todos -->
      <span class="todo__chip todo__purple"> {{ todosLength }} </span>
    </div>
    <!-- iterate over todos -->
    <ul @click="toggleTodo(index)" v-for="(todo, index) in todos" :key="index">
      <li class="todo__liste">
        <span class="todo__name todo__done"> {{ todo.name }} </span>

        <!-- delete the  todo -->
        <button class="todo__right todo__button" @click="deleteTodo(index)">
          delete
        </button>
      </li>
    </ul>
  </div>
</template>

<script>
  import { mapGetters, mapMutations } from "vuex";

  export default {
    data() {
      return {
        todo: "",
      };
    },
    /* add a calculated property */
    computed: {
      todos() {
        return this.$store.state.todos;
      },
      ...mapGetters(["todosLength"]),
    },
    methods: {
      /* The mapMutations will automatically add the passed parameter if the mutation uses a payload. */
      ...mapMutations(["addTodo", "deleteTodo"]),
    },
  };
</script>

<style scoped>
  .todo {
    width: 500px;
    border: 1px solid #eee;
    border-radius: 3px;
    padding: 20px;
    display: flex;
    flex-direction: column;
    width: 100%;
    margin-top: 50px;
  }
  .todo__add {
    display: flex;
    margin-bottom: 20px;
  }

  button {
    padding: 5px 15px;
    border: 0px;
    border-radius: 5px;
    cursor: pointer;
    margin: 0 3px;
  }
  input {
    padding: 8px 15px;
    outline: 0;
    border: 1px solid #ddd;
    border-radius: 3px;
  }

  .todo__add input {
    flex: 1;
    margin-right: 15px;
  }

  ul {
    padding: 0;
    list-style: none;
  }

  li {
    display: flex;
    align-items: center;
  }

  li p {
    flex: 1;
  }
  li .todo__name {
    flex: 0 0 20px;
    height: 20px;
    border-radius: 30px;
    margin-right: 15px;
    border: 2px solid #333;
    margin-top: 50px;
  }

  li .todo__name .todo__done {
    background: #333;
  }
  .todo__liste {
    display: flex;
    justify-content: space-between;
    gap: 200px;
  }

  .todo__right {
    margin-left: 100px;
  }

  .todo__button {
    color: red;
    font-size: 3rem;
  }

  .todo__chip {
    display: inline-block;
    text-align: center;
    width: 50px;
    border-radius: 100%;
    background: #333;
    color: white;
  }

  .todo__purple {
    background: #be418c;
  }

   @media only screen and (max-width: 600px) {
    
  }
</style>
