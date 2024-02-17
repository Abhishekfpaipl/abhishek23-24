<template>
    <div class="container mt-4">
        <div class="d-flex justify-content-between">
            <i class="bi bi-chevron-left fs-3" @click="goback()"></i>
            <h1>Login</h1>
        </div>
        <form @submit.prevent="submitForm">
            <div class="form-group">
                <label for="email">Email</label>
                <input type="email" class="form-control" id="email" v-model="formData.email" required>
            </div>
            <div class="form-group">
                <label for="password">Password</label>
                <input type="password" class="form-control" id="password" v-model="formData.password" required>
            </div>
            <div class="mt-3 d-flex justify-content-center">
                <button type="submit" class="btn btn-primary">Log In</button>
            </div>
        </form>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            formData: {
                email: '',
                password: ''
            }
        };
    },
    methods: {
        submitForm() { 
            console.log('Form submitted:', this.formData);
        },
        goback() {
            window.history.back();
        }
    }
};
</script>
  
<style>
/* Optional styling */
.container {
    max-width: 400px;
}
</style>
  