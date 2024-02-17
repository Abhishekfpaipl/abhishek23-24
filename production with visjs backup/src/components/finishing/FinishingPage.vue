<template>
    <div style="padding-bottom: 80px;">
        <TopNav> Finishing Incharge</TopNav>
        <div class="mt-2">
            <div v-for="(finishing, index) in finishings" :key="index"
                class="d-flex justify-content-between align-items-center border-bottom p-2">
                <div class="d-flex align-items-center">
                    <img :src="`${publicPath}${finishing.img}`" class="rounded-circle"
                        style="height:60px;width:60px; object-fit: fill;">
                    <div class="ms-3">
                        <p class="m-0">#{{ finishing.style }} | <span>Qty : {{ finishing.qty }}</span></p>
                        <p class="m-0">Costing : {{ finishing.costing }}</p>
                    </div>
                </div>
                <div class="text-success rounded">
                    <div v-if="accepted[index]">
                        <BtnChange :finishing="finishing"></BtnChange>
                    </div>
                    <div class="" v-else>
                        <button @click="acceptOrder(index)" class="btn btn-success">Accept</button>
                    </div>
                </div>
            </div>
        </div>
 
    </div>
</template>

<script>


import TopNav from '../navbar/TopNav.vue';
import BtnChange from './BtnChange.vue';

export default {
    components: { TopNav, BtnChange },
    data() {
        return {
            publicPath: process.env.BASE_URL,
            accepted: []
        };
    },
    computed: {
        finishings() {
            return this.$store.getters.getFinishings;
        }
    },
    methods: {
        acceptOrder(index) {
            this.accepted[index] = true;
        }
    }
}
</script>

 