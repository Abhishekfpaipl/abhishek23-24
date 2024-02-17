<template>
    <div style="height: 100vh" class="bg-light">
    <div class="d-flex justify-content-between align-items-center container position-sticky top-0  py-2 border-bottom"
        style="z-index: 12; height:63px;">
        <div class="">
            <i class="bi bi-arrow-left fs-4" @click="goBack()"></i>
            <span class="fs-4 ms-2" style="font-size: 16px; font-weight: 500;">Create New Member</span>
        </div>
        <div class="">

        </div>
    </div>
    <ImageUploadBox></ImageUploadBox>
    <div class="container my-3" style="padding-bottom: 100px;">
        <!-- <p class="fs-4 ">Create New Member</p> -->
        <form @submit="update" method="post">
            <TextInputs name="Full Name" type="text" design="floating" v-model="form.Name" />
            <TextInputs name="Post" type="text" design="floating" v-model="form.Post" />
            <TextInputs name="Department" type="text" design="floating" v-model="form.Department" />
            <TextInputs name="Rate" type="text" design="floating" v-model="form.Rate" />
              
            <div class="d-flex my-3 p-2">
                <input type="checkbox">
                <p class="m-0 ms-2">Stay on page after creating new</p>
            </div>
            <div class="buttons d-flex mt-2">
                <div type="Reset" class="btn btn-light w-100 border mx-2">Reset Fields</div>
                <input @click="getData()" name="Get Data" type="submit" class="btn btn-light w-100 border mx-2"
                    value="Update Details" />
            </div>
        </form>
    </div>
    </div>
</template>

<script>
import TextInputs from '../textinputs/TextInputs.vue';
import ImageUploadBox from '../avatar/ImageUploadBox.vue';
export default {
    components: { TextInputs, ImageUploadBox },
    data() {
        return {
            form: {
                Name: "",
                Post: "",
                Department: "",
                Rate: "",
            },
        };
    },
    methods: {
        getData() {
            console.warn("values :  ", this.form.Name, this.form.Post, this.form.Department, this.form.Rate, this.form.ConfirmPassword);
        },
        goBack() {
            window.history.back()
        }

    }
}
</script>

<style lang="scss" scoped></style>