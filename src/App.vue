<template>
  <AddEmp @refresh="fetchEmployees"/>
  <ViewEmp :list="employees"/>
  <UpdelEmp :list="employees" @refresh="fetchEmployees"/>
</template>

<script>
import axios from "axios"
import AddEmp from './components/AddEmployees.vue'
import ViewEmp from './components/EmployeesList.vue'
import UpdelEmp from './components/UpdateEmployees.vue'

export default {
  components: { AddEmp, ViewEmp, UpdelEmp },

  data() {
    return {
      employees: []
    }
  },

  methods: {
    async fetchEmployees() {
      const res = await axios.get("https://69e8965055d62f34797967c8.mockapi.io/api/emp")
      this.employees = res.data
    }
  },

  mounted() {
    this.fetchEmployees()
  }
}
</script>