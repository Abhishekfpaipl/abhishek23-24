<template>
    <ProductionLinks active="Order"></ProductionLinks>
    <div class="mt-2">
        <div v-for="(order, index) in orders" :key="index"
            class="d-flex justify-content-between align-items-center border-bottom p-2">
            <div class="d-flex align-items-center">
                <img :src="`${publicPath}${order.img}`" class="rounded-circle"
                    style="height:60px;width:60px; object-fit: fill;">
                <div class="ms-3">
                    <p class="m-0 fw-bold">#{{ order.style }} | <span>Qty : {{ order.qty }}</span></p>
                    <p class="m-0" style="font-size: 13px;">Exp. Date : {{ order.date }}</p>
                </div>
            </div>
            <div class="text-success rounded">
                <button type="button" style="font-size: 14px;" data-bs-toggle="modal" data-bs-target="#exampleModal"
                    class="btn" :class="order.btn">
                    {{ order.assign }}
                </button>
            </div>
            <!-- Modal -->
            <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
                <div class="modal-dialog">
                    <div class="modal-content">
                        <div class="modal-header">
                            <h5 class="modal-title" id="exampleModalLabel">#{{ order.style }}</h5>
                            <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                        </div>
                        <div class="modal-body">
                            <h4 class="text-center mb-4">Assign this catalog</h4>
                            <div class="d-flex justify-content-evenly my-4">
                                <button class="btn btn-warning" data-bs-dismiss="modal"
                                    aria-label="Close">Fabrication</button>
                                <button class="btn btn-info" data-bs-dismiss="modal" aria-label="Close">Production</button>
                            </div>
                        </div>

                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import ProductionLinks from './ProductionLinks.vue';
export default {
    name: "InwardPage",
    data() {
        return {
            publicPath: process.env.BASE_URL
        };
    },
    computed: {
        orders() {
            return this.$store.getters.getProductionOrder;
        }
    },
    components: { ProductionLinks }
}
</script>

<style lang="scss" scoped></style>