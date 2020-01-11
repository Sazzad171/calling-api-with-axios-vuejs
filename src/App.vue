<template>
  <div id="app">
    <div v-for="todo in todos">
      <p> {{todo.title}} 
        <button>X</button>
      </p>
    </div>
    <addItem v-on:add-item="addItem"/>
  </div>
</template>


<script>
import addItem from './components/addItem'
import axios from 'axios'

export default {
  name: 'app',
  data() {
    return {
      todos: []
    }
  },

  components: {
    addItem
  },

  methods: {
    addItem(newItem) {
      const { title, completed} = newItem;
      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
      .then(res => this.todos = [...this.todos, res.data])
    }
  },
  
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=5')        //can be limit of data
      .then(res => this.todos = res.data)
      .catch(err => console.log(err));
  }
}
</script>
