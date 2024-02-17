<template>
    <div>
        <div class="d-flex justify-content-between align-items-center container position-sticky top-0 bg-light py-2"
            style="z-index: 12; height:63px;">
            <div class="">
                <i class="bi bi-arrow-left fs-4" @click="goBack()"></i>
                <span class="fs-4 ms-2" style="font-size: 16px; font-weight: 500;">View Member</span>
            </div>
        </div>
        
            <ImageUploadBox></ImageUploadBox>
         
    </div>
    <div class="w-100 px-2">
        <div class=" ">
            <form @submit="update" method="post">
                <TextInputs name="Full Name" type="text" design="floating"  />
                <TextInputs name="Mobile" type="number" design="floating"   />
                <TextInputs name="Email Id" type="email" design="floating"   />
                <TextInputs name="Password" type="password" design="floating"   />
                <TextInputs name="Change Password" type="password" design="floating" />
                <div class="buttons d-flex mt-2 mb-4">
                    <div type="Reset" class="btn btn-primary w-100 border mx-2">Reset Fields</div>
                    <input   name="Get Data" type="submit" class="btn btn-primary w-100 border mx-2"
                        value="Update Details" />
                </div>
            </form>
        </div>
    </div>
</template>

<script>
import ImageUploadBox from '../avatar/ImageUploadBox.vue';
import TextInputs from '../textinputs/TextInputs.vue';
export default {
    methods: {
        goBack() {
            window.history.back();
        }
    },
    components: { TextInputs, ImageUploadBox }
}
</script>

<style lang="scss" scoped></style>