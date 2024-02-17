<template>
    <OrderLinks></OrderLinks>
    <div class="mt-2">
        <div v-for="(order, index) in orders" :key="index" class="border-bottom p-2">
            <div class="d-flex align-items-center">
                <img :src="`${publicPath}${order.img}`" class="rounded-circle"
                    style="height:60px;width:60px; object-fit: fill;">
                <div class="ms-3">
                    <b class="m-0">#{{ order.style }} | <span>Shipped : {{ order.shipped }}</span></b>
                    <p class="m-0">Colors: {{ order.color }} | <span>Sizes: {{ order.size }}</span></p>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import OrderLinks from './OrderLinks.vue';
export default {
    name: "ShippedPage",
    data() {
        return {
            publicPath: process.env.BASE_URL
        }
    },
    computed: {
        orders() {
            return this.$store.getters.getOrder;
        }
    },
    components: { OrderLinks }
}
</script>
