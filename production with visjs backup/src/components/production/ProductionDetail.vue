<template>
    <div>
            <div class="  pt-0 px-0" style="background-color: #e8e8e8;">
                <div class="container p-2 border-bottom bg-white" style="     ;">
                    <div class="d-flex justify-content-between">
                       <div class="d-flex">
                        <img :src="`${publicPath}${order.img}`" class="rounded-circle"
                            style="height:60px;width:60px; object-fit: fill;">
                        <div class="d-flex flex-column ms-2" data-bs-toggle="collapse" data-bs-target="#collapseExample">
                            <b class="m-0">#{{ order.style }} | <span>Bal : {{ order.bal }}
                                </span>
                            </b>
                            <p class="m-0 text-success">{{ order.date }} | <span>{{ order.time }}
                                </span>
                            </p>
                        </div>
                       </div>
                        <div class="d-flex">
                            <button class="btn" type="button" data-bs-toggle="collapse" data-bs-target="#collapseExample"
                            aria-expanded="false" aria-controls="collapseExample">
                            <i class="bi bi-chevron-down"></i>
                        </button>
                        <RouterLink to="/production/order">
                            <button type="button" class="btn" >
                                <i class="bi bi-x fs-4"></i>
                            </button>
                        </RouterLink>
                        </div>

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
                      
                    <div class="bg-white rounded">
                        <nav class="mt-3">
                            <div class="nav nav-tabs d-flex justify-content-center w-100" id="nav-tab" role="tablist">
                                <button class="nav-link active w-50" id="nav-assignment-tab" data-bs-toggle="tab"
                                    data-bs-target="#nav-assignment" type="button" role="tab" aria-controls="nav-assignment"
                                    aria-selected="false">Order Assignment</button>
                                <button class="nav-link w-50" id="nav-collection-tab" data-bs-toggle="tab"
                                    data-bs-target="#nav-collection" type="button" role="tab" aria-controls="nav-collection"
                                    aria-selected="false">Order Collection</button>
                            </div>
                        </nav>
                        <div class="tab-content" id="nav-tabContent">
                            <div class="tab-pane fade show active bg-white py-2" id="nav-assignment" role="tabpanel"
                                aria-labelledby="nav-assignment-tab">
                                <div class="container mt-4">
                                    <div class="input-group mb-3 w-100">
                                        <span class="input-group-text w-75" id="basic-addon1">Order Quantity</span>
                                        <input style="background-color: #f8f9fa;" type="number" readonly value="1000"
                                            class="form-control w-25" aria-describedby="basic-addon1">
                                    </div>
                                    <div class="input-group mb-3 w-100">
                                        <span class="input-group-text w-75" id="basic-addon1">Available Order Quantity</span>
                                        <input style="background-color: #f8f9fa;" type="number" readonly value="500"
                                            class="form-control w-25" aria-describedby="basic-addon1">
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
                                        <label for="floatingInput">Issued Quantity</label>
                                    </div>
                                    <div class="d-flex w-100 my-3">
                                        <div class="mb-2 mx-2 w-50">
                                            <label for="date" class="form-label ms-1">Expected Date</label>
                                            <input type="date" class="form-control" id="date" v-model="selectedDate">
                                        </div>
                                        <div class="mb-2  mx-2 w-50">
                                            <label for="time" class="form-label ms-1">Expected Time</label>
                                            <input type="time" class="form-control" id="time" v-model="selectedTime">
                                        </div>
                                    </div>
                                    <div class="d-flex justify-content-center mb-3">
                                        <button class="btn btn-primary">Submit</button>
                                    </div>
                                </div>
                            </div>
                            <div class="tab-pane fade bg-white py-2" id="nav-collection" role="tabpanel"
                                aria-labelledby="nav-collection-tab">
                                <div class="container mt-4">
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
                                    <div class="input-group mb-3 w-100">
                                        <span class="input-group-text w-75" id="basic-addon1">Issued Quantity</span>
                                        <input style="background-color: #f8f9fa;" type="number" value='1000' readonly
                                            class="form-control w-25" aria-describedby="basic-addon1">
                                    </div>
                                    <div class="input-group mb-3 w-100">
                                        <span class="input-group-text w-75" id="basic-addon1">Available Issued
                                            Quantity</span>
                                        <input v-model="availableQuantity" style="background-color: #f8f9fa;" type="number"
                                            class="form-control w-25" aria-describedby="basic-addon1">
                                    </div>
                                    <div class="form-floating mb-3">
                                        <input v-model="collectedQuantity" type="number" class="form-control"
                                            id="floatingInput" placeholder="Catalog Quantity">
                                        <label for="floatingInput">Collected Quantity</label>
                                    </div>
                                    <div class="input-group mb-3 w-100">
                                        <span class="input-group-text w-75" id="basic-addon1">Balance Quantity</span>
                                        <input style="background-color: #f8f9fa;" type="number" class="form-control w-25"
                                            aria-describedby="basic-addon1" :value="balanceQuantity()">
                                    </div>
                                    <div class="d-flex w-100 my-3">
                                        <div class="mb-2 mx-2 w-50">
                                            <label for="date" class="form-label ms-1">Collection Date</label>
                                            <input type="date" class="form-control" id="date" v-model="selectedDate">
                                        </div>
                                        <div class="mb-2  mx-2 w-50">
                                            <label for="time" class="form-label ms-1">Collection Time</label>
                                            <input type="time" class="form-control" id="time" v-model="selectedTime">
                                        </div>
                                    </div>
                                    <div class="d-flex justify-content-center mb-3">
                                        <button class="btn btn-primary">Submit</button>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                  
                    <div class="accordion-item  mt-3 mb-5">
                        <h2 class="accordion-header" id="panelsStayOpen-headingThree">
                            <button class="accordion-button  border" type="button" data-bs-toggle="collapse"
                                data-bs-target="#production-status" aria-expanded="false" aria-controls="production-status">
                                Production Status
                            </button>
                        </h2>
                        <div id="production-status" class="accordion-collapse collapse show"
                            aria-labelledby="panelsStayOpen-headingThree">
                            <div class="body  border border-2 p-1 ">
                                <div class="overflow-x-scroll">
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

   
</template>

<script>
    export default {
        data() {
        return {
            publicPath: process.env.BASE_URL,
            availableQuantity: 800,
            collectedQuantity: 0,
            

        };
    },
    computed: {
        order() {
            let productionId = this.$route.params.productionId;
            return this.$store.getters.getProduction(productionId);
        },
    },
    methods:{
        balanceQuantity() {
            return this.availableQuantity - this.collectedQuantity;
        },
    }
    }
</script>

<style scoped>
.nav-link.active {
    color: #fff;
    background-color: #606C5D;
}

.nav-link {
    color: #000000;
}
.accordion-button:not(.collapsed) {
    color: #fff;
    background-color: none;
}

.accordion {
    --bs-accordion-active-bg: #606C5D !important;
    --bs-accordion-btn-focus-box-shadow: none;
    --bs-accordion-active-color: #ffffff;
    --bs-accordion-btn-icon-width: 1rem;
}

.accordion-item {
    border: none;
}
</style>