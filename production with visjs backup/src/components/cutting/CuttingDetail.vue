<template>
    <div>
        <div class="pt-0 px-0 pb-5">
            <div class="container p-2 border-bottom bg-white">
                <div class="d-flex justify-content-between">
                    <div class="d-flex">
                        <img :src="`${publicPath}${subfab.img}`" class="rounded-circle"
                            style="height:60px;width:60px; object-fit: fill;">
                        <div class="d-flex flex-column ms-2" data-bs-toggle="collapse" data-bs-target="#collapseExample">
                            <b class="m-0">#{{ subfab.style }} | <span>Bal : {{ subfab.bal }}
                                </span>
                            </b>
                            <p class="m-0 text-success">{{ subfab.date }} | <span>{{ subfab.time }}
                                </span>
                            </p>
                        </div>
                    </div>
                    <div class="d-flex">
                        <button class="btn" type="button" data-bs-toggle="collapse" data-bs-target="#collapseExample"
                            aria-expanded="false" aria-controls="collapseExample">
                            <i class="bi bi-chevron-down"></i>
                        </button>
                        <RouterLink to="/subfab">
                            <button type="button" class="btn">
                                <i class="bi bi-x fs-4"></i>
                            </button>
                        </RouterLink>
                    </div>

                </div>

            </div>
            <div class="collapse" id="collapseExample">
                <img :src="`${publicPath}${subfab.img}`" style=" width: 100%;  object-fit: fill;">
                <div class="box mt-2">
                    <table class="table table-striped table-hover">
                        <tbody>
                            <tr>
                                <th scope="row">Name</th>
                                <td class="text-muted">{{ subfab.name }}</td>
                            </tr>
                            <tr>
                                <th scope="row">Sale Price</th>
                                <td class="text-muted">{{ subfab.sp }}</td>
                            </tr>
                            <tr>
                                <th scope="row">Panna</th>
                                <td class="text-muted">{{ subfab.panna }}</td>
                            </tr>
                            <tr>
                                <th scope="row">Fc / Piece</th>
                                <td class="text-muted">{{ subfab.fc }}</td>
                            </tr>
                            <tr>
                                <th scope="row">Search Tags</th>
                                <td class="text-muted">{{ subfab.stag }}</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
            <!-- ---------New Jobs------------/ -->
            <div class="container mt-4">
                <p class="text-white px-2 py-3 rounded-top" data-bs-toggle="collapse" data-bs-target="#Newjobs"
                    aria-expanded="false" aria-controls="Newjobs" style="background-color: #606C5D;">New Jobs</p>

                <div class="collapse border py-2 pt-4" id="Newjobs">
                    <div class="container">
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
                            <option v-for="(user, index) in users" :key="index" value="1">{{ user.name }}</option>
                        </select>
                        <div class="form-floating mb-3">
                            <input type="number" class="form-control" id="floatingInput" placeholder="Catalog Quantity">
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
            <!-- ---------New Jobs------------/ -->

            <!-- ----------Running Jobs--------------- -->
            <div class="container mt-4">
                <p class="text-white px-2 py-3 rounded-top" data-bs-toggle="collapse" data-bs-target="#runningJob"
                    aria-expanded="false" aria-controls="runningJob" style="background-color: #606C5D;">Running Jobs</p>

                <div class="collapse" id="runningJob">
                    <div class="d-flex justify-content-between mt-2 py-1 fw-bold">

                        <div class="mx-2 d-flex justify-content-center">
                            Inchrg
                        </div>

                        <div class="mx-2 text-center">
                            Issued
                        </div>

                        <div class="mx-2 text-center">
                            Lost
                        </div>

                        <div class="text-center  mx-2">
                            Bal.
                        </div>

                        <div class="mx-2 text-center">
                            Received
                        </div>


                    </div>
                    <div class="d-flex flex-column" v-for="(issue, index) in issues" :key="index">
                        <IssuedJob :index="index" :issue="issue"></IssuedJob>
                    </div>
                </div>
            </div>
            <!-- ----------Running Jobs--------------- -->


            <!-- -----------Production Status------------------  -->
            <div class="container mt-4">
                <p class="text-white px-2 py-3 rounded-top  " data-bs-toggle="collapse" data-bs-target="#ProdStatus"
                    aria-expanded="false" aria-controls="ProdStatus" style="background-color: #606C5D;">Completed Jobs
                </p>

                <div class="overflow-x-scroll collapse " id="ProdStatus">
                    <table class="table table-responsive table-striped table-hover ">
                        <thead>
                            <tr style="font-size: 13px;">
                                <th class="py-3 text-center" scope="col">Workers</th>
                                <th class="py-3 text-center" scope="col">Issue</th>
                                <th class="py-3 text-center" scope="col">Loss</th>
                                <th class="py-3 text-center" scope="col">Recv.</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="(item, index) in items" :key="index">
                                <td class="d-flex justify-content-center"><img :src="item.img" class="rounded-circle "
                                        style="width: 45px; height: 45px; object-fit: cover;" alt="">
                                </td>

                                <td class="text-center">{{ item.issue }} <p class=" m-0 " style="font-size: 10px;">{{
                                    item.issueDate }}</p>
                                </td>

                                <td class="text-center">{{ item.loss }} <p class=" m-0" style="font-size: 10px;">
                                        {{ item.lossDate }}</p>
                                </td>
                                <td class="text-center">{{ item.recv }} <p class=" m-0" style="font-size: 10px;">
                                        {{ item.recvDate }}</p>
                                </td>

                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
            <!-- -----------Production Status------------------  -->
        </div>
    </div>
