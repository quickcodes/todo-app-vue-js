<template>
  <div class="container">
    <h2 class="text-center mt-5">My Vue Todo App</h2>

    <!-- Input -->
    <div class="d-flex">
      <input v-model="task" type="text" placeholder="Enter Text" class="form-control">
      <button @click="submitTask">SUBMIT</button>
    </div>

    <!-- Task Table -->
    <table class="table table-bordered">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col">#</th>
          <th scope="col">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <th>{{task.name}}</th>
          <td style="width: 120px">
            <span @click="changeStatus(index)" class="pointer"
              :class="{
                'text-danger': task.status === 'to-do',
                'text-success': task.status === 'finished',
                'text-warning': task.status === 'in-progress'
              }"
            >
              {{task.status}}
            </span>
          </td>
          <td>
            <div @click="editTask(index)">
              <span class="fa fa-pen"></span>
            </div>
          </td>
          <td>
            <div @click="deleteTask(index)">
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
      task: "",
      editedTask: null,
      availableStatuses: ['to-do', 'in-progress', 'finished'],

      tasks: [
        {
          name: 'Steal bananas from the store',
          status: 'to-do'
        },
        {
          name: 'Eat 1kg choclates in 1 hours',
          status: 'in-progress'
        }
      ]
    }
  },

  methods: {
    submitTask(){
      if(this.task.length === 0) return;

      if(this.editedTask === null){
        this.tasks.push({
          name: this.task,
          status: 'to-do'
        })
      }else{
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      }

      this.task = "";
    },

    deleteTask(index){
      this.tasks.splice(index, 1);
    },

    editTask(index){
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },

    changeStatus(index){
      let i = this.availableStatuses.indexOf(this.tasks[index].status);
      // console.log("THIS IS THE STATUS")
      // console.log(this.availableStatuses.indexof(this.tasks[index].status));
      // let i = this.availableStatuses[this.tasks[index].status];
      if(++i > 2) i = 0;
      this.tasks[index].status = this.availableStatuses[i];
      // console.log("THIS IS THE STATUS")
      // console.log(this.tasks[index].status)
      // console.log(this.availableStatuses.indexOf('to-do'))
    },
  }
}
</script>

<style scoped>
.pointer{
  cursor: pointer;
}
</style>