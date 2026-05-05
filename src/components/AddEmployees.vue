<template>   
  <form @submit.prevent="postData">
  <div class="container mt-5">
    
    <h2 class="text-center mb-4">Employee Management System</h2>
    <p class="text-center mb-4">A Vue.js-based CRUD Application for Managing Employee Records</p>

    <div class="row g-3">

      <div class="col-md-2">
        <label>Emp ID</label>
        <input type="number" class="form-control" v-model="emp.eid">
      </div>

      <div class="col-md-3">
        <label>Name</label>
        <input type="text" class="form-control" v-model="emp.name">
      </div>

      <div class="col-md-3">
        <label>Designation</label>
        <input type="text" class="form-control" v-model="emp.desig">
      </div>

      <div class="col-md-2">
        <label>Department</label>
        <select class="form-select" v-model="emp.dept">
          <option disabled value="">Choose...</option>
          <option>HR</option>
          <option>IT</option>
          <option>Sales</option>
          <option>Marketing</option>
          <option>Finance</option>
          <option>Administration</option>
        </select>
      </div>

      <div class="col-md-1">
        <label>Salary</label>
        <input type="number" class="form-control" v-model="emp.sal">
      </div>

      <div class="col-md-1 d-flex align-items-end">
        <button type="submit" class="btn btn-success w-100">ADD</button>
      </div>

    </div>

  </div>
</form>
    </template>
<script>
import axios from 'axios';
export default {
    name: 'Employees',
    data() {
        return {
            emp:{
                eid: 0,
                name: null,
                desig: null,
                dept:"",
                sal:0
            }
        }
    },
    methods: {
        postData(e) {
            axios.post("https://69e8965055d62f34797967c8.mockapi.io/api/emp", {
                eid: this.emp.eid,
                name: this.emp.name,
                desig: this.emp.desig,
                dept: this.emp.dept,
                sal: this.emp.sal
            })
                .then(res => console.log(res.data))
                .catch(err => console.log(err));
             
        }
    }
}
</script>
<style>
</style>