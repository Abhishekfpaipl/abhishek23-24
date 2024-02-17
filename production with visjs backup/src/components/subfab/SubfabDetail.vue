<template>
    <div>
        <div class="pt-0 px-0 pb-5">

            <!-- ----------Top-----------------  -->
            <div class="container p-2 border-bottom "
                style="background-color: #e8e8e8; position: sticky; top: 0; z-index: 999;">
                <div class="d-flex justify-content-between">
                    <div class="d-flex">
                        <img :src="`${publicPath}${subfab.img}`" class="rounded-circle"
                            style="height:60px;width:60px; object-fit: fill;">
                        <div class="ms-3">
                            <p class="m-0 fw-bold" style="font-size: 1.2rem;">#{{ subfab.style }}</p>
                            <p class="m-0">Order Qty : {{ subfab.costing }}</p>
                        </div>
                    </div>
                    <div class="d-flex">
                        <RouterLink to="/subfab">
                            <button type="button" class="btn">
                                <i class="bi bi-x fs-4"></i>
                            </button>
                        </RouterLink>
                    </div>

                </div>

            </div>
            <!-- ----------Top-----------------  -->

            <h4 class="text-center mb-3 mt-4">Production Order Details</h4>

            <!-- ----------ManageReceipts--------------- -->
            <div class="container mt-4">
                <!-- <p class="text-white px-2 py-3 rounded-top" data-bs-toggle="collapse" data-bs-target="#OrderReceipts"
                    aria-expanded="false" aria-controls="OrderReceipts" style="background-color: #28CC9E;">Manage Orders
                </p> -->
                <div>
                    <!-- <div class="collapse show" id="OrderReceipts"> -->
                    <div class="d-flex justify-content-between mt-2 py-1 text-white py-3 rounded-top"
                        style="background-color: #28CC9E;">

                        <div class="mx-2 d-flex justify-content-center">
                            Catlg.
                        </div>

                        <div class="mx-2 text-center">
                            Issue
                        </div>

                        <div class="mx-2 text-center">
                            Recv.
                        </div>

                        <div class="text-center  mx-2">
                            Lost
                        </div>

                        <div class="mx-2 text-center">
                            Balance
                        </div>


                    </div>
                    <div class="d-flex flex-column">
                        <!-- <SubIssuedJob :index="index" :issues="issues"></SubIssuedJob> -->
                        <div class="d-flex justify-content-between align-items-center  py-2 bg-light">

                            <div data-bs-toggle="collapse" :data-bs-target="'#detail'" aria-expanded="false"
                                :aria-controls="'detail'" class="mx-2 d-flex justify-content-center">
                                <img :src="`${publicPath}${subfab.img}`" class="rounded-circle "
                                    style="width: 45px; height: 45px; object-fit: cover;" alt="">
                            </div>

                            <div class="mx-2 text-center">
                                <span class="d-block"> 9000 </span>
                                <span class="smaller ">
                                    jul 19
                                </span>
                            </div>

                            <div class="mx-2 text-center">
                                <span class="d-block"> 8000 </span>
                                <span class="smaller ">
                                    jul 19
                                </span>
                            </div>

                            <div class="text-center  mx-2">
                                <span class="d-block">100</span>
                                <span class="smaller">
                                    jul 21
                                </span>

                            </div>

                            <button class="btn btn-outline-secondary px-2 mx-2" data-bs-toggle="collapse"
                                :data-bs-target="'#collapseJob'" aria-expanded="false" :aria-controls="'collapseJob'">
                                900<span class="smaller d-block">Balance</span>
                            </button>

                        </div>
                        <div class="collapse show" id="collapseJob">

                            <div class="mt-2 mx-4">
                                <table class="table table-light table-striped border">
                                    <thead>
                                        <tr class="text-center">
                                            <th scope="col">Recv.</th>
                                            <th scope="col">Lost</th>
                                            <th scope="col">Settle</th>
                                            <th scope="col">Date</th>
                                            <th scope="col">Bal.</th>
                                        </tr>
                                    </thead>
                                    <tbody>
                                        <tr class="text-center">
                                            <td>1000</td>
                                            <td>0</td>
                                            <td>1000</td>
                                            <td>jul 21</td>
                                            <td>8000</td>
                                        </tr>
                                        <tr class="text-center">
                                            <td>3000</td>
                                            <td>100</td>
                                            <td>3100</td>
                                            <td>jul 21</td>
                                            <td>4900</td>
                                        </tr>
                                        <tr class="text-center">
                                            <td>4000</td>
                                            <td>0</td>
                                            <td>4000</td>
                                            <td>jul 21</td>
                                            <td>900</td>
                                        </tr>
                                    </tbody>
                                </table>

                            </div>
                        </div>
                        <!-- ---------detail------------/ -->

                        <div class="collapse container" id="detail">
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

                            <!-- ---------detail------------/ -->
                        </div>


                    </div>
                </div>

            </div>
            <!-- ----------ManageReceipts--------------- -->


            <!-- ---------Completed job------------/ -->
            <!-- <div class="container mt-4">
                <p class="text-white px-2 py-3 rounded-top  " data-bs-toggle="collapse" data-bs-target="#ProdStatus"
                    aria-expanded="false" aria-controls="ProdStatus" style="background-color: #28CC9E;">Completed Orders
                </p>
                <div class="overflow-x-scroll collapse " id="ProdStatus">
                    <table class="table table-responsive table-striped table-hover ">
                        <thead>
                            <tr style="font-size: 13px;">
                                <th class="py-3 text-center" scope="col">Order Id</th>
                                <th class="py-3 text-center" scope="col">Issued</th>
                                <th class="py-3 text-center" scope="col">Received</th>
                                <th class="py-3 text-center" scope="col">Lost</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="(item, index) in items" :key="index">
                                <td class="text-center">
                                    78695
                                </td>
                                <td class="text-center">{{ item.issue }} <p class=" m-0 " style="font-size: 10px;">
                                        {{ item.issueDate }}</p>
                                </td>
                                <td class="text-center">{{ item.recv }} <p class=" m-0" style="font-size: 10px;">
                                        {{ item.recvDate }}</p>
                                </td>
                                <td class="text-center">{{ item.loss }} <p class=" m-0" style="font-size: 10px;">
                                        {{ item.lossDate }}</p>
                                </td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div> -->
            <!-- ---------Completed job------------/ -->

            <h4 class="text-center mb-3 mt-4">Labour Details</h4>

            <!-- ---------New Jobs------------/ -->
            <div class="container mt-4" v-if="!showCompletedJobs">
                <p class="text-white px-2 py-3 rounded-top" data-bs-toggle="collapse" data-bs-target="#Newjobs"
                    aria-expanded="false" aria-controls="Newjobs" style="background-color: #28CC9E;">New Jobs</p>

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
                        <div class="d-flex w-100 my-3 gap-2">
                            <div class="form-floating mb-3 ">
                                <input type="number" class="form-control" id="floatingInput" placeholder="Catalog Quantity">
                                <label for="floatingInput">Issued Quantity</label>
                            </div>
                            <div class="form-floating mb-3 ">
                                <input type="number" class="form-control" id="floatingInput" placeholder="Catalog Rate">
                                <label for="floatingInput">Rate</label>
                            </div>
                        </div>
                        <!-- <div class="d-flex w-100 my-3">
                            <div class="mb-2 mx-2 w-50">
                                <label for="date" class="form-label ms-1">Expected Date</label>
                                <input type="date" class="form-control" id="date" v-model="selectedDate">
                            </div>
                            <div class="mb-2  mx-2 w-50">
                                <label for="time" class="form-label ms-1">Expected Time</label>
                                <input type="time" class="form-control" id="time" v-model="selectedTime">
                            </div>
                        </div> -->
                        <div class="d-flex justify-content-center mb-3">
                            <button class="btn btn-primary">Submit</button>
                        </div>
                    </div>
                </div>
            </div>
            <!-- ---------New Jobs------------/ -->

            <!-- ----------Running Jobs--------------- -->
            <div class="container mt-4" v-if="!showCompletedJobs">
                <p class="text-white px-2 py-3 rounded-top" data-bs-toggle="collapse" data-bs-target="#runningJob"
                    aria-expanded="false" aria-controls="runningJob" style="background-color: #28CC9E;">Running Jobs</p>

                <div class="collapse" id="runningJob">
                    <div class="d-flex justify-content-between mt-2 py-1 fw-bold">

                        <div class="mx-2 d-flex justify-content-center">
                            Inchrg
                        </div>

                        <div class="mx-2 text-center">
                            Issued
                        </div>

                        <div class="text-center  mx-2">
                            Recv.
                        </div>

                        <div class="mx-2 text-center">
                            Lost
                        </div>


                        <div class="mx-2 text-center">
                            Balance
                        </div>


                    </div>
                    <div class="d-flex flex-column" v-for="(issue, index) in issues" :key="index">
                        <IssuedJob :index="index" :issue="issue"></IssuedJob>
                    </div>
                </div>
            </div>
            <!-- ----------Running Jobs--------------- -->


            <!-- -----------Completed JObs ------------------  -->
            <div class="container mt-4">
                <p class="text-white px-2 py-3 rounded-top  " data-bs-toggle="collapse" data-bs-target="#Cjobs"
                    aria-expanded="false" aria-controls="Cjobs" style="background-color: #28CC9E;">Completed Jobs
                </p>

                <div class="overflow-x-scroll collapse " id="Cjobs">
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
            <!-- -----------Completed JObs ------------------  -->
            <div class="d-flex  justify-content-center container mt-4">
                <button class="btn btn-danger p-2" :disabled="btnDisable" @click="btnCompleted" data-bs-toggle="collapse"
                    data-bs-target="#Cjobs " aria-expanded="false" aria-controls="Cjobs">Completed Order</button>
                <!-- <button class="btn btn-danger p-2" :disabled="btnDisable"
                    @click="showCompletedJobs = !showCompletedJobs" data-bs-toggle="collapse" data-bs-target="#Cjobs "
                    aria-expanded="false" aria-controls="Cjobs">Completed Order</button> -->
            </div>
        </div>
    </div>
