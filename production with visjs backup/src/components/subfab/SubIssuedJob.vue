<template>
    <div class="border">
        <div class="d-flex justify-content-between align-items-center  py-2 bg-light">

            <div class="mx-2 d-flex justify-content-center">
                <img :src="issues.img" class="rounded-circle " style="width: 45px; height: 45px; object-fit: cover;" alt="">
            </div>

            <div class="mx-2 text-center">
                <span class="d-block"> {{ issues.qty }} </span>
                <span class="smaller ">
                    {{ new Date(issues.start_date).toDateString().substring(4, 10) }}
                </span>
            </div>

            <div class="mx-2 text-center">
                <span class="d-block"> {{ lostQuantity(issues) }} </span>
                <span class="smaller ">
                    {{ new Date(issues.start_date).toDateString().substring(4, 10) }}
                </span>
            </div>

            <div class="text-center  mx-2">
                <span class="d-block">{{ balanceQuantity(issues) }}</span>
                <span class="smaller">
                    {{ new Date(issues.due_date).toDateString().substring(4, 10) }}
                </span>

            </div>

            <button class="btn btn-outline-secondary px-2 mx-2" data-bs-toggle="collapse"
                :data-bs-target="'#collapseJob' + index" aria-expanded="false" :aria-controls="'collapseJob' + index">
                {{ receivedQuantity(issues) }}<span class="smaller d-block">Received</span>
            </button>

        </div>

        <div :id="'collapseJob' + index" class="collapse ">
            <div class="d-flex justify-content-between border-bottom py-2 bg-light rounded">
                <div class="form-floating mx-2">
                    <input v-model="received.collect" type="number" class="form-control" id="floatingInput">
                    <label for="floatingInput">Received Qty</label>
                    <small v-if="(received.collect + received.loss) > balanceQuantity(issues)" class="text-danger">
                        Invalid quantity.
                    </small>
                </div>
                <div class="form-floating mx-2">
                    <input v-model="received.loss" type="number" class="form-control" id="floatingInput"
                        placeholder="Loss Quantity">
                    <label for="floatingInput">Loss Qty</label>
                </div>
                <div class="d-flex flex-column justify-content-center mx-2">
                    <button class="btn btn-outline-secondary " style="width: 4.1em;" @click="stockIn(index)"> <span>+</span>
                        <span class="smaller d-block">Stock</span></button>
                </div>
            </div>
            <div class="mt-2 mx-4">s
                <table class="table table-light table-striped border">
                    <thead>
                        <tr class="text-center">
                            <th scope="col">Collect</th>
                            <th scope="col">Lost</th>
                            <th scope="col">Date</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="(job, jobIndex) in issues.jobs" :key="jobIndex" class="text-center">
                            <td>{{ job.collect }}</td>
                            <td>{{ job.loss }}</td>
                            <td>{{ job.date }}</td>
                        </tr>
                    </tbody>
                </table>

            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'issuesdJob',
    props: ['index', 'issues'],
    data() {
        return {
            received: {
                collect: null,
                loss: 0,
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
        stockInn() {
            this.$store.dispatch('stockInn', {
                issues: this.issues,
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
        collectedQuantity(issues) {
            if (issues.jobs.length > 0) {
                return issues.jobs.reduce((accumulator, job) => accumulator + job.collect, 0);
            } else {
                return 0;
            }
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
        balanceQuantity(issues) {
            return issues.qty - this.receivedQuantity(issues);
        }
    },
}
</script>

