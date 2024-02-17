<template>
    <div class="container" style="padding-top: 20px;">
        <div class="d-flex flex-column align-items-center text-center">
            <i class="bi bi-envelope-check-fill icon" style="font-size:100px; color: rgb(38,130,193)"></i>
            <h4>OTP has been sent to your email</h4>
            <p>We've sent an email to user@gmail.com to verify your email address, please update OTP in a email verification
                section and activate your account.
            </p>
            <RouterLink to="/registration-page" class="text-decoration-none" style="cursor: pointer;">Click here</RouterLink>
            <p> If you would like to change the email address you signed up with.</p>
            <div class="w-100 p-2 form-floating container">
                <input type="number" class="form-control" id="floatingInput" placeholder="Enter OTP">
                <label for="floatingInput">Enter Otp</label>
            </div>
        </div>
        <div class="d-flex justify-content-between container">
            <div class=""><p v-if="displayText">{{ displayText }}</p></div>
            <RouterLink to="" class="text-decoration-none" @click="showText">Resend OTP</RouterLink>
        </div>
        
        <div class="mt-4 p-2">
            <button data-bs-toggle="modal" data-bs-target="#exampleModal" class="btn w-100 text-white fs-5"
                style="box-shadow: rgba(67, 71, 85, 0.27) 0px 0px 0.25em, rgba(90, 125, 188, 0.05) 0px 0.25em 1em;
                    background: linear-gradient(113deg, #1FAB89  31%,  #28CC9E 97%);padding: 13px 12px !important;">
                Submit
            </button>
        </div>
        <!-- -------------Modal----------------- -->
        <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
            <div class="modal-dialog modal-dialog-centered">
                <div class="modal-content">
                    <div class="modal-header">
                        <h1 class="modal-title fs-5" id="exampleModalLabel">Congratulations</h1>
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body text-center">
                        <p class="m-0 mb-4">Your Email verification has been done successfully, Now you can use this app
                            uninterruptedly</p>
                        <router-link to="/login-page">
                            <button class="btn text-white w-100" data-bs-dismiss="modal"
                                style="background: linear-gradient(113deg, #1FAB89  31%,  #28CC9E 97%);padding:12px 24px !important;">Ok</button>
                        </router-link>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

export default {
data(){
    return{
        displayText:''
    }
},
methods:{
    showText() {
        this.displayText  = 'OTP Resent';
      }
}
}
</script>

<style  scoped>
.icon {
    background: -webkit-linear-gradient(113deg, #28CC9E 31%, #1FAB89 97%);
    -webkit-text-fill-color: transparent;
    background-clip: text;
}
</style>





  