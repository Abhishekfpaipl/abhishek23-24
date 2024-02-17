<template>
    <div class="" v-for="(job, index) in jobs" :key="index">
        <div class="d-flex justify-content-between align-items-center  py-2 bg-light">

            <div class="mx-2 d-flex justify-content-center">
                <img :src="`${publicPath}${getUserForJob(job).imgu}`" class="rounded-circle "
                    style="width: 45px; height: 45px; object-fit: cover;" alt="">

            </div>
            <div class="mx-2 text-center">
                <span class="d-block"> {{ job.qty }} </span>
                <span class="smaller ">
                    {{ new Date(job.start_date).toDateString().substring(4, 10) }}
                </span>
            </div>

            <div class="text-center  mx-2">
                <!-- <span class="d-block">{{ collectQuantity(job) }}</span> -->
                <span class="smaller">
                    {{ new Date(job.due_date).toDateString().substring(4, 10) }}
                </span>

            </div>
            <div class="mx-2 text-center">
                <!-- <span class="d-block"> {{ lostQuantity(job) }} </span> -->
                <span class="smaller ">
                    {{ new Date(job.start_date).toDateString().substring(4, 10) }}
                </span>
            </div>

            <button class="btn btn-outline-secondary px-2 mx-2" data-bs-toggle="collapse"
                :data-bs-target="'#Job' + index" aria-expanded="false" :aria-controls="'Job' + index">
                {{ job.qty - 200 }}<span class="smaller d-block">Balance</span>
            </button>

        </div>
        <!-- <div >
            <div :id="'Job' + index" class="collapse ">
                <div class="d-flex justify-content-between border-bottom py-2 bg-light rounded">
                    <div class="form-floating mx-2">
                        <input v-model="received.collect" type="number" class="form-control" id="floatingInput">
                        <label for="floatingInput">Received Qty</label>
                        <small v-if="(received.collect + received.loss) > balanceQuantity(issue)" class="text-danger">
                            Invalid quantity.
                        </small>
                    </div>
                    <div class="form-floating mx-2">
                        <input v-model="received.loss" type="number" class="form-control" id="floatingInput"
                            placeholder="Loss Quantity">
                        <label for="floatingInput">Lost Qty</label>
                    </div>
                    <div class="d-flex flex-column justify-content-center mx-2">
                        <button class="btn btn-outline-secondary " style="width: 4.1em;" @click="stockIn(index)">
                            <span>+</span>
                            <span class="smaller d-block">Settle</span></button>
                    </div>
                </div>
                <div class="mt-2">
                    <table class="table table-light table-striped border">
                        <thead>
                            <tr class="text-center">
                                <th scope="col">Date</th>
                                <th scope="col">Recv.</th>
                                <th scope="col">Rate</th>
                                <th scope="col">Amt.</th>
                                <th scope="col">Lost</th>
                                <th scope="col">Settle</th>
                            </tr>
                        </thead>
                        <tbody>
                            <tr v-for="(job, jobIndex) in issue.jobs" :key="jobIndex" class="text-center">
                                <td>{{ new Date(job.date).toDateString().substring(4, 10) }}</td>
                                <td>{{ job.collect }}</td>
                                <td>{{ issue.rate }}</td>
                                <td>{{ job.collect * issue.rate }}</td>
                                <td>{{ job.loss }}</td>
                                <td>{{ jobSettleQuantity(job) }}</td>
                            </tr>
                        </tbody>
                    </table>

                </div>
            </div>
        </div> -->
    </div>
</template>

<script>
export default {
    data() {
        return {
            publicPath: process.env.BASE_URL
        }
    },
    computed: {
        jobs() {
            return this.$store.getters.getJob
        },
        users() {
            return this.$store.getters.getUsers;
        },
        // userId(){
        //     return 8;
        // },
        getUserForJob() {
            return job => {
                // Find the user with the userId from the current job
                return this.users.find(user => user.id === job.userId);
            };
        }
    }
}
</script>

