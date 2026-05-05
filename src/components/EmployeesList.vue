<template>
<div class="container mt-4">
  <table class="table table-striped table-bordered table-hover">

    <thead class="table-dark">
      <tr>
        <th>Emp ID</th>
        <th>Name</th>
        <th>Designation</th>
        <th>Department</th>
        <th>Salary</th>
      </tr>
    </thead>

    <tbody>
      <tr v-for="item in list" :key="item.id">
        <td>{{ item.eid }}</td>
        <td>{{ item.name }}</td>
        <td>{{ item.desig }}</td>
        <td>{{ item.dept }}</td>
        <td>{{ item.sal }}</td>
      </tr>
    </tbody>

  </table>
</div>
</template>
<script>
import axios from 'axios';
export default {
    name: "Employees",
    data() {
        return {
            list:[]
        }
    },
    mounted() {
        axios.get("https://69e8965055d62f34797967c8.mockapi.io/api/emp")
            .then((res) => {
                this.list = res.data;
            })
        .catch(err => console.log(err));
    }
}
</script>