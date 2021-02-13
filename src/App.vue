// เรียนถึง 19:00

<template>
  <div id="app">
    <h1>Employee</h1>
    <employee-form @add:employee="addEmployee" />
    <!-- : หมายถึงอนุญาตให้เราส่งข้อมูลผ่านทางนี้ได้ -->
    <employee-table
      v-bind:employees="employees"
      @delete:employee="deleteEmployee"
    />
  </div>
</template>

<script>
import EmployeeTable from "@/components/EmployeeTable";
import EmployeeForm from "@/components/EmployeeForm";
export default {
  name: "App",
  components: {
    EmployeeForm,
    EmployeeTable,
  },
  data() {
    return {
      employees: [
        {
          id: "1",
          name: "Taninchot Phuwaloetthiwat",
          email: "Taninchot0919@live.com",
        },
      ],
    };
  },
  methods: {
    addEmployee(employee) {
      const lastId =
        this.employees.length > 0
          ? this.employees[this.employees.length - 1].id
          : 0;
      const id = lastId + 1;
      const newEmployee = { ...employee, id };
      this.employees = [...this.employees, newEmployee];
      console.log(this.employees);
    },
    // ลบ Employee โดยเอาเฉพาะ employee ที่นอกเหนือจาก id ที่รับเข้ามา (ลบ id เฉพาะ Employee id นั้นๆ)
    deleteEmployee(id) {
      this.employees = this.employees.filter((employee) => employee.id !== id);
    },
  },
};
</script>

<style>
#app {
}
</style>
