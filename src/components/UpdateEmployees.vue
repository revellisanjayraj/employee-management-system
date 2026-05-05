<template>
  <div class="container mt-5">

    <table class="table table-bordered text-center">
      <thead class="table-dark">
        <tr>
          <th>ID</th>
          <th>Name</th>
          <th>Designation</th>
          <th>Department</th>
          <th>Salary</th>
          <th>Action</th> 
        </tr>
      </thead>

      <tbody>
        <tr v-for="emp in list" :key="emp.id">
          <td>{{ emp.eid }}</td>
          <td>{{ emp.name }}</td>
          <td>{{ emp.desig }}</td>
          <td>{{ emp.dept }}</td>
          <td>{{ emp.sal }}</td>
          <td>
            <button class="btn btn-primary btn-sm me-2" @click="openEdit(emp)">
              Update
            </button>
            <button class="btn btn-danger btn-sm" @click="deleteEmployee(emp.id)">
              Delete
            </button>
          </td>
        </tr>
      </tbody>
    </table>

    <!-- Modal -->
    <div class="modal fade show d-block" v-if="showForm">
      <div class="modal-dialog">
        <div class="modal-content">

          <div class="modal-header">
            <h5>Edit Employee</h5>
            <button class="btn-close" @click="closeForm"></button>
          </div>

          <div class="modal-body">
            <input class="form-control mb-2" v-model="editEmp.name">
            <input class="form-control mb-2" v-model="editEmp.desig">
            <input class="form-control mb-2" v-model="editEmp.dept">
            <input class="form-control mb-2" v-model="editEmp.sal">
          </div>

          <div class="modal-footer">
            <button class="btn btn-success" @click="updateEmployee">Save</button>
            <button class="btn btn-secondary" @click="closeForm">Cancel</button>
          </div>

        </div>
      </div>
    </div>

  </div>
</template>

<script>
import axios from "axios"

export default {
  props: ["list"],

  data() {
    return {
      showForm: false,
      editEmp: {}
    }
  },

  methods: {
    openEdit(emp) {
      this.editEmp = { ...emp }
      this.showForm = true
    },

    closeForm() {
      this.showForm = false
    },

    async updateEmployee() {
      await axios.put(
        `https://69e8965055d62f34797967c8.mockapi.io/api/emp/${this.editEmp.id}`,
        this.editEmp
      )

      this.showForm = false
      this.$emit("refresh")   // 🔥 update list
    },

    async deleteEmployee(id) {
      await axios.delete(`https://69e8965055d62f34797967c8.mockapi.io/api/emp/${id}`)

      this.$emit("refresh")   // 🔥 update list
    }
  }
}
</script>