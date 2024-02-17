<template>
    <!-- Main container -->
    <div class="my-4">
        <!-- Job Form -->
        <div class="collapse show border" id="Newjobs">
            <div class="px-2 py-3">
                <form @submit.prevent="submitForm()">



                    <!-- Status-dependent text -->
                    <p v-if="manager.status === 'Accept'" class="mb-0">Receive From Stations</p>
                    <!-- Assignee selection based on status -->
                    <select v-if="manager.status === 'Accept'" class="form-select my-3" aria-label="Default select example"
                        v-model="form.assignee">
                        <option selected>Select Assignee</option>
                        <option v-for="(user, index) in recvCutting" :key="index" :value="user.id">{{ user.dept }} ({{
                            user.name }})</option>
                    </select>

                    <p v-if="manager.status === 'Stiching'" class="mb-0">Receive From Stitching</p>
                    <select v-if="manager.status === 'Stiching'" class="form-select my-3"
                        aria-label="Default select example" v-model="form.assignee">
                        <option selected>Select Assignee</option>
                        <option v-for="(user, index) in recvStiching" :key="index" :value="user.id">{{ user.dept }} ({{
                            user.name }})</option>
                    </select>

                    <p v-if="manager.status === 'Finishing'" class="mb-0">Receive To Finishing</p>
                    <select v-if="manager.status === 'Finishing'" class="form-select my-3"
                        aria-label="Default select example" v-model="form.assignee">
                        <option selected>Select Assignee</option>
                        <option v-for="(user, index) in recvFinishing" :key="index" :value="user.id">{{ user.dept }} ({{
                            user.name }})</option>
                    </select>

                    <!-- Table for data entry -->
                    <table class="table table-responsive">
                        <!-- Table header -->
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
                        <!-- Table body for quantity input -->
                        <tbody>
                            <tr v-for="(color, colorIndex) in manager.colors" :key="colorIndex">
                                <td>
                                    <div class="rounded px-1 align-items-center justify-content-center d-flex"
                                        style="width: 36px; height: 36px;" :style="'background-color :' + color.bg"></div>
                                </td>
                                <td v-for="(size, sizeIndex) in manager.sizes" :key="sizeIndex">
                                    <input type="number" class="form-control text-center"
                                        v-model="quantities[`${color.id}_${size.id}`]">
                                </td>
                            </tr>
                            <!-- Row for calculating sizes total -->
                            <tr scope="row">
                                <th>Qty</th>
                                <td class="text-center" v-for="(size, sizeindex) in  manager.sizes" :key="sizeindex">
                                    {{ calculateSizesTotal(sizeindex) }}
                                </td>
                            </tr>
                        </tbody>
                    </table>

                    <!-- Container for total ordered quantity -->
                    <div class="container mb-3">
                        <div class="d-flex justify-content-between mx-3 py-2 px-4 border"
                            style="background-color: #e8e8e8;">
                            <p class="mb-0">Actual Ordered Qty</p>
                            <p class="fw-bold text-center mb-0">{{ calculateGrossTotalQty }} pcs</p>
                        </div>
                    </div>

                    <!-- Assignee selection based on status -->
                    <p v-if="manager.status === 'Accept'" class="mb-0">Issue To Stitching</p>
                    <select v-if="manager.status === 'Accept'" class="form-select my-3" aria-label="Default select example"
                        v-model="form.assign">
                        <option selected>Select Assignee</option>
                        <option v-for="(user, index) in recvStiching" :key="index" :value="user.id">{{ user.dept }} ({{
                            user.name }})</option>
                    </select>

                    <p v-if="manager.status === 'Stiching'" class="mb-0">Issue To Finishing</p>
                    <select v-if="manager.status === 'Stiching'" class="form-select my-3"
                        aria-label="Default select example" v-model="form.assign">
                        <option selected>Select Assignee</option>
                        <option v-for="(user, index) in recvFinishing" :key="index" :value="user.id">{{ user.dept }} ({{
                            user.name }})</option>
                    </select>

                    <p v-if="manager.status === 'Finishing'" class="mb-0">Issue To Shop</p>
                    <select v-if="manager.status === 'Finishing'" class="form-select my-3"
                        aria-label="Default select example" v-model="form.assign">
                        <option selected>Select Assignee</option>
                        <option v-for="(user, index) in filteredUser" :key="index" :value="user.id">{{ user.dept }} ({{
                            user.name }})</option>
                    </select>

                    <!-- Date and Time inputs -->
                    <div class="d-flex w-100">
                        <div class="mb-2 mx-2 w-50">
                            <label for="date" class="form-label ms-1">Expected Date</label>
                            <input type="date" class="form-control" id="date" v-model="form.exp_date">
                        </div>
                        <div class="mb-2 mx-2 w-50">
                            <label for="time" class="form-label ms-1">Expected Time</label>
                            <input type="time" class="form-control" id="time" v-model="form.exp_time">
                        </div>
                    </div>

                    <!-- Submit button -->
                    <div class="d-flex justify-content-center mb-3">
                        <button class="btn btn-primary">Issue Job</button>
                    </div>
                </form>
            </div>
        </div>

        <div class="my-3" v-if="jobHistory.length > 0">
            <h2 class="text-center">Job History</h2>
            <div class="" v-for="(job, index) in jobHistory" :key="index">
                <div class="border my-2">
                    <p class=""></p>
                    <table class="table">
                        <tbody>
                            <tr>
                                <th>Received From</th>
                                <td>{{ job.assignee }}</td>
                            </tr>
                            <tr>
                                <th>Issued To</th>
                                <td>{{ job.assign }}</td>
                            </tr>
                            <tr>
                                <th>Expected Date</th>
                                <td>{{ job.exp_date }}</td>
                            </tr>
                            <tr>
                                <th>Expected Time</th>
                                <td>{{ job.exp_time }}</td>
                            </tr>
                        </tbody>
                    </table>
                    <div class="accordion" id="accordionExample">
                        <div class="accordion-item">
                            <h2 class="accordion-header">
                                <button class="accordion-button collapsed" type="button" data-bs-toggle="collapse"
                                    :data-bs-target="'#collapseTwo' + index" aria-expanded="false"
                                    :aria-controls="'collapseTwo' + index">
                                    Job Details
                                </button>
                            </h2>
                            <div :id="'collapseTwo' + index" class="accordion-collapse collapse"
                                data-bs-parent="#accordionExample">
                                <div class="accordion-body">
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
                                                        style="width: 36px; height: 36px;"
                                                        :style="'background-color :' + color.bg">
                                                    </div>
                                                </td>
                                                <td v-for="(size, sizeIndex) in managerSizes" :key="sizeIndex">
                                                    {{ job.tableData[`${color.id}_${size.id}`] || 0 }}
                                                </td>
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
    props: ['manager'],
    data() {
        return {
            form: {
                qty: 0,
                rate: 0,
                amt: 0,
                lost: 0,
                assignee: null,
                assign: null,
                exp_date: '',
                exp_time: '',
                end_date: null,
                received: {
                    collect: null,
                    loss: null,
                    date: null,
                },
                jobs: []
            },
            quantities: {},
            // jobHistory: [{ "assignee": "Cutting (Mohan)", "assign": "Stiching (Sameer)", "exp_date": "2023-09-06", "exp_time": "15:41", "tableData": { "1_1": 1, "1_2": 1, "1_3": 1, "1_4": 11, "2_1": 1, "2_2": 1, "2_3": 1, "2_4": 0, "3_1": 1, "3_2": 0, "3_3": 1, "3_4": 0, "4_1": 1, "4_2": 1, "4_3": 0, "4_4": 1 } }]

        }
    },
    computed: {
        jobHistory() {
            return this.$store.getters.getJobHistory
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
        users() {
            return this.$store.getters.getUsers;
        },
        recvCutting() {
            return this.users.filter(user => user.post === 'Incharge' && user.dept === 'Cutting');
        },
        recvStiching() {
            return this.users.filter(user => user.post === 'Incharge' && user.dept === 'Stiching');
        },
        recvFinishing() {
            return this.users.filter(user => (user.dept === 'Finishing') && user.post === 'Incharge');
        },
        filteredUser() {
            return this.users.filter(user => (user.dept === 'Shop') && user.post === 'Owner');
        },
        skuCount() {
            return this.manager.colors.length * this.manager.sizes.length;
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
        calculateGrossTotalQty() {
            let totalQty = 0;
            this.manager.colors.forEach(color => {
                this.manager.sizes.forEach(size => {
                    const quantity = this.quantities[`${color.id}_${size.id}`];
                    if (quantity) {
                        totalQty += parseInt(quantity);
                    }
                });
            });
            return totalQty;
        },
    },
    methods: {
        findUserById(userId) {
            return this.users.find(user => user.id === userId);
        },
        submitForm() {
            const assigneeUser = this.findUserById(this.form.assignee);
            const assignUser = this.findUserById(this.form.assign);

            if (assigneeUser && assignUser) {
                this.$store.dispatch('createNewJob', {
                    assignee: `${assigneeUser.dept} (${assigneeUser.name})`,
                    assign: `${assignUser.dept} (${assignUser.name})`,
                    exp_date: this.form.exp_date,
                    exp_time: this.form.exp_time,
                    tableData: this.quantities,
                })
                // .then(() => {
                //     this.resetAllotmentForm();
                // })
            }
            // if (assigneeUser && assignUser) {
            //     const newJob = {
            //         assignee: `${assigneeUser.dept} (${assigneeUser.name})`,
            //         assign: `${assignUser.dept} (${assignUser.name})`,
            //         exp_date: this.form.exp_date,
            //         exp_time: this.form.exp_time,
            //         tableData: this.quantities,
            //     };
            //     this.jobHistory.push(newJob);
            // }
        },
        resetAllotmentForm() {
            this.form.assignee = null;
            this.form.assign = null;
            this.form.exp_date = new Date().toISOString().slice(0, 10);
            this.form.exp_time = new Date().toTimeString().slice(0, 5);
            this.manager.colors.forEach(color => {
                this.manager.sizes.forEach(size => {
                    this.quantities[`${color.id}_${size.id}`] = 0;
                });
            });
        },
    },
    mounted() {
        this.resetAllotmentForm();
    },
}
</script>
  