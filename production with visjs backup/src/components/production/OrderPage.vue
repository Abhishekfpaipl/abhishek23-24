<template>
    <!-- <ProductionLinks active="Order"></ProductionLinks> -->
    <TopNav>Line Incharge</TopNav>
    <div class="mt-2">
        <div v-for="(production, index) in productions" :key="index"
            class="d-flex justify-content-between align-items-center border-bottom p-2">
            <div class="d-flex align-items-center">
                <img :src="`${publicPath}${production.img}`" class="rounded-circle"
                    style="height:60px;width:60px; object-fit: fill;">
                <div class="ms-3">
                    <p class="m-0">#{{ production.style }} | <span>Qty : {{ production.qty }}</span></p>
                    <p class="m-0">Costing : {{ production.costing }}</p>
                </div>
            </div>
            <div class="text-success rounded">
                <div v-if="accepted[index]">
                    <BtnChange :production="production"></BtnChange>
                </div>
                <div class="" v-else>
                    <button @click="acceptOrder(index)" class="btn btn-success">Accept</button>
                </div>
            </div>
        </div>
    </div>
    <ProductionBottomnav></ProductionBottomnav>
</template>

<script>
import TopNav from '../navbar/TopNav.vue';
import BtnChange from '@/components/production/btn/BtnChange.vue';

export default {
    name: "InwardPage",
    components: { TopNav, BtnChange },
    data() {
        return {
            publicPath: process.env.BASE_URL,
            accepted: []
        };
    },
    computed: {
        productions() {
            return this.$store.getters.getProductions;
        }
    },
    methods: {
        acceptOrder(index) {
            this.accepted[index] = true;
        }
    }

}
</script>
 