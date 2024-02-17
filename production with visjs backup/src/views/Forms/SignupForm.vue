<template>
    <div class="p-2 d-flex justify-content-between border-bottom">
        <i class="bi bi-chevron-left fs-3" @click="goback()"></i>
        <h2>Sign Up</h2>
    </div>
    <div class="container mt-4">
        <form @submit.prevent="submitForm">
            <div class="form-group">
                <label for="name">Name</label>
                <input type="text" class="form-control" id="name" v-model="formData.name" required>
            </div>
            <div class="form-group">
                <label for="email">Email</label>
                <input type="email" class="form-control" id="email" v-model="formData.email" required>
            </div>
            <div class="form-group">
                <label for="password">Password</label>
                <input type="password" class="form-control" id="password" v-model="formData.password" required>
            </div>
            <div class="d-flex mt-3 justify-content-center">
                <button type="submit" class="btn btn-primary">Sign Up</button>
            </div>
        </form>
    </div>
</template>
  
<script>
export default {
    data() {
        return {
            formData: {
                name: '',
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
  