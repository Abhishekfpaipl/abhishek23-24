<template>
    <div class="border">
        <div v-if="balanceQuantity(issue) > 0">
            <div class="d-flex justify-content-between align-items-center  py-2 bg-light">

                <div class="mx-2 d-flex justify-content-center">
                    <img :src="issue.img" class="rounded-circle " style="width: 45px; height: 45px; object-fit: cover;"
                        alt="">
                </div>

                <div class="mx-2 text-center">
                    <span class="d-block"> {{ issue.qty }} </span>
                    <span class="smaller ">
                        {{ new Date(issue.start_date).toDateString().substring(4, 10) }}
                    </span>
                </div>

                <div class="text-center  mx-2">
                    <span class="d-block">{{ collectQuantity(issue) }}</span>
                    <span class="smaller">
                        {{ new Date(issue.due_date).toDateString().substring(4, 10) }}
                    </span>

                </div>
                <div class="mx-2 text-center">
                    <span class="d-block"> {{ lostQuantity(issue) }} </span>
                    <span class="smaller ">
                        {{ new Date(issue.start_date).toDateString().substring(4, 10) }}
                    </span>
                </div>

                <button class="btn btn-outline-secondary px-2 mx-2" data-bs-toggle="collapse"
                    :data-bs-target="'#collapseJob' + index" aria-expanded="false" :aria-controls="'collapseJob' + index">
                    {{ balanceQuantity(issue) }}<span class="smaller d-block">Balance</span>
                </button>

            </div>
        </div>

        <div v-if="balanceQuantity(issue) > 0">
            <div :id="'collapseJob' + index" class="collapse ">
                <div class="d-flex justify-content-between border-bottom py-2 bg-light rounded">
                    <div class="">
                        <div class="d-flex">
                            <div class="form-floating mx-2">
                                <input v-model="received.collect" type="number" class="form-control" id="floatingInput">
                                <label for="floatingInput">Received Qty</label>
                                <small v-if="(received.collect + received.loss) > balanceQuantity(issue)"
                                    class="text-danger">
                                    Invalid quantity.
                                </small>
                            </div>
                            <div class="form-floating mx-2">
                                <input v-model="received.loss" type="number" class="form-control" id="floatingInput"
                                    placeholder="Loss Quantity">
                                <label for="floatingInput">Lost Qty</label>
                            </div>
                        </div>
                        <div class="mx-2">
                            <p class="mb-0">Lorem ipsum dolor sit amet consectetur adipisicing elit. Voluptas, odio!</p>
                        </div>
                    </div>

                    <div class="d-flex flex-column justify-content-center align-items-center mx-2">
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
        </div>
    </div>
</template>

<script>
export default {
    name: 'issuedJob',
    props: ['index', 'issue'],
    data() {
        return {
            received: {
                collect: null,
                loss: 0,
                balance: this.issue.qty,
                date: null,
            },
            publicPath: process.env.BASE_URL,
        };
    },
    mounted() {
        this.setTodayDate();
    },
    methods: {
        setTodayDate() {
            const now = new Date();
            this.received.date = now.toUTCString().slice(4, 17);
            // this.received.date = now.toISOString().slice(0, 10);
        },
        stockIn() {
            this.received.balance = this.received.collect + this.received.lost
            this.$store.dispatch('stockIn', {
                issue: this.issue,
                qty: this.received
            }).then(() => {
                this.received = {
                    collect: null,
                    loss: 0,
                    date: null,
                };
                this.setTodayDate();

            });

        },

        lostQuantity(issue) {
            if (issue.jobs.length > 0) {
                return issue.jobs.reduce((accumulator, job) => accumulator + job.loss, 0);
            } else {
                return 0;
            }
        },
        collectQuantity(issue) {
            if (issue.jobs.length > 0) {
                return issue.jobs.reduce((accumulator, job) => accumulator + job.collect, 0);
            } else {
                return 0;
            }
        },
        receivedQuantity(issue) {
            return this.collectQuantity(issue) + this.lostQuantity(issue);
        },


        balanceQuantity(issue) {
            return issue.qty - this.receivedQuantity(issue);
        },

        jobSettleQuantity(job) {
            return job.collect + job.loss;
        },
    },
}
</script>

