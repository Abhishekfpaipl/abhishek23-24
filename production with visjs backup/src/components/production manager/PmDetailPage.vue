<template>
    <div class="pb-5">
        <!-- ----------Top-----------------  -->
        <div class="pt-0 px-0" style="background-color: #e8e8e8; position: sticky; top: 0; z-index:10;">
            <div class="container p-2 border-bottom ">
                <div class="d-flex justify-content-between ">
                    <div class="d-flex align-items-center justify-content-center">
                        <i class="bi bi-arrow-left fs-4" @click="goBack()"></i>
                    </div>

                    <div class="d-flex align-items-center ">
                        <img :src="`${publicPath}${manager.img}`" class="rounded-circle"
                            style="height:60px;width:60px; object-fit: fill;">
                        <div class="ms-3">
                            <p class="m-0 fw-bold" style="font-size: 1.2rem;">{{ manager.style }}</p>
                            <p class="m-0">Order Qty : {{ manager.costing }}</p>
                            <p class="m-0">Sub Order Id : {{ manager.subOrderId }}</p>
                        </div>
                    </div>
                    <div class="d-flex align-items-center ">
                        <button type="button" class="btn" data-bs-toggle="collapse" data-bs-target="#detail"
                            aria-expanded="false" aria-controls="detail">
                            <i class="bi bi-chevron-down fs-4"></i>
                        </button>
                    </div>
                </div>

            </div>
        </div>
        <!-- ----------Top-----------------  -->

        <!-- ----------Detail-----------------  -->
        <div class="container" v-if="!show">
            <div class="collapse container" id="detail">
                <img :src="`${publicPath}${manager.img}`" style=" width: 100%;  object-fit: fill;">
                <div class="box mt-2">
                    <table class="table table-striped table-hover ">
                        <tbody>
                            <tr>
                                <th scope="row">Name</th>
                                <td class="text-muted">{{ manager.name }}</td>
                            </tr>
                            <tr>
                                <th scope="row">Fc / Piece</th>
                                <td class="text-muted">{{ manager.fc }} Grm</td>
                            </tr>
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

        <FabricProcurement :manager="manager" @parent-data="onTotalCalculated"></FabricProcurement>

        <!-- Fabric Procurement -->

        <div class="container mt-4">
            <ul class="nav nav-tabs d-flex justify-content-between">
                <li class="nav-item w-25 text-center">
                    <a class="nav-link active" id="tab1" data-bs-toggle="tab" href="#content1">Allotment</a>
                </li>
                <li class="nav-item w-25 text-center">
                    <a class="nav-link " id="tab2" data-bs-toggle="tab" href="#content2">Finishing</a>
                </li>
                <!--  <li class="nav-item w-25 text-center">
                    <a class="nav-link " id="tab1" data-bs-toggle="tab" href="#content3">Trims</a>
                </li>
                <li class="nav-item w-25 text-center">
                    <a class="nav-link " id="tab2" data-bs-toggle="tab" href="#content4">Buttons</a>
                </li> -->
            </ul>

            <div class="tab-content mt-2">
                <div class="tab-pane fade show active" id="content1">
                    <!-- ---------New Jobs------------/ -->
                    <div class="container mt-4">
                        <div class="px-2 py-3">
                            <form @submit.prevent="addJob()" class="row g-3">

                                <input v-model="newJob.content" type="hidden" required>
                                <input v-model="newJob.fcpu" type="hidden" required>
                                <input v-model="newJob.ptpuim" type="hidden" required>

                                <div class="col-md-4">
                                    <label for="jobFabric" class="form-label">Choose Fabric / Material</label>
                                    <select v-model="newJob.allotedFabric" class="form-select" id="jobFabric">
                                        <option v-for="(fabric, index) in manager.fabrics" :key="index" :value="fabric.id">
                                            {{ fabric.name }}
                                        </option>
                                    </select>
                                </div>
                                <div class="col-md-4">
                                    <label for="jobFabric" class="form-label">Fabric Allotment</label>
                                    <input v-model="newJob.fabric" type="text" class="form-control" id="jobFabric" required>
                                    <small>Available Fabric {{ totalFromChild }} mtr</small>
                                </div>
                                <div v-if="showStartDateInput" class="col-md-4">
                                    <label for="jobGroup" class="form-label">Station</label>
                                    <select v-model="newJob.group" class="form-select" id="jobGroup">
                                        <option v-for="(station, index) in stations" :key="index" :value="station.id">
                                            {{ station.content }}
                                        </option>
                                    </select>
                                    <small>Prefered Station</small>
                                </div>

                                <div v-if="hideDepartmentInput" class="col-md-4">
                                    <label for="jobDept" class="form-label">Department</label>
                                    <select v-model="newJob.dept" class="form-select" id="jobDept">
                                        <option v-for="(dept, index) in department" :key="index" :value="dept.id">
                                            {{ dept.name }}
                                        </option>
                                    </select>
                                    <small>Prefered Department</small>
                                </div>

                                <div v-if="showStartDateInput" class="col-md-4">
                                    <label for="jobStart" class="form-label">Start Date</label>
                                    <input v-model="newJob.start" type="datetime-local" class="form-control" id="jobStart">
                                    <small>Available Slot</small>
                                </div>

                                <div class="col-12">
                                    <button type="submit" class="btn btn-primary">Create Job</button>
                                </div>
                            </form>
                        </div>
                    </div>
                    <!-- ----------New Jobs-----------/ -->
                </div>

                <div class="tab-pane fade" id="content2">
                    <form @submit.prevent="submitFinishing()" class="row g-3">
                        <table class="table table-responsive">
                            <thead>
                                <tr>
                                    <th scope="col">
                                        <div class="d-flex flex-column align-items-center">
                                            <p class="m-0">{{ skuCount }}</p>
                                            <p class="m-0" style="font-size: 12px;">SKU</p>
                                        </div>
                                    </th>
                                    <th scope="col" class="text-center" v-for="(size, index) in manager.sizes" :key="index">
                                        <div class="fw-bold">
                                            <p class="">{{ size.name }}</p>
                                        </div>
                                    </th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(color, colorIndex) in manager.colors" :key="colorIndex">
                                    <td>
                                        <div class="rounded px-1 align-items-center justify-content-center d-flex"
                                            style="width: 36px; height: 36px;" :style="'background-color :' + color.bg">
                                        </div>
                                    </td>
                                    <td v-for="(size, sizeIndex) in manager.sizes" :key="sizeIndex">
                                        <input type="number" class="form-control text-center"
                                            v-model="quantities[`${color.id}_${size.id}`]">
                                    </td>
                                </tr>
                                <tr scope="row">
                                    <th>Qty</th>
                                    <td class="text-center" v-for="(size, sizeindex) in  manager.sizes" :key="sizeindex">
                                        {{ calculateSizesTotal(sizeindex) }}
                                    </td>
                                </tr>
                            </tbody>
                        </table>

                        <p class="mb-0">Issue To Shop</p>
                        <select class="form-select my-3" aria-label="Default select example" v-model="finishingForm.issue">
                            <option selected>{{ finishingForm.issue }}</option>
                            <!-- <option v-for="(user, index) in filteredUser" :key="index" :value="user.id">{{ user.dept }} ({{
                                user.name }})</option> -->
                        </select>

                        <div class="col-12 d-flex justify-content-center">
                            <button type="submit" class="btn btn-primary">Issue</button>
                        </div>
                    </form>

                    <div class="" v-for="(job, index) in finishingHistory" :key="index">
                        <table class="table mb-0">
                            <thead>
                                <tr>
                                    <th scope="col">{{ skuCount }} <br>Sku</th>
                                    <th scope="col" v-for="(size, sizeIndex) in managerSizes" :key="sizeIndex">
                                        <p>{{ size.name }}</p>
                                    </th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="(color, colorIndex) in managerColors" :key="colorIndex">
                                    <td>
                                        <div class="rounded px-1 align-items-center justify-content-center d-flex"
                                            style="width: 36px; height: 36px;" :style="'background-color :' + color.bg">
                                        </div>
                                    </td>
                                    <td v-for="(size, sizeIndex) in managerSizes" :key="sizeIndex">
                                        {{ job.tableData[`${color.id}_${size.id}`] || 0 }}
                                    </td>
                                </tr>

                            </tbody>

                        </table>

                        <p>Isuued To : {{ job.issue }}</p>
                    </div>
                </div>
            </div>
        </div>


        <!-- Cutting TimeLine -->
        <router-link to="/visData" class="d-flex justify-content-center text-decoration-none my-2">
            <button class="btn btn-dark">Timeline</button>
        </router-link>

        <div class="container my-4 " v-for="(job, index) in filteredJobs" :key="index">
            <h2 class="text-center">Cutting Job History</h2>
            <table class="table">
                <tbody>
                    <tr>
                        <th>Catalog Id</th>
                        <td>{{ job.content }}</td>
                    </tr>
                    <tr>
                        <th>Expected Quantity</th>
                        <td>{{ job.fabric }}</td>
                    </tr>
                    <tr>
                        <th>Start Date & Time</th>
                        <td>{{ job.start }}</td>
                    </tr>
                    <tr>
                        <th>End Date & Time</th>
                        <td>{{ job.end }}</td>
                    </tr>
                    <tr>
                        <th>Station</th>
                        <td>{{ job.group }}</td>
                    </tr>
                </tbody>
            </table>
        </div>

        <!-- Cutting TimeLine -->


        <!-- InterDepartment Alloment -->
        <h4 class="text-center mb-3 mt-4">InterDepartmental Alloment</h4>

        <div class="container mt-4">
            <ManageProduction :manager="manager"></ManageProduction>
        </div>
        <!-- InterDepartment Alloment -->
        <h4 class="text-center mb-3 mt-4">Shop Order Details</h4>

        <!-- --------Po Placed-------------  -->
        <div class="container" v-if="!show">
            <div class="border p-2 py-3  text-white w-100 rounded-top" data-bs-toggle="collapse" data-bs-target="#Poplaced"
                aria-expanded="false" aria-controls="Poplaced" style="background-color: #28CC9E;">
                PO Placed
            </div>
            <div class="overflow-x-scroll bg-white collapse" id="Poplaced">
                <div class="px-2 my-2">
                    <p class="mb-0">Order Date: {{ manager.orderdate }}</p>
                    <p class="mb-0">Expected Delivery Date: {{ manager.expecteddate }}</p>
                </div>
                <table class="table table-responsive table-striped  border border-1">
                    <thead>
                        <tr>
                            <th scope="col">
                                <div class="d-flex flex-column align-items-center">
                                    <p class="m-0">{{ skuCount }}</p>
                                    <p class="m-0" style="font-size: 12px;">SKU</p>
                                </div>
                            </th>
                            <th scope="col" class="text-center" v-for="(size, index) in manager.sizes" :key="index">
                                <div class="fw-bold" style="">
                                    <p class="">{{ size.name }}</p>
                                </div>
                            </th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(color, colorIndex) in manager.colors" :key="colorIndex">
                            <td class="">
                                <div class="rounded-circle m-2 px-1 align-items-center justify-content-center d-flex"
                                    style="width: 30px; height: 30px;" :style="'background-color :' + color.bg">
                                </div>
                            </td>
                            <td v-for="(z, sizeIndex) in manager.sizes" :key="sizeIndex">
                                <input type="number" class="form-control text-center"
                                    v-model="quantities[colorIndex][sizeIndex]">

                            </td>
                        </tr>
                        <tr scope="row">
                            <th>Qty</th>
                            <td class="text-center" v-for="(size, sizeindex) in  manager.sizes" :key="sizeindex">
                                {{ calculateQty(sizeindex) }}
                            </td>
                        </tr>
                    </tbody>
                </table>
                <div class="container mb-3 ">
                    <div class=" d-flex justify-content-between mx-3 py-2 px-4 border" style="background-color: #e8e8e8;">
                        <p class=" mb-0">Actual Ordered Qty</p>
                        <p class=" fw-bold text-center mb-0">
                            {{ calculateTotalQty }} pcs
                        </p>
                    </div>
                </div>
                <div class="d-flex justify-content-center">
                    <button class="btn btn-primary">Update</button>
                </div>
            </div>

        </div>

        <h4 class="text-center mb-3 mt-4">Shop Order Management</h4>

        <!-- ---------Chat Page---------- -->
        <div class="container mt-4">
            <div>
                <div class="mt-3">
                    <div class="d-flex align-items-center">
                        <div class="border p-2 py-3  rounded-top  text-white w-100" style="background-color: #28CC9E;"
                            data-bs-toggle="collapse" data-bs-target="#collapseExampleNew" aria-expanded="false"
                            aria-controls="collapseExampleNew">
                            Order Transactions
                        </div>

                    </div>
                    <div class="collapse show bg-white p-2" id="collapseExampleNew">
                        <div v-for="message in messages" :key="message.id" :class="message.type">
                            <div class="message mt-3 mb-2 d-flex flex-column"
                                style="width: calc(100% - 40px) !important; margin-left:auto; margin-right: 0;">
                                <div class="d-flex   align-items-center">
                                    <i class="bi bi-person fs-4 border rounded-circle me-2"
                                        style="padding: 5px 10px !important;"></i>
                                    <div class="message-content border w-100 "
                                        style=" background-color: #28CC9E; word-wrap: break-word; padding: 10px !important; border-radius: 8px; border-top-right-radius: 15px; border-bottom-left-radius: 15px; border-bottom-right-radius: 0px !important; color: white;">
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
                <div class="border bg-white" v-if="isVisible">
                    <div class="container pb-2 ">
                        <div class="form-check border-bottom py-2 " v-for="(action_name, index) in inputList" :key="index">
                            <div class="d-flex align-items-center">
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
                            <div @click="sendMessage" class="ms-2 "><i class="bi bi-telegram fs-1 p-3"
                                    style="color: #28CC9E;"></i>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <!-- ---------Chat Page---------- -->

        <div class="d-flex justify-content-between container my-4 w-100">
            <div class="d-flex justify-content-center">
                <button data-bs-toggle="modal" data-bs-target="#exampleModal" class="btn btn-danger"> Shop Order
                </button>
            </div>

            <div class="d-flex justify-content-center">
                <button class="btn btn-danger" :disabled="btnDisable" @click="btnCompleted" data-bs-toggle="collapse"
                    data-bs-target="#ProdStatus" aria-expanded="false" aria-controls="ProdStatus">Production
                    Order</button>
            </div>
        </div>

        <!-- ------------Chat close Modal-----------  -->
        <div class="modal fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
            <div class="modal-dialog modal-dialog-centered">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="exampleModalLabel">Order Completed</h5>
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body text-center">
                        <p>Are you sure you have received <br> <b> Quantity of this
                                Order</b></p>
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-light border" style="width: 30%;"
                            data-bs-dismiss="modal">Close</button>
                        <button @click="hideDiv()" data-bs-dismiss="modal" style="width: 30%;" type="button"
                            class="btn btn-light border">Yes</button>
                    </div>
                </div>
            </div>
        </div>
        <!-- ------------Chat close Modal-----------  -->


    </div>
