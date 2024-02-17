<template>
    <OrderLinks></OrderLinks>
    <div class="mt-2">
        <div v-for="(order, index) in orders" :key="index" class="border-bottom p-2">
            <div class="d-flex align-items-center" @click="showReadyOrder(order)">
                <img :src="`${publicPath}${order.img}`" class="rounded-circle"
                    style="height:60px;width:60px; object-fit: fill;">
                <div class="ms-3">
                    <b class="m-0">#{{ order.style }} | <span>Qty : {{ order.qty }}</span></b>
                    <p class="m-0">{{ order.status }}</p>
                </div>
            </div>
        </div>

        <div v-if="Object.keys(activeOrder).length !== 0" class="">
            <div class="offcanvas offcanvas-end show " data-bs-backdrop="static" tabindex="-1" id="staticBackdrop"
                aria-labelledby="offcanvasWithBackdropLabel">
                <!-- ---------------------- -->
                <div class="offcanvas-body pt-0 px-0">
                    <div class="container p-2">
                        <div class="d-flex justify-content-between">
                            <img :src="`${publicPath}${activeOrder.img}`" class="rounded-circle"
                                style="height:60px;width:60px; object-fit: fill;">
                            <div class="d-flex flex-column ms-2" data-bs-toggle="collapse"
                                data-bs-target="#collapseExample">
                                <b class="m-0">#{{ activeOrder.style }} | <span>Bal : {{ activeOrder.ready }}
                                    </span>
                                </b>
                                <p class="m-0 text-success">{{ activeOrder.date }} | <span>{{ activeOrder.time }}
                                    </span>
                                </p>
                            </div>
                            <button class="btn" type="button" data-bs-toggle="collapse" data-bs-target="#collapseExample"
                                aria-expanded="false" aria-controls="collapseExample">
                                <i class="bi bi-chevron-down"></i>
                            </button>
                            <button type="button" class="btn" @click="hideReadyOrder()">
                                <i class="bi bi-x fs-4"></i>
                            </button>

                        </div>

                    </div>
                    <div class="collapse" id="collapseExample">
                        <img :src="`${publicPath}${activeOrder.img}`" style=" width: 100%;  object-fit: fill;">
                        <div class="box mt-2">
                            <table class="table table-striped table-hover">
                                <tbody>
                                    <tr>
                                        <th scope="row">Name</th>
                                        <td class="text-muted">{{ activeOrder.name }}</td>
                                    </tr>
                                    <tr>
                                        <th scope="row">Sale Price</th>
                                        <td class="text-muted">{{ activeOrder.sp }}</td>
                                    </tr>
                                    <tr>
                                        <th scope="row">Panna</th>
                                        <td class="text-muted">{{ activeOrder.panna }}</td>
                                    </tr>
                                    <tr>
                                        <th scope="row">Fc / Piece</th>
                                        <td class="text-muted">{{ activeOrder.fc }}</td>
                                    </tr>
                                    <tr>
                                        <th scope="row">Search Tags</th>
                                        <td class="text-muted">{{ activeOrder.stag }}</td>
                                    </tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                    <div class="accordion container" id="accordionPanelsStayOpenExample">
                        <h4 class="text-center mt-3">New Order</h4>
                        <div class="accordion-item mt-3">
                            <h2 class="accordion-header" id="headingTwo">
                                <button class="accordion-button collapsed bg-success text-white" type="button"
                                    data-bs-toggle="collapse" data-bs-target="#collapseTwo" aria-expanded="false"
                                    aria-controls="collapseTwo">
                                    Progress Stage
                                </button>
                            </h2>
                            <div id="collapseTwo" class="accordion-collapse collapse" aria-labelledby="headingTwo"
                                data-bs-parent="#accordionExample">
                                <div class="body border border-2 border-success">
                                    <p class="border-1 border-bottom p-2 m-0" style="font-size: 14px;"><i
                                            class="bi bi-check2-circle"></i>
                                        New Order Posted</p>
                                    <div class="d-flex justify-content-between p-2 border-1 border-bottom py-2">
                                        <button class="btn btn-warning text-center w-100">Accept Order</button>
                                    </div>
                                    <p class="text-danger border-1 border-bottom p-2 m-0" style="font-size: 14px;"><i
                                            class="bi bi-dash-circle"></i>
                                        Manager Has Accepted</p>
                                    <p class="text-danger border-1 border-bottom p-2 m-0" style="font-size: 14px;"><i
                                            class="bi bi-dash-circle"></i>
                                        Material is Available At Godown</p>

                                    <p class="text-danger border-1 border-bottom p-2 m-0" style="font-size: 14px;"><i
                                            class="bi bi-dash-circle"></i>
                                        Material is Arrange For Delivery</p>

                                    <p class="text-danger border-1 border-bottom p-2 m-0" style="font-size: 14px;"><i
                                            class="bi bi-dash-circle"></i>
                                        Material Delivery To Assignee</p>

                                    <p class="text-danger border-1 border-bottom p-2 m-0" style="font-size: 14px;"><i
                                            class="bi bi-dash-circle"></i>
                                        Production Has Started</p>
                                    <p class="text-danger border-1 border-bottom p-2 m-0" style="font-size: 14px;"><i
                                            class="bi bi-dash-circle"></i>
                                        Order is Available For Dispatch</p>
                                    <p class="text-danger border-1 border-bottom p-2 m-0" style="font-size: 14px;"><i
                                            class="bi bi-dash-circle"></i>
                                        Order Completely Dispatched</p>
                                </div>
                            </div>
                        </div>
                        <div class="accordion-item mt-3">
                            <h2 class="accordion-header" id="panelsStayOpen-headingThree">
                                <button class="accordion-button collapsed bg-warning " type="button"
                                    data-bs-toggle="collapse" data-bs-target="#panelsStayOpen-collapseThree"
                                    aria-expanded="false" aria-controls="panelsStayOpen-collapseThree">
                                    Order-quantity
                                </button>
                            </h2>
                            <div id="panelsStayOpen-collapseThree" class="accordion-collapse collapse"
                                aria-labelledby="panelsStayOpen-headingThree">
                                <div class="body border border-2 border-warning p-1 ">
                                    <div class="border mt-4">
                                        <div class="table-responsive " id="scroll" style="font-size: 12px !important;">
                                            <table class="table m-0">
                                                <thead>
                                                    <tr>
                                                        <th scope="col" class="text-center">Qty</th>
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
                                                    </tr>
                                                </thead>
                                                <tbody>
                                                    <tr>
                                                        <th scope="row" style="font-size:14px">
                                                            <div class="rounded-circle m-2 px-1 align-items-center justify-content-center d-flex"
                                                                style="width: 30px; height: 30px;background-color:black">
                                                            </div>
                                                        </th>
                                                        <td class="text-center">
                                                            <input type="number" class="form-control"
                                                                style="width: 50px;font-size: 15px !important;"
                                                                placeholder="10">
                                                        </td>
                                                        <td class="text-center">
                                                            <input type="number" class="form-control"
                                                                style="width: 50px;font-size: 15px !important;"
                                                                placeholder="20">
                                                        </td>
                                                        <td class="text-center">
                                                            <input type="number" class="form-control"
                                                                style="width: 50px;font-size: 15px !important;"
                                                                placeholder="30">
                                                        </td>
                                                        <td class="text-center">
                                                            <input type="number" class="form-control"
                                                                style="width: 50px;font-size: 15px !important;"
                                                                placeholder="40">
                                                        </td>
                                                        <td class="text-center">
                                                            <input type="number" class="form-control"
                                                                style="width: 50px;font-size: 15px !important;"
                                                                placeholder="50">
                                                        </td>
                                                        <td class="text-center">
                                                            <input type="number" class="form-control"
                                                                style="width: 50px;font-size: 15px !important;"
                                                                placeholder="60">
                                                        </td>
                                                    </tr>
                                                    <tr>
                                                        <th scope="row" style="font-size:14px">
                                                            <div class="rounded-circle m-2 px-1 align-items-center justify-content-center d-flex"
                                                                style="width: 30px; height: 30px;background-color:red">
                                                            </div>
                                                        </th>
                                                        <td class="text-center">
                                                            <input type="number" class="form-control" placeholder="10"
                                                                style="width: 50px;font-size: 15px !important;">
                                                        </td>
                                                        <td class="text-center">
                                                            <input type="number" class="form-control" placeholder="20"
                                                                style="width: 50px;font-size: 15px !important;">
                                                        </td>
                                                        <td class="text-center">
                                                            <input type="number" class="form-control" placeholder="30"
                                                                style="width: 50px;font-size: 15px !important;">
                                                        </td>
                                                        <td class="text-center">
                                                            <input type="number" class="form-control" placeholder="40"
                                                                style="width: 50px;font-size: 15px !important;">
                                                        </td>
                                                        <td class="text-center">
                                                            <input type="number" class="form-control" placeholder="50"
                                                                style="width: 50px;font-size: 15px !important;">
                                                        </td>
                                                        <td class="text-center">
                                                            <input type="number" class="form-control" placeholder="60"
                                                                style="width: 50px;font-size: 15px !important;">
                                                        </td>
                                                    </tr>
                                                </tbody>
                                            </table>

                                        </div>
                                        <div class="d-flex justify-content-center">
                                            <button class="btn btn-secondary m-2">Submit</button>
                                        </div>
                                    </div>
                                </div>
                            </div>
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
    components: { OrderLinks },
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
.accordion {
    --bs-accordion-active-bg: none;
}

.accordion-button:focus {
    border-color: none;
    box-shadow: none;
}

.btn {
    --bs-btn-border-width: none;
}
</style>
