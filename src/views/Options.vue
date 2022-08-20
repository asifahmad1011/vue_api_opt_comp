<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <h3>you have {{ todosCount }} to todos!</h3>
    <div>
      <input v-model="newTodoName" @keyup.enter="addTodo" placeholder="Add a todo" type="text">
    </div>
    <div>
      <ul>
        <li v-for="(todo, index) in todos" :key="todo.id">
          <span>{{ todo.name }}</span>
          <button @click="deleteTodo(index)">X</button>
        </li>

      </ul>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src

export default {
  data() {
    return {
      newTodoName: '',
      todos: [
        {
          id: 1,
          name: "One"
        },
        {
          id: 2,
          name: "Two"
        },
        {
          id: 3,
          name: "Three"
        }
      ],
      badwords: ["ugly", "fart"]
    }
  },

  computed: {
    todosCount() {      
      return this.todos.length
    }
  },
  // mounted() {
  //   console.log(`the component is now mounted.`)
  // },

  methods: {
    addTodo() {
      if (this.newTodoName != '') {
        let newTodo = {
          id: Date.now(),
          name: this.newTodoName
        }
        this.todos.push(newTodo)
        this.newTodoName = ''
      }
    },
    deleteTodo(id) {
      this.todos.splice(id, 1)

    }
  },

  watch: {
    newTodoName(newValue) {
      if (this.badwords.includes(newValue.toLowerCase())) {
        this.newTodoName = ''
        alert("you cannot use " + newValue + " word !")
      }
    }
  }


}
</script>

<style>
ul {
  list-style: none;
  padding: 0;
  width: 200px;
  margin: 20px auto 0;
}

li {
  border: 1px solid;
  display: flex;
  margin-bottom: 10px;
}

li span {
  flex-grow: 1;
}
</style>