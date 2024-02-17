<template>
    <div>
        <button @click="showManager(manager)" class="btn btn-warning" type="button"
            aria-controls="offcanvasRight">Manage</button>

        <div v-if="Object.keys(activeManager).length !== 0" class="offcanvas offcanvas-end show " tabindex="-1"
            id="offcanvasRight" aria-labelledby="offcanvasRightLabel">
            <div class="offcanvas-body pt-0 px-0" style="background-color: #e8e8e8;">
                <div class="container p-2 border-bottom bg-white" style="box-shadow: rgba(67, 71, 85, 0.27) 0px 0px 0.25em, rgba(90, 125, 188, 0.05) 0px 0.25em 1em;">
                    <div class="d-flex justify-content-between ">
                        <div class="d-flex align-items-center ">
                            <img :src="`${publicPath}${activeManager.img}`" class="rounded-circle"
                            style="height:60px;width:60px; object-fit: fill;">
                        <div class="d-flex flex-column ms-2" data-bs-toggle="collapse" data-bs-target="#collapseExample">
                            <b class="m-0" style="font-size: 1.2rem;">#{{ activeManager.style }} | <span>Bal : {{ activeManager.bal }}
                                </span>
                            </b>
                            <p class="m-0 text-success" style="font-size: .8rem;">{{ activeManager.date }} | <span>{{ activeManager.time }}
                                </span>
                            </p>
                        </div>
                        </div>
                        <div class="d-flex align-items-center ">
                            <button class="btn" type="button" data-bs-toggle="collapse" data-bs-target="#collapseExample"
                            aria-expanded="false" aria-controls="collapseExample">
                            <i class="bi bi-chevron-down"></i>
                        </button>
                        <button type="button" class="btn" @click="hideManager()">
                            <i class="bi bi-x fs-4"></i>
                        </button>
                        </div>

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
                    <!-- ---------Chat Page---------- -->
                   <div style="box-shadow: rgba(67, 71, 85, 0.27) 0px 0px 0.25em, rgba(90, 125, 188, 0.05) 0px 0.25em 1em;">
                    <div class="mt-3">
                        <div class="d-flex align-items-center">
                            <div class="border p-2 py-3 ps-4  text-white w-100" style="background-color: #606C5D;" data-bs-toggle="collapse"
                                data-bs-target="#collapseExampleNew" aria-expanded="false"
                                aria-controls="collapseExampleNew">
                                Order Management
                            </div>
                            <!-- <button type="button" class="d-flex btn btn-primary rounded-circle ms-2"
                                @click="showActionModal = !showActionModal">
                                <i class="bi bi-plus fs-3"></i>
                            </button> -->
                        </div>
                        <div class="collapse show bg-white p-2" id="collapseExampleNew">
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
                    <div class="border bg-white">
                        <!-- <p class="text-center text-white py-2" style="background-color: #606C5D;">Order Management</p> -->
                        <div class="container pb-2 ">
                            <div class="form-check border-bottom py-2 " v-for="(action_name, index) in inputList"
                                :key="index">
                               <div class="d-flex align-items-center ">
                                <input class="form-check-input" :ID="'radio' + index" type="radio" :value="action_name"
                                    v-model="actionName">
                                <label class="form-check-label w-100" :for="'radio' + index">
                                    <span><i :class="action_name.icon" class="fs-4 mx-3"></i></span>
                                    <span class="text-capitalize">{{ action_name.title }}</span>
                                </label>
                               </div>
                            </div>

                            <div class=" d-flex bg-light p-2 align-items-center">
                                <input v-model="actionValue" type="text" class="form-control"
                                    placeholder="Type your message..." />
                                <div @click="sendMessage" class="ms-2 "><i class="bi bi-telegram fs-1 text-primary p-3"></i>
                                </div>
                            </div>
                        </div>
                    </div> 
                   </div>
                    <!-- <div v-if="showActionModal" class="modal fade show d-block" tabindex="-1"
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
 
                                    <div class=" d-flex bg-light p-2 align-items-center">
                                        <input v-model="actionValue" type="text" class="form-control"
                                            placeholder="Type your message..." />
                                        <div @click="sendMessage" class="ms-2 "><i
                                                class="bi bi-telegram fs-1 text-primary p-3"></i></div>
                                    </div>
                                    
                                </div>
                            </div>
                        </div>
                    </div> -->
                    <!-- ---------Chat Page---------- -->


                    <div class="accordion-item mt-3">
                        <h2 class="accordion-header" id="headingTwo">
                            <button class="accordion-button collapsed" type="button"
                                data-bs-toggle="collapse" data-bs-target="#collapseTwo" aria-expanded="false"
                                style="box-shadow: rgba(67, 71, 85, 0.27) 0px 0px 0.25em, rgba(90, 125, 188, 0.05) 0px 0.25em 1em;"
                                aria-controls="collapseTwo">
                                Progress Stage
                            </button>
                        </h2>
                        <div id="collapseTwo" class="accordion-collapse collapse" aria-labelledby="headingTwo"
                            data-bs-parent="#accordionExample">
                            <div class="body border border-2 border-secondary" style="background-color: #e8e8e8;">
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
                            <button class="accordion-button collapsed " type="button"
                                data-bs-toggle="collapse" data-bs-target="#panelsStayOpen-collapseThree"
                                style="box-shadow: rgba(67, 71, 85, 0.27) 0px 0px 0.25em, rgba(90, 125, 188, 0.05) 0px 0.25em 1em;"
                                aria-expanded="false" aria-controls="panelsStayOpen-collapseThree">
                                Order-quantity
                            </button>
                        </h2>
                        <div id="panelsStayOpen-collapseThree" class="accordion-collapse collapse"
                            aria-labelledby="panelsStayOpen-headingThree">
                            <div class="body border border-2 border-secondary p-1">
                                <div class="border">
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
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class="accordion-item mt-3">
                        <h2 class="accordion-header" id="panelsStayOpen-headingThree">
                            <button class="accordion-button collapsed" type="button"
                                data-bs-toggle="collapse" data-bs-target="#Status" aria-expanded="false"
                                style="box-shadow: rgba(67, 71, 85, 0.27) 0px 0px 0.25em, rgba(90, 125, 188, 0.05) 0px 0.25em 1em;"
                                aria-controls="Status">
                                Order-Status
                            </button>
                        </h2>
                        <div id="Status" class="accordion-collapse collapse" aria-labelledby="panelsStayOpen-headingThree">
                            <div class="body border border-2 border-secondary p-1">
                                <div class="overflow-x-scroll">
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

                    <h4 class="text-center mt-5 my-3">Production Detail</h4>

                    <!-- -----------Nav-Tabs------------- -->
                    <div class="bg-white rounded"
                        style="box-shadow: rgba(67, 71, 85, 0.27) 0px 0px 0.25em, rgba(90, 125, 188, 0.05) 0px 0.25em 1em;">
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
                            <div class="tab-pane fade bg-white py-2" id="nav-collection" role="tabpanel"
                                aria-labelledby="nav-collection-tab">
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
                    <!-- -----------Nav-Tabs------------- -->

                    <div class="accordion-item my-3">
                        <h2 class="accordion-header" id="panelsStayOpen-Status">
                            <button class="accordion-button collapsed " data-bs-toggle="collapse"
                                data-bs-target="#production-status" aria-expanded="false"
                                style="box-shadow: rgba(67, 71, 85, 0.27) 0px 0px 0.25em, rgba(90, 125, 188, 0.05) 0px 0.25em 1em;"
                                aria-controls="production-status">
                                Production Status
                            </button>
                        </h2>
                        <div id="production-status" class="accordion-collapse collapse"
                            aria-labelledby="panelsStayOpen-Status">
                            <div class="body border border-2 border-secondary p-1">
                                <div class=" overflow-x-scroll">
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
            // inputList: ["Balance", "Ready", "Send", "Dispatched", "Received", "Message"],
            inputList: [
                {
                    title:'Balance Quantity',
                    icon:'bi bi-pause-btn'
                },
                {
                    title:'Ready Quantity',
                    icon:'bi bi-check2'
                },
                {
                    title:'Sending Request',
                    icon:'bi bi-envelope'
                },
                {
                    title:'Dispatched Quantity',
                    icon:'bi bi-truck'
                },
                {
                    title:'Received Quantity',
                    icon:'bi bi-check2-all'
                },
                {
                    title:'Chat Message',
                    icon:'bi bi-chat-dots'
                },
                 
            ],
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
                    title: this.actionName.title,
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
.nav-link.active {
    color: #fff;
    background-color: #606C5D;
}

.nav-link {
    color: #000000;
}
</style>