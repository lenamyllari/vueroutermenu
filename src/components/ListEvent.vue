<template>

  <div >
      <table id="task-table" class="table table-striped">
        <thead>
        <tr>
          <th>Course</th>
          <th>Task</th>
          <th>Deadline</th>
          <th>Done</th>
        </tr>
        </thead>
        <tbody>

        <tr v-for="note in notes" :key="note.id">
          <td>{{ note.course }}</td>
          <td>{{ note.task }}</td>
          <td>{{ note.date }}</td>
          <td v-if="note.done===true">yes</td>
          <td v-if="note.done===false">no</td>
        </tr>
        </tbody>
      </table>

  </div>
</template>
<script>
  import axios from 'axios';

export default {
  name: 'ListEvent',

  data() {
    return {
      notes: [],
      note: {
        id: '',
        course: '',
        task:'',
        date: '',
        done: ''
      }
    }
  },
  async created() {
    try {
      const res = await axios.get(`http://localhost:3000/notes`)

      this.notes = res.data;
    } catch(e) {
      console.error(e)
    }
  },
};
</script>
<style scoped>
.homeText{
  font-size: 35px;
  color: red;
  text-align: center;
  position: relative;
  top:30px;
  text-shadow: 2px 2px 2px gray;
}
</style>
