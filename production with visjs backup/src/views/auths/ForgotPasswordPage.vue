<template>
    <div class="container" style="padding-top: 20px;">

        <div class="d-flex justify-content-center">
            <img :src="`${publicPath}${logo}`" width="150">
        </div>
        <div class="d-flex justify-content-center">
            <p class="mt-2 m-0 fw-bold icon">FABRICATION</p>
        </div>
        <div class="text text-center mt-4">
            <p class="fs-5">Forgot Password </p>

        </div>
        <div class="mt-3">
            <div class="w-100 p-2 form-floating container">
                <input type="text" class="form-control" id="floatingInput" placeholder="Email" v-model="email" required>
                <label for="floatingInput" class="text-muted">Enter your Email</label>
            </div>
        </div>

        <div class="p-2">
            <button class="btn btn-light  text-dark py-2 w-100 fs-5" data-bs-toggle="modal" data-bs-target="#exampleModal"
                style="padding: 10px 12px !important;box-shadow: rgba(67, 71, 85, 0.27) 0px 0px 0.25em, rgba(90, 125, 188, 0.05) 0px 0.25em 1em;">Submit</button>
        </div>
        <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
            <div class="modal-dialog modal-dialog-centered">
                <div class="modal-content">
                    <div class="modal-header">
                        <h1 class="modal-title fs-5" id="exampleModalLabel">New Password Sent Successfully</h1>
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body text-center">
                        <p class="m-0 mb-4">A new password has been sent to your registered email address, Please find and
                            login
                            again.</p>
                        <router-link to="/login-page">
                            <button class="btn text-white w-100" data-bs-dismiss="modal"
                                style="background: rgb(38,130,193);
background: linear-gradient(113deg, rgba(38,130,193,1) 31%, rgba(36,81,159,1) 97%);padding:12px 24px !important;">Ok</button>
                        </router-link>
                    </div>
                </div>
            </div>
        </div>

        <div class="text-center mt-2 px-2">
            <span>If you submit your email here, Will send you a One Time Password at your registered email address</span>
        </div>

        <div class="mt-3">
            <div class="d-flex justify-content-center mt-4 p-2">
                <router-link to="/login-page" class="w-100 rounded"
                    style="box-shadow: rgba(67, 71, 85, 0.27) 0px 0px 0.25em, rgba(90, 125, 188, 0.05) 0px 0.25em 1em;">
                    <button class="btn text-white w-100 fs-5" style="background: rgb(38,130,193);
background: linear-gradient(113deg, rgba(38,130,193,1) 31%, rgba(36,81,159,1) 97%);padding: 14px 12px !important;">
                        Click here for Login
                    </button>
                </router-link>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    data() {
        return {
            logo: "img/images/logo1.png",
            publicPath: process.env.BASE_URL,
            email: '',
        };
    },

    methods: {
        login() {
            console.log('Email:', this.email);
        }
    }
}
</script>

<style lang="scss" scoped>
.icon {
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    font-size: 2rem;
    background: -webkit-linear-gradient(#273990, #24aae3);
    -webkit-text-fill-color: transparent;
     background-clip: text;
}
</style>
