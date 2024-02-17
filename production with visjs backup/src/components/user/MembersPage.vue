<template>
    <div>
        <TopNav>Members</TopNav>
        <div>
            <FilterPage></FilterPage>

            <div class="d-flex flex-column mt-2" style="padding-bottom:100px; height: 100vh; overflow-y: scroll;">
                <div v-for="(user, index) in users" :key="index" class="mx-3 m-2 bg-white  border">
                    <RouterLink to="/create-member" style="text-decoration: none">
                        <p class="m-0 fs-5 fw-semibold  ms-3 text-dark">#{{ user.id }}12 | {{ user.name }}</p>
                        <div class="d-flex d-flex p-2 text-dark">
                            <div class="left me-2">
                                <img class="rounded" style="width: 80px; height: 80px;object-fit: fill;"
                                    :src="`${publicPath}${user.imgu}`" alt="">
                            </div>
                            <div class="right ms-2">
                                <!-- <p class="m-0">ID : {{ user.id }}</p> -->
                                <!-- <p class="m-0">Name : {{ user.name }}</p> -->
                                <p class="m-0">Rate : ₹{{ user.rate }}</p>
                                <p class="m-0">Post : {{ user.post }}</p>
                                <p class="m-0">Dept : {{ user.dept }}</p>

                            </div>
                        </div>
                    </RouterLink>
                    <!-- <div class="d-flex">
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
                    </div> -->
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import TopNav from '../navbar/TopNav.vue';
import FilterPage from '../Filter/FilterPage.vue';

export default {
    components: {
        TopNav,
        FilterPage
    },
    data() {
        return {
            publicPath: process.env.BASE_URL
        }
    },
    computed: {
        users() {
            return this.$store.getters.getUsers;
        }
    }
}
</script>