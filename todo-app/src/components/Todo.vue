<template>
  <div class="container">
    <h2 class="text-center mt-5">My Vue Todo App</h2>

    <!-- Input -->
    <div class="d-flex">
      <input v-model="task" type="text" placeholder="Enter task" class="form-control">
      <button @click="submitTask" class="btn btn-warning rounded-0">SUBMIT</button>
    </div>

    <!-- Task table -->
    <table class="table table-bordered mt-5">
      <thead>
      <tr>
        <th scope="col">Task</th>
        <th scope="col">Status</th>
        <th scope="col" class="text-center">#</th>
        <th scope="col" class="text-center">#</th>
      </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td>{{ task.name }}</td>
          <td>{{ task.status }}</td>
          <td>
            <div class="text-center">
              <span class="fa fa-pen"></span>
            </div>
          </td>
          <td>
            <div class="text-center" @click="deleteTask(index)">
              <span class="fa fa-trash"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      task: 'Hello World!!!',
      tasks: [
        {
          name: 'Steal bananas',
          status: 'To-do'
        },
        {
          name: 'Eat chocolte',
          status: 'In progress'
        }
      ]
    }
  },

  methods: {
    submitTask() {
      if(this.task.length === 0) return;

      this.tasks.push({
        name: this.task,
        status: 'To-do'
      });

      this.task = '';
    },

    deleteTask(index) {
      this.tasks.splice(index, 1);
    }
  }
}
</script>


<style scoped>

</style>
