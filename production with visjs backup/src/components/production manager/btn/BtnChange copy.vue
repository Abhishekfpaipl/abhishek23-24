<template>
    <div>
        <button @click="showManager(manager)" class="btn btn-warning" type="button"
            aria-controls="offcanvasRight">Manage</button>

        <div v-if="Object.keys(activeManager).length !== 0" class="offcanvas offcanvas-end show " tabindex="-1"
            id="offcanvasRight" aria-labelledby="offcanvasRightLabel">
            <div class="offcanvas-body pt-0 px-0">
                <div class="container p-2">
                    <div class="d-flex justify-content-between">
                        <img :src="`${publicPath}${activeManager.img}`" class="rounded-circle"
                            style="height:60px;width:60px; object-fit: fill;">
                        <div class="d-flex flex-column ms-2" data-bs-toggle="collapse" data-bs-target="#collapseExample">
                            <b class="m-0">#{{ activeManager.style }} | <span>Bal : {{ activeManager.bal }}
                                </span>
                            </b>
                            <p class="m-0 text-success">{{ activeManager.date }} | <span>{{ activeManager.time }}
                                </span>
                            </p>
                        </div>
                        <button class="btn" type="button" data-bs-toggle="collapse" data-bs-target="#collapseExample"
                            aria-expanded="false" aria-controls="collapseExample">
                            <i class="bi bi-chevron-down"></i>
                        </button>
                        <button type="button" class="btn" @click="hideManager()">
                            <i class="bi bi-x fs-4"></i>
                        </button>

                    </div>

                </div>
                <div class="collapse" id="collapseExample">
                    <img :src="`${publicPath}${activeManager.img}`" style=" width: 100%;  object-fit: fill;">
                    <div class="box mt-2 container">
                        <table class="table table-striped table-hover ">
                            <tbody>
                                <tr>
                                    <th scope="row">Name</th>
                                    <td class="text-muted">{{ activeManager.name }}</td>
                                </tr>
                                <tr>
                                    <th scope="row">Sale Price</th>
                                    <td class="text-muted">{{ activeManager.sp }}</td>
                                </tr>
                                <tr>
                                    <th scope="row">Panna</th>
                                    <td class="text-muted">{{ activeManager.panna }}</td>
                                </tr>
                                <tr>
                                    <th scope="row">Fc / Piece</th>
                                    <td class="text-muted">{{ activeManager.fc }}</td>
                                </tr>
                                <tr>
                                    <th scope="row">Search Tags</th>
                                    <td class="text-muted">{{ activeManager.stag }}</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>


                <div class="accordion container" id="accordionPanelsStayOpenExample">
                    <h4 class="text-center mt-3">Order Details</h4>
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
                                    Production Has Started</p>
                                <div class="d-flex justify-content-between p-2 border-1 border-bottom py-2">
                                    <button class="btn btn-warning text-center w-100">Start</button>
                                </div>
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
                            <button class="accordion-button collapsed bg-warning " type="button" data-bs-toggle="collapse"
                                data-bs-target="#Status" aria-expanded="false" aria-controls="Status">
                                Order-Status
                            </button>
                        </h2>
                        <div id="Status" class="accordion-collapse collapse" aria-labelledby="panelsStayOpen-headingThree">
                            <div class="body border border-2 border-warning p-1 ">
                                <div class=" mt-4 overflow-x-scroll">
                                    <table class="table table-responsive table-striped table-hover ">
                                        <thead>
                                            <tr style="font-size: 13px;">
                                                <th class="py-3" scope="col">Shop</th>
                                                <th class="py-3" scope="col">Bal.</th>
                                                <th class="py-3" scope="col">Ready</th>
                                                <th class="py-3" scope="col">Send</th>
                                                <th class="py-3" scope="col">Disp.</th>
                                                <th class="py-3" scope="col">Rec.</th>

                                            </tr>
                                        </thead>
                                        <tbody>
                                            <tr>
                                                <td><img src="http://dillisix.com/storage/83/IMG20230404151417.jpg"
                                                        class="rounded-circle "
                                                        style="width: 40px; height: 40px; object-fit: cover;" alt="">
                                                </td>
                                                <td>3000</td>
                                                <td>6000</td>
                                                <td>3000</td>
                                                <td>3000</td>
                                                <td>2000</td>

                                            </tr>
                                            <tr>
                                                <td><img src="http://dillisix.com/storage/54/kedar.jpg"
                                                        class="rounded-circle "
                                                        style="width: 40px; height: 40px; object-fit: cover;" alt="">
                                                </td>
                                                <td>3000</td>
                                                <td>7000</td>
                                                <td>5000</td>
                                                <td>3000</td>
                                                <td>8000</td>

                                            </tr>
                                            <tr>
                                                <td><img src="http://dillisix.com/storage/53/narender-profile-image.jpeg"
                                                        class="rounded-circle "
                                                        style="width: 40px; height: 40px; object-fit: cover;" alt="">
                                                </td>
                                                <td>1000</td>
                                                <td>6000</td>
                                                <td>1000</td>
                                                <td>1000</td>
                                                <td>1000</td>

                                            </tr>
                                            <tr>
                                                <td><img src=" http://dillisix.com/storage/54/kedar.jpg"
                                                        class="rounded-circle "
                                                        style="width: 40px; height: 40px; object-fit: cover;" alt="">
                                                </td>
                                                <td>3000</td>
                                                <td>5000</td>
                                                <td>3000</td>
                                                <td>8000</td>
                                                <td>2000</td>

                                            </tr>
                                            <tr>
                                                <td><img src="http://dillisix.com/storage/53/narender-profile-image.jpeg"
                                                        class="rounded-circle "
                                                        style="width: 40px; height: 40px; object-fit: cover;" alt="">
                                                </td>
                                                <td>3000</td>
                                                <td>6000</td>
                                                <td>5000</td>
                                                <td>2000</td>
                                                <td>6000</td>

                                            </tr>
                                            <tr>
                                                <td><img src="http://dillisix.com/storage/83/IMG20230404151417.jpg"
                                                        class="rounded-circle "
                                                        style="width: 40px; height: 40px; object-fit: cover;" alt="">
                                                </td>
                                                <td>1000</td>
                                                <td>6000</td>
                                                <td>1000</td>
                                                <td>1000</td>
                                                <td>6000</td>

                                            </tr>

                                        </tbody>
                                    </table>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="accordion-item mt-3">
                        <h2 class="accordion-header" id="panelsStayOpen-headingThree">
                            <button class="accordion-button collapsed bg-secondary text-white" type="button"
                                data-bs-toggle="collapse" data-bs-target="#panelsStayOpen-collapseThree"
                                aria-expanded="false" aria-controls="panelsStayOpen-collapseThree">
                                Order-quantity
                            </button>
                        </h2>
                        <div id="panelsStayOpen-collapseThree" class="accordion-collapse collapse"
                            aria-labelledby="panelsStayOpen-headingThree">
                            <div class="body border border-2 border-success p-1">
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
                    <!-- ---------Chat Page---------- -->
                    <div class="mt-3">
                        <div class="d-flex align-items-center">
                            <div class="border p-2 pb-3 bg-warning w-100" data-bs-toggle="collapse"
                                data-bs-target="#collapseExampleNew" aria-expanded="false"
                                aria-controls="collapseExampleNew">
                                Transaction History
                            </div>
                            <button type="button" class="d-flex btn btn-primary rounded-circle ms-2"
                                @click="showActionModal = !showActionModal">
                                <i class="bi bi-plus fs-3"></i>
                            </button>
                        </div>
                        <div class="collapse show" id="collapseExampleNew">
                            <div v-for="message in messages" :key="message.id" :class="message.type">
                                <div class="message mt-3 mb-2 d-flex flex-column"
                                    style="width: calc(100% - 40px) !important; margin-left:auto; margin-right: 0;">
                                    <div class="d-flex   align-items-center">
                                        <i class="bi bi-person fs-4 border rounded-circle me-2"
                                            style="padding: 5px 10px !important;"></i>
                                        <div class="message-content border w-100 bg-primary"
                                            style="word-wrap: break-word; padding: 10px !important; border-radius: 8px; border-top-right-radius: 15px; border-bottom-left-radius: 15px; border-bottom-right-radius: 0px !important; color: white;">
                                            <p class="m0">
                                                <strong>{{ message.title }}</strong>: {{ message.text }}
                                            </p>
                                        </div>
                                    </div>
                                    <div class="text-end text-muted " style="font-size: 10px;">{{ message.timestamp2 }},
                                        {{ message.timestamp }}</div>
                                </div>
                            </div>
                        </div>
                    </div>
                    <div v-if="showActionModal" class="modal fade show d-block" tabindex="-1"
                        aria-labelledby="exampleModalLabel" aria-hidden="false">
                        <div class="modal-dialog ">
                            <div class="modal-content">
                                <div class="modal-header">
                                    <h5 class="modal-title" id="exampleModalLabel">Action</h5>
                                    <button type="button" class="btn" aria-label="Close"
                                        @click="showActionModal = !showActionModal">
                                        <i class="bi bi-x fs-3"></i>
                                    </button>
                                </div>
                                <div class="modal-body">
                                    <div class="form-check border-bottom py-2" v-for="(action_name, index) in inputList"
                                        :key="index">
                                        <input class="form-check-input" :ID="'radio' + index" type="radio"
                                            :value="action_name" v-model="actionName">
                                        <label class="form-check-label w-100" :for="'radio' + index">
                                            <span class="text-capitalize">{{ action_name }}</span>
                                        </label>
                                    </div>

                                    <!-- <div class="form-floating mb-3">
                                            <input type="text" class="form-control" placeholder="name@example.com"
                                                v-model="actionValue">
                                            <label for="floatingInput">Action Value</label>
                                        </div> -->
                                    <div class=" d-flex bg-light p-2 align-items-center">
                                        <input v-model="actionValue" type="text" class="form-control"
                                            placeholder="Type your message..." />
                                        <div @click="sendMessage" class="ms-2 "><i
                                                class="bi bi-telegram fs-1 text-primary p-3"></i></div>
                                    </div>
                                    <!-- <button @click="sendMessage" class="btn btn-outline-secondary w-100"
                                            type="button">Send</button> -->
                                </div>
                            </div>
                        </div>
                    </div>
                    <!-- ---------Chat Page---------- -->
                    <h4 class="text-center mt-5 my-3">Production Detail</h4>
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
                                    <div class="input-group mb-3 w-100">
                                        <span class="input-group-text w-75" id="basic-addon1">Order Quantity</span>
                                        <input style="background-color: #f8f9fa;" type="number" readonly value="1000"
                                            class="form-control w-25" aria-describedby="basic-addon1">
                                    </div>
                                    <div class="input-group mb-3 w-100">
                                        <span class="input-group-text w-75" id="basic-addon1">Available Quantity</span>
                                        <input style="background-color: #f8f9fa;" type="number" readonly value="500"
                                            class="form-control w-25" aria-describedby="basic-addon1">
                                    </div>
                                    <select class="form-select my-3" aria-label="Default select example">
                                        <option selected>Select Assignee</option>
                                        <option value="1">Assignee 1</option>
                                        <option value="2">Assignee 2</option>
                                        <option value="3">Assignee 3</option>
                                        <option value="4">Assignee 4</option>
                                        <option value="5">Assignee 5</option>
                                        <option value="6">Assignee 6</option>
                                        <option value="1">Assignee 7</option>
                                        <option value="2">Assignee 8</option>
                                        <option value="3">Assignee 9</option>
                                        <option value="4">Assignee 10</option>
                                        <option value="5">Assignee 11</option>
                                        <option value="6">Assignee 12</option>
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
                        </div>
                    </div>
                    <div class="accordion-item mt-3">
                        <h2 class="accordion-header" id="panelsStayOpen-headingThree">
                            <button class="accordion-button collapsed bg-success text-white " type="button"
                                data-bs-toggle="collapse" data-bs-target="#allotment-collection" aria-expanded="false"
                                aria-controls="allotment-collection">
                                Order Collection
                            </button>
                        </h2>
                        <div id="allotment-collection" class="accordion-collapse collapse"
                            aria-labelledby="panelsStayOpen-headingThree">
                            <div class="body border border-2 border-success p-1 ">
                                <div class="container mt-4">
                                    <select class="form-select my-3" aria-label="Default select example">
                                        <option selected>Select Assignee</option>
                                        <option value="1">Assignee 1</option>
                                        <option value="2">Assignee 2</option>
                                        <option value="3">Assignee 3</option>
                                        <option value="4">Assignee 4</option>
                                        <option value="5">Assignee 5</option>
                                        <option value="6">Assignee 6</option>
                                        <option value="1">Assignee 7</option>
                                        <option value="2">Assignee 8</option>
                                        <option value="3">Assignee 9</option>
                                        <option value="4">Assignee 10</option>
                                        <option value="5">Assignee 11</option>
                                        <option value="6">Assignee 12</option>
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
                    <div class="accordion-item mt-3">
                        <h2 class="accordion-header" id="panelsStayOpen-headingThree">
                            <button class="accordion-button collapsed bg-warning" type="button" data-bs-toggle="collapse"
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
                                                <th class="py-3" scope="col">Recv.</th>
                                                <th class="py-3" scope="col">Date</th>
                                                <th class="py-3" scope="col">Loss</th>
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
                                                <td>3000</td>
                                                <td>12/07</td>
                                                <td>8000</td>
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
                                                <td>3000</td>
                                                <td>02/08</td>
                                                <td>2000</td>
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
                                                <td>04/08</td>
                                                <td>1000</td>
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
                                                <td>08/08</td>
                                                <td>3000</td>
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
                                                <td>12/08</td>
                                                <td>3000</td>
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
                                                <td>13/08</td>
                                                <td>1000</td>
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
    props: ['manager'],
    data() {
        return {
            publicPath: process.env.BASE_URL,
            inputData: "",
            actionName: [],
            actionValue: '',
            showActionModal: false,
            inputList: ["Balance", "Ready", "Send", "Dispatched", "Received", "Message"],
            displayData: "",
            messages: [],
            availableQuantity: 800,
            collectedQuantity: 0,
            selectedDate: '',
            selectedTime: '',
        };
    },
    computed: {
        activeManager() {
            return this.$store.getters.getActiveManager
        }
    },
    methods: {
        showManager(manager) {
            return this.$store.dispatch('selectManager', manager);
        },
        hideManager() {
            return this.$store.dispatch('hideManager');
        },
        sendMessage() {
            if (this.actionValue.trim() !== '') {
                const message = {
                    id: Date.now(),
                    text: this.actionValue,
                    // title: this.actionName [0],
                    title: this.actionName,
                    timestamp: new Date().toLocaleDateString('en-US', { day: 'numeric', month: 'long' }),
                    timestamp2: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' }),
                    type: 'outgoing', // Change to 'incoming' for received messages
                };
                this.messages.push(message);
                // Clear the input value for the specific action
                this.actionName = [];
                this.actionValue = '';
                this.showActionModal = false;
            }
        },
        balanceQuantity() {
            return this.availableQuantity - this.collectedQuantity;
        },

    },
    mounted() {
        // Set the current date and time as the default values
        const now = new Date();
        this.selectedDate = now.toISOString().slice(0, 10);
        this.selectedTime = now.toTimeString().slice(0, 5);
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