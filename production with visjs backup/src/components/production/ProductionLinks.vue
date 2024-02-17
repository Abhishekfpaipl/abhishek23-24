<template>
    <TopNav> Production</TopNav>
    <div class="nav nav-tabs py-2 d-flex overflow-x-scroll flex-nowrap ws-nowarp align-items-center"
        style="font-size: 10px; height: 63px; font-weight: 500;" id="nav-tab" role="tablist">

        <RouterLink class="nav-link ws-nowarp" :to="{ name: 'Production-Order' }"
            :class="currentRouteName('Production-Order') ? 'active' : ''">Order
        </RouterLink>
        <router-link class="nav-link ws-nowarp" :to="{ name: 'Production-Inhand' }"
            :class="currentRouteName('Production-Inhand') ? 'active' : ''">Allotment</router-link>
        <router-link class="nav-link ws-nowarp" :to="{ name: 'Production-Inproduction' }"
            :class="currentRouteName('Production-Inproduction') ? 'active' : ''">In-Production</router-link>

        <router-link class="nav-link ws-nowarp " :to="{ name: 'production-production' }"
            :class="currentRouteName('production-production') ? 'active' : ''">Worker </router-link>

        <router-link class="nav-link ws-nowarp " :to="{ name: 'production-catalog' }"
            :class="currentRouteName('production-catalog') ? 'active' : ''">Catalog </router-link>
        </div>
         
</template>

<script>
import TopNav from '../navbar/TopNav.vue';
 

export default {
    name: "ProductionLinks",
    components: { TopNav,  },
    data() {
        return {
            // links:[
            //     {route:''}
            // ]
        };
    },
    props: ["active"],
    computed: {
        // currentRouteName() {
        //     return this.$route.name;
        // }
    },
    methods: {
        currentRouteName(routeName) {
            return this.$route.name.includes(routeName);
        }
    },
    
}
</script>
<style>
.nav-link {
    color: grey
}

.ws-nowarp {
    white-space: nowrap;
}
</style>