</template>

<script>
import ManageProduction from './ManageProduction.vue';
import FabricProcurement from './FabricProcurement.vue';

export default {
    data() {
        return {
            isVisible: true,
            show: false,
            btnDisable: false,
            quantities: [],
            publicPath: process.env.BASE_URL,
            inputData: "",
            actionName: [],
            actionValue: '',
            showActionModal: false,
            inputList: [
                {
                    title: 'Balance Quantity',
                    icon: 'bi bi-pause-btn'
                },
                {
                    title: 'Ready Quantity',
                    icon: 'bi bi-check2'
                },
                {
                    title: 'Sending Request',
                    icon: 'bi bi-envelope'
                },
                {
                    title: 'Dispatched Quantity',
                    icon: 'bi bi-truck'
                },
                {
                    title: 'Received Quantity',
                    icon: 'bi bi-check2-all'
                },
                {
                    title: 'Chat Message',
                    icon: 'bi bi-chat-dots'
                },

            ],
            messages: [],

            availableQuantity: 800,
            collectedQuantity: null,
            lossQuantity: null,
            selectedUserId: null,
            form: {
                qty: 0,
                rate: 0,
                ptpuim: '',
                assignee: null,
                start_date: '',
                due_date: '',
                end_date: null,
                received: {
                    collect: null,
                    loss: null,
                    date: null,
                },
                jobs: []
            },
            total: 0,
            newJob: {
                content: '',
                ptpuim: 1,
                fcpu: 1,
                fabric: '',
                allotedFabric: '',
                start: '',
                end: '',
                group: '',
                dept: ''
            },
            totalFromChild: 0,
            acceptedFabric: {
                name: ''
            },
            additionalMinutes: 30, // Additional minutes to add
            finishingForm: {
                issue: 'Shop(Amit Sardar)'
            }
        };
    },
    components: {
        ManageProduction,
        FabricProcurement
    },
    computed: {
        finishingHistory() {
            return this.$store.getters.getFinishingHistory
        },
        managerColors() {
            // Extract unique colors based on the color.id in tableData
            const colorIds = Object.keys(this.quantities)
                .map(id => id.split('_')[0])
                .filter((value, index, self) => self.indexOf(value) === index);

            return this.manager.colors.filter(color => colorIds.includes(color.id.toString()));
        },
        managerSizes() {
            // Extract unique sizes based on the size.id in tableData
            const sizeIds = Object.keys(this.quantities)
                .map(id => id.split('_')[1])
                .filter((value, index, self) => self.indexOf(value) === index);

            return this.manager.sizes.filter(size => sizeIds.includes(size.id.toString()));
        },
        showStartDateInput() {
            // Assuming 'fabric' is the currently selected fabric in your form
            return this.newJob.allotedFabric && this.manager.fabrics.find(fabric => fabric.id === this.newJob.allotedFabric).name.includes('Fabric');
        },
        hideDepartmentInput() {
            // Assuming 'fabric' is the currently selected fabric in your form
            return this.newJob.allotedFabric && !this.manager.fabrics.find(fabric => fabric.id === this.newJob.allotedFabric).name.includes('Fabric');
        },
        department() {
            return this.$store.getters.getDepartment
        },
        earliestAvailableStationId() {
            const currentTime = new Date();
            const activeJobs = this.jobs.filter(job => job.end > currentTime);

            // Create an array to store the availability of each station
            const stationAvailability = this.stations.map(station => {
                const jobsAtStation = activeJobs.filter(job => job.group === station.id);
                if (jobsAtStation.length > 0) {
                    // Find the maximum end time among jobs at this station
                    const maxEndTime = Math.max(...jobsAtStation.map(job => job.end));
                    return { stationId: station.id, end: maxEndTime };
                }
                // If no jobs at the station, set end time to now
                return { stationId: station.id, end: currentTime };
            });

            // Sort stations by end time in ascending order
            stationAvailability.sort((a, b) => a.end - b.end);

            // Find the station with the earliest available end time
            return stationAvailability[0].stationId;
        },
        jobEndForEarliestStation() {
            const earliestAvailableStationId = this.earliestAvailableStationId;
            if (earliestAvailableStationId) {
                // Find the job associated with the earliest available station
                const jobWithEarliestEnd = this.jobs.find(job => job.group === earliestAvailableStationId);

                // Return the end time of the associated job
                return jobWithEarliestEnd ? jobWithEarliestEnd.end : null;
            }
            return null;
        },
        formattedJobEnd: {
            get() {
                const jobEnd = this.jobEndForEarliestStation;
                if (jobEnd) {
                    // Create a date object from the UTC string
                    const utcDate = new Date(jobEnd);

                    // Convert UTC time to IST (Indian Standard Time)
                    const istDate = new Date(utcDate.getTime() + 330 * 60000); // 330 minutes offset for IST

                    // Add additional minutes
                    istDate.setMinutes(istDate.getMinutes() + this.additionalMinutes);

                    // Format date and time to match datetime-local format
                    const year = istDate.getUTCFullYear();
                    const month = (istDate.getUTCMonth() + 1).toString().padStart(2, '0'); // Months are zero-based
                    const day = istDate.getUTCDate().toString().padStart(2, '0');
                    const hours = istDate.getUTCHours().toString().padStart(2, '0');
                    const minutes = istDate.getUTCMinutes().toString().padStart(2, '0');

                    return `${year}-${month}-${day}T${hours}:${minutes}`;
                }
                return '';
            },
            // set(newValue) {
            //     // Handle changes to the input field if needed
            // },
        },
        stations() {
            return this.$store.getters.getStation
        },
        jobs() {
            return this.$store.getters.getStationJob
        },
        filteredJobs() {
            // Filter jobs based on manager.style
            return this.jobs.filter((job) => job.content === this.manager.style);
        },
        issues() {
            return this.$store.getters.getIssues;
        },
        item() {
            return this.$store.getters.getitem;
        },
        users() {
            return this.$store.getters.getUsers;
        },
        selectedUser() {
            return this.users.find(user => user.id === this.selectedUserId);
        },
        filteredUser() {
            return this.users.filter(user => (user.dept === 'Shop') && user.post === 'Owner');
        },
        filteredUsers() {
            return this.users.filter(user => (user.dept === 'Stiching' || user.dept === 'Fabricator') && user.post === 'Incharge');
        },
        manager() {
            let managerId = this.$route.params.managerId;
            return this.$store.getters.getManager(managerId);
        },
        skuCount() {
            return this.manager.colors.length * this.manager.sizes.length;
        },
        calculateQty() {
            return (sizeIndex) => {
                let qtyTotal = 0;
                for (let colorIndex = 0; colorIndex < this.manager.colors.length; colorIndex++) {
                    const quantity = this.quantities[colorIndex][sizeIndex] || 0;
                    qtyTotal += parseInt(quantity);
                }
                return qtyTotal;
            };
        },
        calculateSizesTotal() {
            return (sizeIndex) => {
                let qtyTotal = 0;
                for (let colorIndex = 0; colorIndex < this.manager.colors.length; colorIndex++) {
                    const quantity = this.quantities[`${this.manager.colors[colorIndex].id}_${this.manager.sizes[sizeIndex].id}`] || 0;
                    qtyTotal += parseInt(quantity);
                }
                return qtyTotal;
            };
        },
        calculateTotalQty() {
            let totalQty = 0;
            for (let colorIndex = 0; colorIndex < this.manager.colors.length; colorIndex++) {
                for (let sizeIndex = 0; sizeIndex < this.manager.sizes.length; sizeIndex++) {
                    const quantity = this.quantities[colorIndex][sizeIndex];
                    if (quantity) {
                        totalQty += parseInt(quantity);
                    }
                }
            }
            return totalQty;
        },
        fabricReq() {
            return this.manager.costing * this.manager.fc
        }

    },
    methods: {
        goBack() {
            window.history.back()
        },
        getSelectedOptionId() {
            if (this.form.assignee) {
                // Find the selected user based on the assignee's name
                const selectedUser = this.filteredUsers.find(user => user.name === this.form.assignee);
                if (selectedUser) {
                    this.selectedUserId = selectedUser.id; // Assuming there's an 'id' property in your user object
                }
            } else {
                this.selectedUserId = null;
            }
        },
        calculateFabricTotal(fabric) {
            return fabric.colors.reduce((total, color) => total + color.fcpu * color.recv, 0);
        },
        hideDiv() {
            this.isVisible = false;
        },
        btnCompleted() {
            this.show = !this.show;
            this.btnDisable = true; // Disable the button
        },
        sendMessage() {
            if (this.actionValue.trim() !== '') {
                const message = {
                    id: Date.now(),
                    text: this.actionValue,
                    title: this.actionName.title,
                    timestamp: new Date().toLocaleDateString('en-US', { day: 'numeric', month: 'long' }),
                    timestamp2: new Date().toLocaleTimeString([], { hour: '2-digit', minute: '2-digit' }),
                    type: 'outgoing',
                };
                this.messages.push(message);
                this.actionName = [];
                this.actionValue = '';
                this.showActionModal = false;
            }
        },
        stockIn(index) {
            this.issues[index].received.date = this.selectedDate;
            let beforCount = this.issues[index].jobs.length;
            this.issues[index].jobs.push(this.issues[index].received);
            let afterCount = this.issues[index].jobs.length;
            console.log(beforCount)
            console.log(afterCount)
        },
        balanceQuantity(item) {
            if (item.jobs.length > 0) {
                return item.jobs.reduce((accumulator, job) => accumulator + job.collect - job.loss, 0);
            } else {
                return 0;
            }
        },
        submitForm() {
            if (this.form.assignee !== null) {
                const issueData = {
                    userId: this.selectedUserId,
                    qty: this.form.qty,
                    rate: this.form.rate,
                    ptpuim: this.form.ptpuim,
                    assignee: this.form.assignee,
                    start_date: this.form.start_date,
                    due_date: this.form.due_date,
                    end_date: null,
                    received: {
                        collect: null,
                        loss: null,
                        date: null,
                    },
                    job: []

                };
                this.$store.dispatch('pushToIssue', issueData).then(() => {
                    this.form = {
                        selectedUserId: null,
                        qty: 0,
                        rate: 0,
                        ptpuim: '',
                        assignee: null,
                        start_date: '',
                        due_date: '',
                        end_date: null,
                        received: {
                            collect: null,
                            loss: null,
                            date: null,
                        },
                        jobs: []
                    }
                });
            }
        },
        saveColorData(colors) {
            const colorDataToSave = colors.map((color) => ({
                bg: color.bg,
                fcpuRecvProduct: color.fcpu * color.recv,
                recv: color.recv,
                fcpu: color.fcpu,
                width: color.width,
                qty: color.qty,
            }));

            this.savedColorData.push(colorDataToSave);

            colors.forEach((color) => {
                color.recv = 0;
            });
        },
        addJob() {
            // Convert start and end to Date objects
            this.newJob.start = new Date(this.newJob.start);

            // Check if start, end, and group are empty and handle them as needed
            if (!this.newJob.start || !this.newJob.group) {
                // Handle empty fields here, for example, set default values
                this.newJob.start = new Date(); // Set to the current date and time
                this.newJob.group = this.stations[0].id; // Set to the first station by default
            }

            // Check if end date is empty
            if (!this.newJob.end) {
                // Calculate end time based on newJob.ptpuim * newJob.fabric
                if (this.newJob.ptpuim && this.newJob.fabric) {
                    const ptpuim = parseFloat(this.newJob.ptpuim);
                    const fabric = parseFloat(this.newJob.fabric);

                    // Calculate the end time in minutes
                    const endTimeInMinutes = ptpuim * fabric;

                    // Calculate the end time as a Date object
                    const startTime = this.newJob.start.getTime();
                    const endTime = new Date(startTime + (endTimeInMinutes * 60 * 1000));
                    this.newJob.end = endTime;
                } else {
                    // Handle the case where ptpuim or fabric is missing
                    // You can display an error message or handle it in your UI as needed.
                    // For now, we'll set end to the start time as a placeholder.
                    this.newJob.end = this.newJob.start;
                }
            }

            if (this.newJob.id !== undefined) {
                // Update existing job
                const updatedJobIndex = this.jobs.findIndex(job => job.id === this.newJob.id);
                if (updatedJobIndex !== -1) {
                    this.jobs[updatedJobIndex] = { ...this.newJob }; // Clone the object
                    this.items.update(this.newJob); // Update the item in DataSet
                }
            } else {
                // Add new job
                this.newJob.id = this.jobs.length + 1; // Assign a unique ID
                // Dispatch a Vuex action to add the job
                this.$store.dispatch('addJob', { job: { ...this.newJob } });
            }

            // Reset the form fields
            this.newJob = {
                content: this.manager.style,
                ptpuim: '',
                fcpu: '',
                fabric: this.totalFromChild,
                start: '',
                end: '',
                group: this.earliestAvailableStationId,
                dept: ''
            };
        },
        onTotalCalculated(parentData) {
            this.totalFromChild = parentData.total
            this.acceptedFabric = parentData.fabric;
            this.newJob.allotedFabric = this.acceptedFabric.id;
        },

        submitFinishing() {
            this.$store.dispatch('finishigNewJob', {
                tableData: this.quantities,
                issue: this.finishingForm.issue
            })
        },



    },
    mounted() {
        this.newJob.fabric = this.totalFromChild;
        this.newJob.content = this.manager.style;
        this.newJob.group = this.earliestAvailableStationId;
        this.newJob.start = this.formattedJobEnd;
        const now = new Date();
        // this.start_date = now.toISOString().slice(0, 10);
        this.selectedDate = now.toISOString().slice(0, 10);
        this.selectedTime = now.toTimeString().slice(0, 5);
        const defaultValue = 100;
        this.quantities = Array.from({ length: this.manager.colors.length }, () =>
            Array(this.manager.sizes.length).fill(defaultValue)
        );
        // Set the default selected fabric to the first one in the manager.fabrics array
        if (this.manager.fabrics.length > 0) {
            this.newJob.allotedFabric = this.manager.fabrics[0].id;
        }
    },
    watch: {
        totalFromChild(newValue) {
            this.newJob.fabric = newValue;
        },
        // Watch for changes in jobEndForEarliestStation and update newJob.start
        jobEndForEarliestStation: {
            handler(newValue) {
                if (newValue) {
                    // Format the newValue to match datetime-local format: "YYYY-MM-DDTHH:mm"
                    const formattedDate = new Date(newValue).toISOString().slice(0, 16);

                    // Update newJob.start with the formatted value
                    this.newJob.start = formattedDate;
                }
            },
            immediate: true, // Trigger the handler immediately
        },
    },
    created() {
        for (let colorIndex = 0; colorIndex < this.manager.colors.length; colorIndex++) {
            this.quantities[colorIndex] = [];
            for (let sizeIndex = ''; sizeIndex < this.manager.sizes.length; sizeIndex++) {
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
}

table th:nth-child(7),
.table td:nth-child(7) {
    position: sticky;
    right: 0;
    background-color: #f8f8f7;
    color: #373737;
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
    /* background-color: #606C5D; */
    background-color: #28CC9E;
}

.nav-link {
    color: #000000;
}
</style>