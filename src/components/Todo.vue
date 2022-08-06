<template>
  <div>
    <input type="text" placeholder="Enter task" v-model="text" />
    <button @click="addTask">Add task</button>
  </div>
  <table border="1">
    <tr>
      <th>Title</th>
      <th>Status</th>
      <th>Edit</th>
      <th>Delete</th>
    </tr>
    <tr v-for="(item, i) in tasks" :key="i">
      <td>{{ item.name }}</td>
      <td @click="changeStatus(i)">{{ item.status }}</td>
      <td class="edit" @click="editTask(i)">Edit</td>
      <td class="delete" @click="deleteTask(i)">Delete</td>
    </tr>
  </table>
</template>

<script>
export default {
  name: "Todo",
  data() {
    return {
      text: "",
      editedTask: null,
      statuses: ["to-do", "in-progress", "completed"],
      tasks: [
        {
          name: "Steal banana from the store",
          status: "to-do",
        },
        {
          name: "Eat 1kg chocolate in 1 hour",
          status: "in-progress",
        },
      ],
    };
  },
  methods: {
    addTask() {
      if (this.text.length == 0) return;

      if (this.text.length > 0 && this.editedTask == null) {
        let payload = {
          name: this.text,
          status: "To-do",
        };
        this.tasks.push(payload);
      } else {
        this.tasks[this.editedTask].name = this.text;
        this.editedTask = null;
      }
      this.text = "";
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(index) {
      // console.log(index,this.tasks[index].name)
      this.text = this.tasks[index].name;
      this.editedTask = index;
    },
    changeStatus(index) {
      let newIndex = this.statuses.indexOf(this.tasks[index].status);
      console.log(newIndex);
      ++newIndex;
      if (newIndex > 2) newIndex = 0;
      console.log(newIndex);
      this.tasks[index].status = this.statuses[newIndex];
    },
  },
};
</script>

<style>
.edit {
  color: red;
  padding: 10px;
  cursor: pointer;
}
.delete {
  color: orange;
  padding: 10px;
  cursor: pointer;
}
</style>