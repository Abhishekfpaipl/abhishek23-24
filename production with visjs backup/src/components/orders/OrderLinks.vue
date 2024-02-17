<template>

    <!-- <div class="container d-flex justify-content-between align-items-center bg-light"
        style="height: 63px !important;box-shadow: rgba(67, 71, 85, 0.27) 0px 0px 0.25em, rgba(90, 125, 188, 0.05) 0px 0.25em 1em;">
        <div class="" data-bs-toggle="offcanvas" data-bs-target="#offcanvasExampleMenu"
            aria-controls="offcanvasExampleMenu">
            <i class="bi bi-list fs-1"></i>
        </div>
        <div class="">
            <h3>Orders</h3>
        </div>

   
        <div class="offcanvas offcanvas-start" tabindex="-1" id="offcanvasExampleMenu"
            aria-labelledby="offcanvasExampleLabel" style="width:80vw !important">
            <div class="offcanvas-header">
                <h5 class="offcanvas-title" id="offcanvasExampleLabel">Menu</h5>
                <button type="button" class="btn-close" data-bs-dismiss="offcanvas" aria-label="Close"></button>
            </div>
            <div class="offcanvas-body p-0">
                <div>
                    <ul class="list-group rounded-0">
                        <router-link to="/SignupForm" class="text-decoration-none text-dark">
                            <li class="list-group-item">Login / SignUp</li>
                        </router-link>
                        <router-link to="/supplier-signup" class="text-decoration-none text-dark">
                            <li class="list-group-item">Profile / Account</li>
                        </router-link>
                    </ul>
                </div>
            </div>
        </div>

    </div> -->
    <TopNav></TopNav>
    <div class="nav nav-tabs align-items-center py-2 d-flex justify-content-around px-2"
        style="font-size: 10px; height: 63px; font-weight: 500;box-shadow: rgba(67, 71, 85, 0.27) 0px 0px 0.25em, rgba(90, 125, 188, 0.05) 0px 0.25em 1em;"
        id="nav-tab" role="tablist">
        <router-link class="nav-link" :to="{ name: 'Order-New' }"
            :class="currentRouteName === 'Order-New' ? 'active' : ''">New</router-link>

        <router-link class="nav-link " :to="{ name: 'Order-Ready' }"
            :class="currentRouteName === 'Order-Ready' ? 'active' : ''">Ready</router-link>

        <router-link class="nav-link " :to="{ name: 'Order-Order' }"
            :class="currentRouteName === 'Order-Order' ? 'active' : ''">Order</router-link>

        <router-link class="nav-link " :to="{ name: 'Order-Shipped' }"
            :class="currentRouteName === 'Order-Shipped' ? 'active' : ''">Shipped</router-link>

        <router-link class="nav-link " :to="{ name: 'Order-Delivered' }"
            :class="currentRouteName === 'Order-Delivered' ? 'active' : ''">Delivered</router-link>

    </div>
</template>                                                 

<script>
import TopNav from '../navbar/TopNav.vue';
export default {
    name: "OrderLinks",
    props: ["active"],
    computed: {
        currentRouteName() {
            return this.$route.name;
        }
    },
    components: { TopNav }
}
</script>
<style>
.nav-link {
    color: grey
}
</style>