</template>

<script>
import IssuedJob from '../production manager/IssuedJob.vue';
export default {
    data() {
        return {
            publicPath: process.env.BASE_URL,

            items: [
                {
                    img: "http://dillisix.com/storage/83/IMG20230404151417.jpg",
                    oid: "A1",
                    id: "01",
                    issue: "9000",
                    issueDate: "09/07",
                    due: "3000",
                    dueDate: "12/07",
                    recv: "2900",
                    recvDate: "12/07",
                    loss: "100",
                    lossDate: "12/07",
                    bal: "6000",
                    balDate: "12/07"
                },
                {
                    img: "http://dillisix.com/storage/83/IMG20230404151417.jpg",
                    oid: "A1",
                    id: "02",
                    issue: "9000",
                    issueDate: "09/07",
                    due: "3000",
                    dueDate: "12/07",
                    recv: "2900",
                    recvDate: "12/07",
                    loss: "100",
                    lossDate: "12/07",
                    bal: "6000",
                    balDate: "12/07"
                },
                {
                    img: "http://dillisix.com/storage/54/kedar.jpg",
                    oid: "B1",
                    id: "01",
                    issue: "9000",
                    issueDate: "09/07",
                    due: "3000",
                    dueDate: "12/07",
                    recv: "2900",
                    recvDate: "12/07",
                    loss: "100",
                    lossDate: "12/07",
                    bal: "6000",
                    balDate: "12/07"
                },
                {
                    img: "http://dillisix.com/storage/54/kedar.jpg",
                    oid: "B1",
                    id: "02",
                    issue: "9000",
                    issueDate: "09/07",
                    due: "3000",
                    dueDate: "12/07",
                    recv: "2900",
                    recvDate: "12/07",
                    loss: "100",
                    lossDate: "12/07",
                    bal: "6000",
                    balDate: "12/07"
                },
                {
                    img: "http://dillisix.com/storage/53/narender-profile-image.jpeg",
                    oid: "C1",
                    id: "01",
                    issue: "9000",
                    issueDate: "09/07",
                    due: "3000",
                    dueDate: "12/07",
                    recv: "2900",
                    recvDate: "12/07",
                    loss: "100",
                    lossDate: "12/07",
                    bal: "6000",
                    balDate: "12/07"
                },
                {
                    img: "http://dillisix.com/storage/53/narender-profile-image.jpeg",
                    oid: "C1",
                    id: "02",
                    issue: "9000",
                    issueDate: "09/07",
                    due: "3000",
                    dueDate: "12/07",
                    recv: "2900",
                    recvDate: "12/07",
                    loss: "100",
                    lossDate: "12/07",
                    bal: "6000",
                    balDate: "12/07"
                },
            ]
        };
    },
    computed: {
        users() {
            return this.$store.getters.getUsers;
        },
        subfab() {
            let subfabId = this.$route.params.subfabId;
            return this.$store.getters.getSubfab(subfabId);
        },
        issues() {
            return this.$store.getters.getIssues;
        },


    },
    methods: {
        balanceQuantity() {
            return this.availableQuantity - (this.collectedQuantity + this.lossQuantity);
        },
    },
    components: { IssuedJob }
}
</script>

<style scoped>
table th:nth-child(1),
.table td:nth-child(1) {
    position: sticky;
    left: 0;
    background-color: #f8f8f7;
    color: #373737;
    z-index: 10;
}

table th:nth-child(7),
.table td:nth-child(7) {
    position: sticky;
    right: 0;
    background-color: #f8f8f7;
    color: #373737;
    z-index: 10;
}

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