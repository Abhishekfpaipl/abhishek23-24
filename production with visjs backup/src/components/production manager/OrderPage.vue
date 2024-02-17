<template>
    <TopNav>Production Manager</TopNav>
    <FilterPageV2></FilterPageV2>
    <div class="mt-2">
        <div v-for="(manager, index) in managers" :key="index"
            class="d-flex justify-content-between align-items-center border-bottom p-2">
            <div class="d-flex align-items-center">
                <img :src="`${publicPath}${manager.img}`" class="rounded-circle"
                    style="height:60px;width:60px; object-fit: fill;">
                <div class="ms-3">
                    <p class="m-0 fw-bold" style="font-size: 1.2rem;">#{{ manager.style }}</p>
                    <p class="m-0">Order Qty : {{ manager.costing }}</p>
                </div>
            </div>
            <div class="text-success rounded"  >
                <div v-if="accepted[index]">
                    <BtnChange :manager="manager"></BtnChange>
                </div>
                <div class="" v-else>
                    <button @click="acceptOrder(index)" class="btn btn-success" style="width: 6em;">Accept</button>
                </div>

            </div>
        </div>
    </div>
    <div class="mt-2">
        <div v-for="(manager, index) in managers" :key="index"
            class="d-flex justify-content-between align-items-center border-bottom p-2">
            <div class="d-flex align-items-center">
                <img :src="`${publicPath}${manager.img}`" class="rounded-circle"
                    style="height:60px;width:60px; object-fit: fill;">
                <div class="ms-3">
                    <p class="m-0 fw-bold" style="font-size: 1.2rem;">#{{ manager.style }}</p>
                    <p class="m-0">Order Qty : {{ manager.costing }}</p>
                </div>
            </div>
            <div class="text-success rounded">
                <button class="btn btn-warning" style="width: 6em;" >Manage</button>
            </div>
        </div>
    </div>
    <div class="mt-2">
        <div v-for="(manager, index) in managers" :key="index"
            class="d-flex justify-content-between align-items-center border-bottom p-2">
            <div class="d-flex align-items-center">
                <img :src="`${publicPath}${manager.img}`" class="rounded-circle"
                    style="height:60px;width:60px; object-fit: fill;">
                <div class="ms-3">
                    <p class="m-0 fw-bold" style="font-size: 1.2rem;">#{{ manager.style }}</p>
                    <p class="m-0">Order Qty : {{ manager.costing }}</p>
                </div>
            </div>
            <div class="text-success rounded">
                <button class="btn btn-primary" style="width: 6em;" >Finished</button>
            </div>
        </div>
    </div>
</template>

<script>
import TopNav from '@/components/navbar/TopNav.vue'
import BtnChange from '@/components/production manager/btn/BtnChange.vue'
import FilterPageV2 from '../Filter/FilterPageV2.vue';


export default {
    name: "InwardPage",
    components: { TopNav, BtnChange, FilterPageV2 },
    data() {
        return {
            publicPath: process.env.BASE_URL,
            accepted: []
        };
    },
    computed: {
        managers() {
            return this.$store.getters.getManagers;
        }
    },
    methods: {
        acceptOrder(index) {
            this.accepted[index] = true;
        }
    }
}
</script>

<style lang="scss" scoped></style>