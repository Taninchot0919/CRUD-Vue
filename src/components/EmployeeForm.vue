<template>
  <div id="employee-form">
    <form @submit.prevent="handleSubmit">
      <label>Employee name</label>
      <input
        ref="first"
        type="text"
        :class="{ 'has-error': submitting && invalidName }"
        v-model="employee.name"
        @focus="clearStauts"
        @keypress="clearStatus"
      />
      <br />
      <label>Employee email</label>
      <input
        type="text"
        :class="{ 'has-error': submitting && invalidEmail }"
        v-model="employee.email"
        @focus="clearStatus"
      />
      <br />
      <p v-if="error && submitting" class="error-message">
        Please fill out all required field
      </p>
      <p v-if="success" class="success-message">Add Employee Successfully</p>
      <button>Add Employee</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "employee-form",
  data() {
    return {
      submitting: false,
      error: false,
      success: false,
      employee: {
        name: "",
        email: "",
      },
    };
  },
  methods: {
    handleSubmit() {
      // console.log(this.employee);
      this.submitting = true;
      this.clearStatus();
      if (this.invalidName || this.invalidEmail) {
        this.error = true;
        return;
      }

      this.$emit("add:employee", this.employee);
      this.$refs.first.focus(); 

      this.employee = {
        name: "",
        email: "",
      };

      // this.error = false,
      // this.success = true
      // this.submitting = false แปลงรูปมาเป็นแบบด้านล่าง
      (this.error = false), (this.success = true), (this.submitting = false);
    },
    clearStatus() {
      this.success = false;
      this.error = false;
    },
  },
  computed: {
    invalidName() {
      return this.employee.name === "";
    },
    invalidEmail() {
      return this.employee.email === "";
    },
  },
};
</script>

<style scoped>
form {
  margin-bottom: 2rem;
}
input {
  margin-left: 0.5rem;
  margin-bottom: 2rem;
}
[class*="-message"] {
  font-weight: bold;
}
.error-message {
  color: red;
}
.success-message {
  color: green;
}
</style>