</template>

<script>
import IssuedJob from '../production manager/IssuedJob.vue';
// import SubIssuedJob from '../subfab/SubIssuedJob.vue';
export default {
    components: { IssuedJob, },
    data() {
        return {
            publicPath: process.env.BASE_URL,
            quantities: [],
            items: [
                {
                    img: "http://dillisix.com/storage/83/IMG20230404151417.jpg",
                    oid: "A1",
                    id: "01",
                    issue: "9000",
                    issueDate: "09/07",
                    due: "3000",
                    dueDate: "12/07",
                    recv: "8900",
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
            ],
            received: {
                collect: null,
                loss: 0,
                date: null,
            },
            showCompletedJobs: false,
            btnDisable: false,
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
        issuess() {
            return this.$store.getters.getIssuess;
        },
        skuCount() {
            return this.subfab.colors.length * this.subfab.sizes.length;
        },
        calculateQty() {
            return (sizeIndex) => {
                let qtyTotal = 0;
                for (let colorIndex = 0; colorIndex < this.subfab.colors.length; colorIndex++) {
                    const quantity = this.quantities[colorIndex][sizeIndex] || 0;
                    qtyTotal += parseInt(quantity);
                }
                return qtyTotal;
            };
        },
        calculateTotalQty() {
            let totalQty = 0;
            for (let colorIndex = 0; colorIndex < this.subfab.colors.length; colorIndex++) {
                for (let sizeIndex = 0; sizeIndex < this.subfab.sizes.length; sizeIndex++) {
                    const quantity = this.quantities[colorIndex][sizeIndex];
                    if (quantity) {
                        totalQty += parseInt(quantity);
                    }
                }
            }
            return totalQty;
        },


    },
    methods: {
        btnCompleted() {
            this.showCompletedJobs = !this.showCompletedJobs;
            this.btnDisable = true; // Disable the button
        },
        balanceQuantity() {
            return this.availableQuantity - (this.collectedQuantity + this.lossQuantity);
        },
        lostQuantity(issues) {
            if (issues.jobs.length > 0) {
                return issues.jobs.reduce((accumulator, job) => accumulator + job.loss, 0);
            } else {
                return 0;
            }
        },
        receivedQuantity(issues) {
            return this.collectedQuantity(issues) + this.lostQuantity(issues);
        },
        balanceQty(issues) {
            return issues.qty - this.receivedQuantity(issues);
        },
        collectedQuantity(issues) {
            if (issues.jobs.length > 0) {
                return issues.jobs.reduce((accumulator, job) => accumulator + job.collect, 0);
            } else {
                return 0;
            }
        },
        setTodayDate() {
            const now = new Date();
            this.received.date = now.toUTCString().slice(4, 17);
            // this.received.date = now.toISOString().slice(0, 10);
        },
    },
    mounted() {
        const now = new Date();
        this.selectedDate = now.toISOString().slice(0, 10);
        this.selectedTime = now.toTimeString().slice(0, 5);
        const defaultValue = 250;
        this.quantities = Array.from({ length: this.subfab.colors.length }, () =>
            Array(this.subfab.sizes.length).fill(defaultValue)
        );

        this.setTodayDate();

    },
    created() {
        this.btnDisable = false; // Enable the button on component creation

        for (let colorIndex = 0; colorIndex < this.subfab.colors.length; colorIndex++) {
            this.quantities[colorIndex] = [];
            for (let sizeIndex = ''; sizeIndex < this.subfab.sizes.length; sizeIndex++) {
                this.quantities[colorIndex][sizeIndex] = '';
            }
        }
    },

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