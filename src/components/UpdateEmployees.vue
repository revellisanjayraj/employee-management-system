<template>
  <div class="container mt-5">
    <h2 class="text-center mb-4">Employee Management</h2>


    <table class="table table-bordered table-striped text-center">
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
        <tr v-for="emp in employees" :key="emp.id">
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
            <h5 class="modal-title">Update Employee</h5>
            <button class="btn-close" @click="closeForm"></button>
          </div>

          <div class="modal-body" v-if="editEmp.eid">
            <input type="text" class="form-control mb-2" v-model="editEmp.name" placeholder="Name">
            <input type="text" class="form-control mb-2" v-model="editEmp.desig" placeholder="Designation">
        <select class="form-select" v-model="editEmp.dept">
          <option disabled value="">Department</option>
          <option>HR</option>
          <option>IT</option>
          <option>Sales</option>
          <option>Marketing</option>
          <option>Finance</option>
          <option>Administration</option>
        </select>
            <input type="number" class="form-control mb-2" v-model="editEmp.sal" placeholder="Salary">
          </div>

          <div class="modal-footer">
            <button class="btn btn-success" @click="updateEmployee">Save</button>
            <button class="btn btn-secondary" @click="closeForm">Cancel</button>
          </div>

        </div>
      </div>
    </div>

    
    <div class="modal-backdrop fade show" v-if="showForm"></div>

   
    <div v-if="message" class="alert alert-success mt-3 text-center">
      {{ message }}
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "UpdateEmployee",

  data() {
    return {
      employees: [],
      showForm: false,
      message: "",
      editEmp: {
        eid: "",
        name: "",
        desig: "",
        dept: "",
        sal: ""
      }
    };
  },

  mounted() {
    this.fetchEmployees();
  },

  methods: {
    fetchEmployees() {
      axios
        .get("https://69e8965055d62f34797967c8.mockapi.io/api/emp")
        .then((res) => {
          this.employees = res.data;
        })
        .catch((err) => console.error(err));
    },

    openEdit(emp) {
      // copy values → avoids instant update issue
      this.editEmp = { ...emp };
      this.showForm = true;
    },

    closeForm() {
      this.showForm = false;
    },

    updateEmployee() {
      axios
        .put(
          `https://69e8965055d62f34797967c8.mockapi.io/api/emp/${this.editEmp.id}`,
          this.editEmp
        )
        .then(() => {
          this.message = "Employee Updated Successfully!";
          this.showForm = false;
          this.fetchEmployees(); // refresh table
        })
        .catch((err) => console.error(err));
    },
    deleteEmployee(id) {
  if (confirm("Are you sure you want to delete this employee?")) {
    axios.delete(`https://69e8965055d62f34797967c8.mockapi.io/api/emp/${id}`)
      .then(() => {
        this.message = "Employee Deleted Successfully!";
        this.fetchEmployees(); // refresh table
      })
      .catch(err => console.error(err));
  }
}
  }
};
</script>