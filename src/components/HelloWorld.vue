<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div class="ui grid container">
      <div class="four wide column"></div>
        <ul v-if="tasks && tasks.length">
          <li v-for="task of tasks" class="task">
            <p><strong>{{task.name}}</strong></p>
            <p>{{task.id}}</p>
          </li>
        </ul>
        <ul v-if="errors && errors.length">
          <li v-for="error of errors">
            {{error.message}}
          </li>
        </ul>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
//import {Collections} from 'semantic-ui-vue2'

export default {

  name: 'HelloWorld',


  data () {
    return {
      msg: 'Welcome to Vue.js App - Lab5',
      tasks: [],
      errors: []
    }
  },

  async created() {
    let taskURL2 = "https://glo3102lab4.herokuapp.com/84a90528-73d1-4ad3-8584-124252a42c7d/tasks";
    let taskIdUpdate = "https://glo3102lab4.herokuapp.com/84a90528-73d1-4ad3-8584-124252a42c7d/tasks/09344174-2ed5-489d-b906-3c7e37353572";
    let taskIdDelete = "https://glo3102lab4.herokuapp.com/84a90528-73d1-4ad3-8584-124252a42c7d/tasks/9bb1c102-e453-4bc8-be94-6b0547f06e6a";

    axios.post(taskURL2, {name: "programming..."})
      .catch(e => {this.errors.push(e)});

    axios.get(taskURL2)
      .then(response => this.tasks = response.data.tasks)
      .catch(e => {this.errors.push(e)});

    axios.put(taskIdUpdate, {name: "tp1 finished"})
      .catch(e => {this.errors.push(e)});

    axios.delete(taskIdDelete)
      .then(response => this.tasks = response.data)
      .catch(e => {this.errors.push(e)});
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.task{
    border: solid gray 1px;
  }
</style>
