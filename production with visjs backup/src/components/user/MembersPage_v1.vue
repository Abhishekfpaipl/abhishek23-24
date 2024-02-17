<template>
    <TopNav>Members</TopNav>
    <div class="">
        <div class="px-3 mt-3">
            <div class="box w-100  p-2 d-block d-md-flex justify-content-center "
                style="box-shadow: rgba(67, 71, 85, 0.27) 0px 0px 0.25em, rgba(90, 125, 188, 0.05) 0px 0.25em 1em">
                <TextInputs class="w-100 " name="Search By Name" type="text" design="floating" />
                <div class="form-floating w-100 ">
                    <select class="form-select" id="floatingSelect" aria-label="Floating label select example">
                        <option selected>Choose User Role</option>
                        <option value="1">User</option>
                        <option value="2">Admin</option>
                        <option value="3">Creator</option>
                        <option value="4">Manager</option>
                        <option value="5">Assignee</option>
                    </select>
                    <label for="floatingSelect">Works with selects</label>
                </div>
                <div class="form-floating w-100 ">
                    <select class="form-select" id="floatingSelect" aria-label="Floating label select example">
                        <option selected>Sort Order By</option>
                        <option value="1">Name (A to Z)</option>
                        <option value="2">Two</option>
                        <option value="3">Three</option>
                    </select>
                    <label for="floatingSelect">Works with selects</label>
                </div>
                <div class="btnsar d-flex justify-content-center align-items-center mx-2">
                    <button class="btn btn-primary w-100 m-1">Active Users</button>
                    <button class="btn btn-light w-100 m-1">Rest Feilds</button>
                </div>
            </div>
            <router-link to="/create-member">
                <button class="btn btn-info w-100 mt-2">Create New User</button>
            </router-link>
        </div>
        <div class="d-flex flex-column mt-2" style="padding-bottom: 80px;">
            <div v-for="(user, index) in users" :key="index" class="mx-3 m-2 bg-white  border"
                style="box-shadow: rgba(67, 71, 85, 0.27) 0px 0px 0.25em, rgba(90, 125, 188, 0.05) 0px 0.25em 1em">
                <div class=" d-flex p-2">
                    <div class="left me-2">
                        <img style="width: 100px; height: 100px;object-fit: fill;" :src="`${publicPath}${user.imgu}`"
                            alt="">
                    </div>
                    <div class="right">
                        <p class="m-0">Name : {{ user.name }}</p>
                        <p class="m-0">Post : {{ user.post }}</p>
                        <p class="m-0">Dept : {{ user.dept }}</p>
                        <p class="m-0">Status : {{ user.status }}</p>

                    </div>
                </div>
                <div class="bottom d-flex">
                    <div class="btn-3 d-flex w-100">
                        <button class="btn btn-light w-100 border rounded-0" style="padding: 5px !important;"><i
                                class="bi bi-telephone fs-6"></i> Call</button>
                        <button class="btn btn-light w-100 border-start-0 border-end-0 border rounded-0 "
                            style="padding: 5px !important;"><i class="bi bi-whatsapp fs-6"></i> Text</button>
                        <RouterLink class="w-100  d-flex justify-content-center" style="text-decoration: none;"
                            to="/create-member">
                            <button class="btn btn-light w-100 border rounded-0 " style="padding: 5px !important;"><i
                                    class="bi bi-pencil-square fs-6"></i> Edit</button>
                        </RouterLink>
                    </div>
                </div>
            </div>
        </div>

    </div>
</template>

<script>
// import TextInputs from '@/components/textinputs/TextInputs.vue';
import TopNav from '@/components/navbar/TopNav.vue';
export default {
    data() {
        return {
            publicPath: process.env.BASE_URL
        }
    },
    components: {
        // TextInputs,
        TopNav
    },
    computed: {
        users() {
            return this.$store.getters.getUsers;
        }
    },

}
</script>

<style  scoped>
@media only screen and (max-width: 600px) {
    .btnsar {
        margin-top: 10px;
    }

    .form-floating {
        margin-top: 10px;
    }
}
</style>