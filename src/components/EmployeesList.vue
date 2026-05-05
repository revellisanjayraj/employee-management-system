<template>
<div class="container mt-4">
  <table class="table table-striped table-bordered">
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
export default {
  props: ["list"]   // 👈 from parent
}
</script>