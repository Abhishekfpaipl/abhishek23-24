<template>
    <TopNav>Incharge</TopNav>
    <FilterPageV2></FilterPageV2>
    <div class="mt-2">
        <div v-for="(subfab, index) in subfabs" :key="index"
            class="d-flex justify-content-between align-items-center border-bottom p-2">
            <div class="d-flex align-items-center">
                <img :src="`${publicPath}${subfab.img}`" class="rounded-circle"
                    style="height:60px;width:60px; object-fit: fill;">
                <div class="ms-3">
                    <p class="m-0 fw-bold" style="font-size: 1.2rem;">#{{ subfab.style }}</p>
                    <p class="m-0">Order Qty : {{ subfab.costing }}</p>
                </div>
            </div>
            <div class="text-success rounded">
                <div v-if="accepted[index]">
                    <BtnChange :subfab="subfab"></BtnChange>
                </div>
                <div class="" v-else>
                    <button @click="acceptOrder(index)" style="width: 6em;" class="btn btn-success">Accept</button>
                </div>
            </div>
        </div>
    </div>
    <div class="mt-2">
        <div v-for="(subfab, index) in subfabs" :key="index"
            class="d-flex justify-content-between align-items-center border-bottom p-2">
            <div class="d-flex align-items-center">
                <img :src="`${publicPath}${subfab.img}`" class="rounded-circle"
                    style="height:60px;width:60px; object-fit: fill;">
                    <div class="ms-3">
                    <p class="m-0 fw-bold" style="font-size: 1.2rem;">#{{ subfab.style }}</p>
                    <p class="m-0">Order Qty : {{ subfab.costing }}</p>
                </div>
            </div>
            <div class="text-success rounded">
                <button class="btn btn-warning" style="width: 6em;">Manage</button>
            </div>
        </div>
    </div>
    <div class="mt-2">
        <div v-for="(subfab, index) in subfabs" :key="index"
            class="d-flex justify-content-between align-items-center border-bottom p-2">
            <div class="d-flex align-items-center">
                <img :src="`${publicPath}${subfab.img}`" class="rounded-circle"
                    style="height:60px;width:60px; object-fit: fill;">
                    <div class="ms-3">
                    <p class="m-0 fw-bold" style="font-size: 1.2rem;">#{{ subfab.style }}</p>
                    <p class="m-0">Order Qty : {{ subfab.costing }}</p>
                </div>
            </div>
            <div class="text-success rounded">
                <button class="btn btn-primary" style="width: 6em;">Completed</button>
            </div>
        </div>
    </div>
</template>

<script>

import TopNav from '../navbar/TopNav.vue';
import BtnChange from './BtnChange.vue';
import FilterPageV2 from '../Filter/FilterPageV2.vue';
export default {
    name: "subfabPage",
    components: { TopNav, BtnChange, FilterPageV2 },
    data() {
        return {
            publicPath: process.env.BASE_URL,
            accepted: []
        };
    },
    computed: {
        subfabs() {
            return this.$store.getters.getSubfabs;
        }
    },
    methods: {
        acceptOrder(index) {
            this.accepted[index] = true;
        }
    }

}
</script>

<style scoped></style>
 