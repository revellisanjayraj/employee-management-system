<template>   
  <form @submit.prevent="postData">
    <div class="container mt-5">
      <h2 class="text-center mb-4">Employee Management System</h2>

      <div class="row g-3">

        <div class="col-md-2">
          <input type="number" class="form-control" placeholder="Emp ID" v-model="emp.eid">
        </div>

        <div class="col-md-3">
          <input type="text" class="form-control" placeholder="Name" v-model="emp.name">
        </div>

        <div class="col-md-3">
          <input type="text" class="form-control" placeholder="Designation" v-model="emp.desig">
        </div>

        <div class="col-md-2">
          <select class="form-select" v-model="emp.dept">
            <option disabled value="">Department</option>
            <option>HR</option>
            <option>IT</option>
            <option>Sales</option>
          </select>
        </div>

        <div class="col-md-1">
          <input type="number" class="form-control" placeholder="Salary" v-model="emp.sal">
        </div>

        <div class="col-md-1 d-flex align-items-end">
          <button type="submit" class="btn btn-success w-100">ADD</button>
        </div>

      </div>
    </div>
  </form>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      emp:{
        eid: 0,
        name: "",
        desig: "",
        dept: "",
        sal: 0
      }
    }
  },

  methods: {
    async postData() {
      await axios.post("https://69e8965055d62f34797967c8.mockapi.io/api/emp", this.emp)

      this.$emit("refresh")   // 🔥 update list

      // clear form
      this.emp = {
        eid: 0,
        name: "",
        desig: "",
        dept: "",
        sal: 0
      }
    }
  }
}
</script>