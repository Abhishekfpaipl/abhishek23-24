<template>
    <div class="d-flex justify-content-between align-items-center container position-sticky top-0 bg-light py-2"
        style="z-index: 12;">
        <div class="">
            <i class="bi bi-arrow-left fs-4" @click="goBack()"></i>
            <span class="fs-4 ms-2" style="font-size: 16px; font-weight: 500;">Edit Member</span>
        </div>
        <!-- <div class="">
            <router-link to="/users/detail" class="text-decoration-none text-dark">
                <i class="bi bi-person-square fs-3 me-3"><span style="font-size: 15px;" class="ms-1">View</span></i>
            </router-link>
        </div> -->
    </div>

    <div class=" w-100 h-100 ">
        <div class="main container d-block w-100  d-md-flex ">
            <div class="left ">
                <ImageUploadBox></ImageUploadBox>
                
            </div>
            <div class="w-100 px-2">
                <div class=" ">
                    <form @submit="update" method="post">
                        <TextInputs name="Full Name" type="text" design="floating" v-model="form.Name" />
                        <TextInputs name="Post" type="text" design="floating" v-model="form.Post" />
                        <TextInputs name="Department" type="text" design="floating" v-model="form.Department" />
                        <TextInputs name="Rate" type="text" design="floating" v-model="form.Rate" />
                        <!-- <div class="mb-3 border rounded p-2">
                            <label for="formFile" class="form-label">Upload Profile Photo</label>
                            <input class="form-control" type="file" id="formFile">
                        </div> -->
                        <div class="buttons d-flex mt-2 mb-5">
                            <div type="Reset" class="btn btn-light w-100 border mx-2">Reset Fields</div>
                            <input @click="getData()" name="Get Data" type="submit" class="btn btn-light w-100 border mx-2"
                                value="Update Details" />
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import ImageUploadBox from '../avatar/ImageUploadBox.vue';
import TextInputs from '@/components/textinputs/TextInputs.vue';
export default {
    components: {
    TextInputs, 
    ImageUploadBox
},
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
