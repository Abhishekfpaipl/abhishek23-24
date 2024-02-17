<template>
    <div style="position: relative; cursor: pointer; ">
        <input type="file" accept="image/*" class="d-none" ref="file" @change="change" >
        <img  @click="browse()" :src="src" alt="Profile Image" width="100" 
            class=" rounded d-flex justify-content-center align-items-center border border-2 border-dark m-2"
            style=" text-align: center;width: 300px; height: 300px;">
        <!-- <button class="round rounded-circle bg-primary border" style="position: absolute; right: 0px; bottom:0 ;"
            @click="browse()"><i class="bi bi-camera2"></i></button> -->
    </div>
</template>

<script>
export default {

    props: {
        value: File
    },
    data() {
        return {
            src: null
        }
    },

    methods: {

        browse() {
            this.$refs.file.click();
        },

        change(e) {
            this.$emit('input', e.target.files[0]);
            let reader = new FileReader();
            reader.readAsDataURL(e.target.files[0]);
            console.log('IMAGE UPLOADED')
            reader.onload = (e) => {
                this.src = e.target.result;
            }
        }
    }
}
</script>

<style scoped></style>