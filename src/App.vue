<template>
  <AddEmp/>
  <ViewEmp/>
  <UpdelEmp/>
</template>
<script>
import AddEmp from './components/AddEmployees.vue';
import ViewEmp from './components/EmployeesList.vue';
import UpdelEmp from './components/UpdateEmployees.vue';
export default {
  components: {
    AddEmp,
    ViewEmp,
    UpdelEmp
  }
}
</script>
<style>
</style>