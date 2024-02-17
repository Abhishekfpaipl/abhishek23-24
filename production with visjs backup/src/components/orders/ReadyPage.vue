<template>
    <OrderLinks></OrderLinks>
    <div class="mt-2">
        <div v-for="(order, index) in orders" :key="index" class="border-bottom p-2">
            <div class="d-flex align-items-center" @click="showReadyOrder(order)">
                <img :src="`${publicPath}${order.img}`" class="rounded-circle"
                    style="height:60px;width:60px; object-fit: fill;">
                <div class="ms-3">
                    <b class="m-0">#{{ order.style }} | <span>Ready : {{ order.ready }}</span></b>
                    <p class="m-0">Colors: {{ order.color }} | <span>Sizes: {{ order.size }}</span></p>
                </div>
            </div>
        </div>
        <div v-if="Object.keys(activeOrder).length !== 0">
            <div class="offcanvas offcanvas-end" data-bs-backdrop="static" tabindex="-1" id="staticBackdrop"
                aria-labelledby="staticBackdropLabel">
                <div class="offcanvas-header border d-flex">
                    <img :src="`${publicPath}${activeOrder.img}`" class="rounded-circle"
                        style="height:60px;width:60px; object-fit: fill;">
                    <div class="d-flex flex-column">
                        <b class="m-0">#{{ activeOrder.style }} | <span>Bal : {{ activeOrder.ready }}</span></b>
                        <p class="m-0 text-success">{{ activeOrder.date }} | <span>{{ activeOrder.time }}</span></p>
                    </div>
                    <button type="button" class="btn" @click="hideReadyOrder()"><i class="bi bi-x fs-4"></i></button>
                </div>
                <div class="offcanvas-body pt-0">
                    <h4 class="text-center mt-4">Ready Quantity Chart</h4>
                    <div class="card rounded-0 p-3 mt-4">
                        <p class="text-center m-0">Click here, if Complete Order Qty is Ready</p>
                    </div>
                    <div class="mt-4 ">
                        <p class="text-success m-0"> Green Qty Indicates Complete Order Qty</p>
                        <p class="text-primary m-0"> Blue Qty Indicates Ready Qty</p>
                    </div>


                    <div class="border mt-4">
                        <div class="table-responsive  border-1" id="scroll"
                            style="font-size: 12px !important;">
                            <table class="table m-0">
                                <thead>
                                    <tr>
                                        <th scope="col" class="text-center"> Qty</th>
                                        <th scope="col">
                                            <div class="d-flex flex-column">
                                                <p class="m-0 text-center">XS</p>
                                            </div>
                                        </th>
                                        <th scope="col">
                                            <div class="d-flex flex-column">
                                                <p class="m-0 text-center">S</p>
                                            </div>
                                        </th>
                                        <th scope="col">
                                            <div class="d-flex flex-column">
                                                <p class="m-0 text-center">M</p>
                                            </div>
                                        </th>
                                        <th scope="col">
                                            <div class="d-flex flex-column">
                                                <p class="m-0 text-center">L</p>
                                            </div>
                                        </th>
                                        <th scope="col">
                                            <div class="d-flex flex-column">
                                                <p class="m-0 text-center">XL</p>
                                            </div>
                                        </th>
                                        <th scope="col">
                                            <div class="d-flex flex-column">
                                                <p class="m-0 text-center">Free</p>
                                            </div>
                                        </th>
                                        <th colspan="2" class="text-center">All same</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr>
                                        <th scope="row" style="font-size:14px">
                                            <div class="rounded-circle m-2 px-1 align-items-center justify-content-center d-flex"
                                                style="width: 30px; height: 30px;background-color:black"></div>
                                        </th>
                                        <td class="text-center">
                                            <input type="number" class="form-control" style="width: 50px;font-size: 15px !important;"
                                                placeholder="10">
                                        </td>
                                        <td class="text-center">
                                            <input type="number" class="form-control" style="width: 50px;font-size: 15px !important;"
                                                placeholder="20">
                                        </td>
                                        <td class="text-center">
                                            <input type="number" class="form-control" style="width: 50px;font-size: 15px !important;"
                                                placeholder="30">
                                        </td>
                                        <td class="text-center">
                                            <input type="number" class="form-control" style="width: 50px;font-size: 15px !important;"
                                                placeholder="40">
                                        </td>
                                        <td class="text-center">
                                            <input type="number" class="form-control" style="width: 50px;font-size: 15px !important;"
                                                placeholder="50">
                                        </td>
                                        <td class="text-center">
                                            <input type="number" class="form-control" style="width: 50px;font-size: 15px !important;"
                                                placeholder="60">
                                        </td>
                                        <td class="text-center">
                                            <p class="m-0" style="width: 50px;font-size: 15px !important;">Copy</p>
                                        </td>
                                        <td class="text-center">
                                            <p class="m-0" style="width: 50px;font-size: 15px !important;">Pase</p>
                                        </td>
                                    </tr>
                                    <tr>
                                        <th scope="row" style="font-size:14px">
                                            <div class="rounded-circle m-2 px-1 align-items-center justify-content-center d-flex"
                                                style="width: 30px; height: 30px;background-color:red"></div>
                                        </th>
                                        <td class="text-center">
                                            <input type="number" class="form-control" placeholder="10" style="width: 50px;font-size: 15px !important;">
                                        </td>
                                        <td class="text-center">
                                            <input type="number" class="form-control" placeholder="20" style="width: 50px;font-size: 15px !important;">
                                        </td>
                                        <td class="text-center">
                                            <input type="number" class="form-control" placeholder="30" style="width: 50px;font-size: 15px !important;">
                                        </td>
                                        <td class="text-center">
                                            <input type="number" class="form-control" placeholder="40" style="width: 50px;font-size: 15px !important;">
                                        </td>
                                        <td class="text-center">
                                            <input type="number" class="form-control" placeholder="50" style="width: 50px;font-size: 15px !important;">
                                        </td>
                                        <td class="text-center">
                                            <input type="number" class="form-control" placeholder="60" style="width: 50px;font-size: 15px !important;">
                                        </td>
                                        <td class="text-center">
                                            <p class="m-0" style="width: 50px;font-size: 15px !important;">Copy</p>
                                        </td>
                                        <td class="text-center">
                                            <p class="m-0" style="width: 50px;font-size: 15px !important;">Paste</p>
                                        </td>
                                    </tr>
                                </tbody>
                            </table>

                        </div>
                        <div class="container d-flex justify-content-between gap-4 w-100"
                            style="font-size: 12px !important; padding:12px;">
                            <p class="m-0 card rounded-0 p-3 w-50 text-center fw-bold">Grand Total</p>
                            <p class="m-0 card rounded-0 p-3 w-50 text-center fw-bold">₹9576</p>
                        </div>

                        <div class="card rounded-0 text-center p-3">Submit
                        </div>
                    </div>





                </div>




            </div>
        </div>
    </div>
</template>

<script>
import OrderLinks from './OrderLinks.vue';
export default {
    name: "NewPage",
    data() {
        return {
            publicPath: process.env.BASE_URL
        }
    },
    computed: {   
        orders() {
            return this.$store.getters.getOrder;
        },
        activeOrder() {
            return this.$store.getters.getActiveReadyOrder;
        }
    },
    components: { OrderLinks },
    methods: {
        showReadyOrder(order) {
            return this.$store.dispatch('selectReadyOrder', order);
        },
        hideReadyOrder() {
            return this.$store.dispatch('hideReadyOrder');
        }
    },
}
</script>
<style scoped>
#scroll::-webkit-scrollbar {
    background-color: none;
    display: none;
}
table th:first-child,
.table td:first-child {
    position: sticky;
    left: 0;
    background-color: #e8e8e8;
    color: #373737;
}
</style>