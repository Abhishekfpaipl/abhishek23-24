<template>
    
    <div class="d-flex justify-content-evenly align-items-center bg-light w-100"
        style="position:fixed;bottom: 0;height:65px;box-shadow: rgba(14, 30, 37, 0.12) 0px 2px 4px 0px, rgba(14, 30, 37, 0.32) 0px 2px 16px 0px;">

        <router-link to="/production-manager/order" :class="{ 'text-danger': currentRoute === 'order' }" class="text-decoration-none">
            <div class="d-flex flex-column align-items-center">
                <i class="bi bi-shop-window fs-3"></i>
                <p class="m-0" style="font-size:12px ;">Order</p>
            </div>
        </router-link>


        <router-link to="/production/inhand" :class="{ 'text-danger': currentRoute === 'production' }"
            class="text-decoration-none "> 
            <div class="d-flex flex-column align-items-center">
                <i class="bi bi-building fs-3"></i>
                <p class="m-0" style="font-size:12px ;">Members</p>
            </div>
        </router-link>

        <router-link to="/production/inproduction" :class="{ 'text-danger': currentRoute === '' }"
            class="text-decoration-none ">
            <div class="d-flex flex-column align-items-center">
                <i class="bi bi-scissors fs-3"></i>
                <p class="m-0" style="font-size:12px ;">Workers</p>
            </div>
        </router-link>

        <!-- <router-link to="" :class="{ 'text-danger': currentRoute === '' }"
            class="text-decoration-none ">
            <div class="d-flex flex-column align-items-center">
                <i class="bi bi-person fs-3"></i>
                <p class="m-0" style="font-size:12px ;">User</p>
            </div>
        </router-link>

        <router-link to="/finishing/order" :class="{ 'text-danger': currentRoute === 'Finishing-Order' }"
            class="text-decoration-none ">
            <div class="d-flex flex-column align-items-center">
                <i class="bi bi-gear fs-3"></i>
                <p class="m-0" style="font-size:12px ;">Setting</p>
            </div>
        </router-link> -->

    </div>
</template>

<script>
export default {
    name: 'ProductionBottomnav',
    computed: {
        currentRoute() {
            return this.$route.name;
        }
    },
    // methods: {
    //     currentRouteName(routeName) {
    //         return this.$route.name.includes(routeName);
    //     }

    // }
}
</script>