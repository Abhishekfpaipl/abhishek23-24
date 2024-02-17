<template>
    <div class="d-flex justify-content-evenly align-items-center bg-light w-100"
        style="position:fixed;bottom: 0;height:65px;box-shadow: rgba(14, 30, 37, 0.12) 0px 2px 4px 0px, rgba(14, 30, 37, 0.32) 0px 2px 16px 0px;">

        <router-link to="/order/new" :class="{ 'text-danger': currentRoute === 'Order-New' }" class="text-decoration-none">
            <div class="d-flex flex-column align-items-center">
                <i class="bi bi-bookmark-plus fs-3"></i>
                <p class="m-0" style="font-size:12px ;">Orders</p>
            </div>
        </router-link>


        <router-link to="/store/inward" :class="{ 'text-danger': currentRoute === 'Store-Inward' }"
            class="text-decoration-none ">

            <div class="d-flex flex-column align-items-center">
                <i class="bi bi-layers fs-3"></i>
                <p class="m-0" style="font-size:12px ;">Store</p>
            </div>
        </router-link>

        <router-link to="/cutting/order" :class="{ 'text-danger': currentRoute === 'Cutting-Order' }"
            class="text-decoration-none ">
            <div class="d-flex flex-column align-items-center">
                <i class="bi bi-scissors fs-3"></i>
                <p class="m-0" style="font-size:12px ;">Cutting</p>
            </div>
        </router-link>

        <router-link to="/production/order" :class="{ 'text-danger': currentRoute === 'Production-Order' }"
            class="text-decoration-none ">
            <div class="d-flex flex-column align-items-center">
                <i class="bi bi-gear fs-3"></i>
                <p class="m-0" style="font-size:12px ;">Production</p>
            </div>
        </router-link>

        <router-link to="/finishing/order" :class="{ 'text-danger': currentRoute === 'Finishing-Order' }"
            class="text-decoration-none ">
            <div class="d-flex flex-column align-items-center">
                <i class="bi bi-bookmark-star fs-3"></i>
                <p class="m-0" style="font-size:12px ;">Finishing</p>
            </div>
        </router-link>

    </div>
</template>

<script>
export default {
    name: 'BottomNav',
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

<style lang="scss" scoped></style>