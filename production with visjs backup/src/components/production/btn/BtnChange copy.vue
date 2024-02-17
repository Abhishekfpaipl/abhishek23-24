<template>
    <div>
        <button @click="showReadyOrder(order)" class="btn btn-warning" type="button"
            aria-controls="offcanvasRight">Manage</button>

        <div v-if="Object.keys(activeOrder).length !== 0" class="offcanvas offcanvas-end show " tabindex="-1"
            id="offcanvasRight" aria-labelledby="offcanvasRightLabel">
            <div class="offcanvas-body pt-0 px-0">
                <div class="container p-2">
                    <div class="d-flex justify-content-between">
                        <img :src="`${publicPath}${activeOrder.img}`" class="rounded-circle"
                            style="height:60px;width:60px; object-fit: fill;">
                        <div class="d-flex flex-column ms-2" data-bs-toggle="collapse" data-bs-target="#collapseExample">
                            <b class="m-0">#{{ activeOrder.style }} | <span>Bal : {{ activeOrder.bal }}
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
                    <img :src="`${publicPath}${order.img}`" style=" width: 100%;  object-fit: fill;">
                    <div class="box mt-2">
                        <table class="table table-striped table-hover">
                            <tbody>
                                <tr>
                                    <th scope="row">Name</th>
                                    <td class="text-muted">{{ order.name }}</td>
                                </tr>
                                <tr>
                                    <th scope="row">Sale Price</th>
                                    <td class="text-muted">{{ order.sp }}</td>
                                </tr>
                                <tr>
                                    <th scope="row">Panna</th>
                                    <td class="text-muted">{{ order.panna }}</td>
                                </tr>
                                <tr>
                                    <th scope="row">Fc / Piece</th>
                                    <td class="text-muted">{{ order.fc }}</td>
                                </tr>
                                <tr>
                                    <th scope="row">Search Tags</th>
                                    <td class="text-muted">{{ order.stag }}</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>


                <div class="accordion container" id="accordionPanelsStayOpenExample">
                    <h4 class="text-center mt-3">New Order</h4>
                    <div class="accordion-item mt-3">
                        <h2 class="accordion-header" id="panelsStayOpen-headingThree">
                            <button class="accordion-button collapsed bg-warning " type="button" data-bs-toggle="collapse"
                                data-bs-target="#panelsStayOpen-collapseThree" aria-expanded="false"
                                aria-controls="panelsStayOpen-collapseThree">
                                Order Details
                            </button>
                        </h2>
                        <div id="panelsStayOpen-collapseThree" class="accordion-collapse collapse"
                            aria-labelledby="panelsStayOpen-headingThree">
                            <div class="body border border-2 border-warning p-1 ">
                                <div class="mt-3">
                                    <div class="table-responsive " id="scroll" style="font-size: 12px !important;">
                                        <p class="fw-bold fs-5 ">Style ID<span class="fw-normal"> #79887</span></p>
                                        <div class="d-flex pb-2">
                                            <img src="http://dillisix.com/storage/345/-23853.jpg"
                                                style="width: 130px; height: 100px; object-fit: cover;" alt="">
                                            <div class="ms-2 w-100">
                                                <p class="fw-bold mb-1 fs-5"> Pocket Faux Leather Jacket </p>
                                                <p class="mb-1">Order Qty: <span> 1,000 pcs</span></p>
                                                <!-- <p class="fw-bold mb-0">Rate: <span class="fw-normal"> ₹ 50 + 50</span></p> -->
                                                <p class="mb-1">Exp. Time: <span> 12:20 AM, 07 July</span></p>
                                            </div>
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <!-- <div class="accordion-item mt-3">
                        <h2 class="accordion-header" id="panelsStayOpen-headingThree">
                            <button class="accordion-button collapsed bg-warning " type="button" data-bs-toggle="collapse"
                                data-bs-target="#panelsStayOpen-collapseThree" aria-expanded="false"
                                aria-controls="panelsStayOpen-collapseThree">
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
                                                         
                                                        <img src="https://img101.urbanic.com/v1/goods-pic/0c245410ea3b44ac88af213d66b31910UR_w1000_q90.webp"
                                                            width="100"
                                                            class="rounded-circle"
                                                            style="width: 30px; height: 30px; object-fit: contain;" alt="">
                                                    </th>
                                                    <td class=" text-center">
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

                                                        <img src="https://img101.urbanic.com/v1/goods-pic/d30ae897e5e04a948cad58ada2f03f21UR_w1000_q90.webp"
                                                            class="rounded-circle   "
                                                            style="width: 30px; height: 30px; object-fit: contain;" alt="">
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
                    </div> -->
                    <div class="accordion-item mt-3">
                        <h2 class="accordion-header" id="panelsStayOpen-headingThree">
                            <button class="accordion-button collapsed bg-success text-white " type="button"
                                data-bs-toggle="collapse" data-bs-target="#allotment-order" aria-expanded="false"
                                aria-controls="allotment-order">
                                Order Assignment
                            </button>
                        </h2>
                        <div id="allotment-order" class="accordion-collapse collapse"
                            aria-labelledby="panelsStayOpen-headingThree">
                            <div class="body border border-2 border-success p-1 ">
                                <div class="container mt-4">

                                    <div class="input-group mb-3">
                                        <span class="input-group-text" id="basic-addon1">Order Quantity</span>
                                        <input style="background-color: #f8f9fa;" type="number" readonly value="1000"
                                            class="form-control" aria-describedby="basic-addon1">
                                    </div>
                                    <div class="input-group mb-3">
                                        <span class="input-group-text" id="basic-addon1">Available Quantity</span>
                                        <input style="background-color: #f8f9fa;" type="number" readonly value="500"
                                            class="form-control" aria-describedby="basic-addon1">
                                    </div>
                                    <select class="form-select my-3" aria-label="Default select example">
                                        <option selected>Select Worker</option>
                                        <option value="1">Worker 1</option>
                                        <option value="2">Worker 2</option>
                                        <option value="3">Worker 3</option>
                                        <option value="4">Worker 4</option>
                                        <option value="5">Worker 5</option>
                                        <option value="6">Worker 6</option>
                                        <option value="1">Worker 7</option>
                                        <option value="2">Worker 8</option>
                                        <option value="3">Worker 9</option>
                                        <option value="4">Worker 10</option>
                                        <option value="5">Worker 11</option>
                                        <option value="6">Worker 12</option>
                                    </select>
                                    <div class="form-floating mb-3">
                                        <input type="number" class="form-control" id="floatingInput"
                                            placeholder="Catalog Quantity">
                                        <label for="floatingInput">Catalog Quantity</label>
                                    </div>
                                    <div class="d-flex w-100 my-3">
                                        <div class="mb-2 mx-2 w-50">
                                            <label for="date" class="form-label ms-1">Expected Date</label>
                                            <input type="date" class="form-control" id="date">
                                        </div>
                                        <div class="mb-2  mx-2 w-50">
                                            <label for="time" class="form-label ms-1">Expected Time</label>
                                            <input type="time" class="form-control" id="time">
                                        </div>
                                    </div>
                                    <div class="d-flex justify-content-center">
                                        <button class="btn btn-primary">Submit</button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="accordion-item mt-3">
                        <h2 class="accordion-header" id="panelsStayOpen-headingThree">
                            <button class="accordion-button collapsed bg-warning " type="button" data-bs-toggle="collapse"
                                data-bs-target="#production-status" aria-expanded="false" aria-controls="production-status">
                                Production Status
                            </button>
                        </h2>
                        <div id="production-status" class="accordion-collapse collapse"
                            aria-labelledby="panelsStayOpen-headingThree">
                            <div class="body border border-2 border-warning p-1 ">
                                <div class=" mt-4 overflow-x-scroll">
                                    <table class="table table-responsive table-striped table-hover ">
                                        <thead>
                                            <tr style="font-size: 13px;">
                                                <th class="py-3" scope="col">Asign.</th>
                                                <th class="py-3" scope="col">Issue</th>
                                                <th class="py-3" scope="col">Date</th>
                                                <th class="py-3" scope="col">Due</th>
                                                <th class="py-3" scope="col">Loss</th>
                                                <th class="py-3" scope="col">Recv.</th>
                                                <th class="py-3" scope="col">Date</th>
                                                <th class="py-3" scope="col">Bal.</th>
                                            </tr>
                                        </thead>
                                        <tbody>
                                            <tr>
                                                <td><img src="http://dillisix.com/storage/83/IMG20230404151417.jpg"
                                                        class="rounded-circle "
                                                        style="width: 40px; height: 40px; object-fit: cover;" alt="">
                                                </td>
                                                <td>3000</td>
                                                <td>09/07</td>
                                                <td>3000</td>
                                                <td>8000</td>
                                                <td>3000</td>
                                                <td>12/07</td>
                                                <td>3000</td> 
                                            </tr>
                                            <tr>
                                                <td><img src="http://dillisix.com/storage/54/kedar.jpg"
                                                        class="rounded-circle "
                                                        style="width: 40px; height: 40px; object-fit: cover;" alt="">
                                                </td>
                                                <td>3000</td>
                                                <td>03/07</td>
                                                <td>5000</td>
                                                <td>2000</td>
                                                <td>3000</td>
                                                <td>02/08</td>
                                                <td>5000</td> 
                                            </tr>
                                            <tr>
                                                <td><img src="http://dillisix.com/storage/53/narender-profile-image.jpeg"
                                                        class="rounded-circle "
                                                        style="width: 40px; height: 40px; object-fit: cover;" alt="">
                                                </td>
                                                <td>1000</td>
                                                <td>28/07</td>
                                                <td>1000</td>
                                                <td>1000</td>
                                                <td>1000</td>
                                                <td>04/08</td>
                                                <td>1000</td> 
                                            </tr>
                                            <tr>
                                                <td><img src=" http://dillisix.com/storage/54/kedar.jpg"
                                                        class="rounded-circle "
                                                        style="width: 40px; height: 40px; object-fit: cover;" alt="">
                                                </td>
                                                <td>3000</td>
                                                <td>23/07</td>
                                                <td>3000</td>
                                                <td>8000</td>
                                                <td>3000</td>
                                                <td>08/08</td>
                                                <td>3000</td> 
                                            </tr>
                                            <tr>
                                                <td><img src="http://dillisix.com/storage/53/narender-profile-image.jpeg"
                                                        class="rounded-circle "
                                                        style="width: 40px; height: 40px; object-fit: cover;" alt="">
                                                </td>
                                                <td>3000</td>
                                                <td>19/07</td>
                                                <td>5000</td>
                                                <td>2000</td>
                                                <td>3000</td>
                                                <td>12/08</td>
                                                <td>5000</td> 
                                            </tr>
                                            <tr>
                                                <td><img src="http://dillisix.com/storage/83/IMG20230404151417.jpg"
                                                        class="rounded-circle "
                                                        style="width: 40px; height: 40px; object-fit: cover;" alt="">
                                                </td>
                                                <td>1000</td>
                                                <td>16/07</td>
                                                <td>1000</td>
                                                <td>1000</td>
                                                <td>1000</td>
                                                <td>13/08</td>
                                                <td>1000</td> 
                                            </tr>

                                        </tbody>
                                    </table>
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
export default {
    name: 'BtnChange',
    props: ['order'],
    data() {
        return {
            publicPath: process.env.BASE_URL,

        };
    },
    computed: {
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
        },

    },

}

</script>

<style scoped>
table th:nth-child(1),

.table td:nth-child(1) {
    position: sticky;
    left: 0;
    background-color: #e8e8e8;
    color: #373737;
    z-index: 10;
}
</style>