<template>
    <div>
        <p>This example demonstrates custom ordering of groups.</p>

        <div class="px-2 py-3">
            <form @submit.prevent="submitForm">
                <div class="form-floating mb-3">
                    <input type="number" class="form-control" id="floatingInput" placeholder="Catalog ID" value="" readonly>
                    <label for="floatingInput">Catalog Id</label>
                </div>
                <div class="form-floating mb-3">
                    <input type="number" class="form-control" id="PTPUIM" placeholder="PTPUIM" v-model="form.ptpuim">
                    <label for="PTPUIM">PTPUIM</label>
                </div>
                <div class="input-group mb-3 w-100">
                    <span class="input-group-text w-75" id="basic-addon1">Expected Qty</span>
                    <input style="background-color: #f8f9fa;" type="number" :value="form.qty" class="form-control w-25"
                        aria-describedby="basic-addon1">
                </div>
                <div>
                    <select class="form-select my-3" aria-label="Default select example" v-model="form.assignee"
                        @change="getSelectedOptionId">
                        <option selected>Select Assignee</option>
                        <option v-for="(user, index) in filteredUsers" :key="index" :value="user.name">
                            {{ user.dept }} ({{ user.name }})
                        </option>
                        <p v-if="selectedUserId">Selected User ID: {{ selectedUserId }}</p>
                        <p v-else>No assignee selected.</p>
                    </select>
                </div>
                <div class=" my-3">
                    <div class="mb-2">
                        <label for="date" class="form-label ms-1">Start Date</label>
                        <input type="datetime-local" class="form-control" id="date" v-model="form.start">
                    </div>
                    <div class="mb-2">
                        <label for="date" class="form-label ms-1">End Date</label>
                        <input type="datetime-local" class="form-control" id="date" v-model="form.end">
                    </div>
                </div>
                <div class="d-flex justify-content-center mb-3">
                    <button class="btn btn-primary">Submit</button>
                </div>
            </form>
        </div>

        <div id="visualization"></div>
    </div>
</template>
  
<script>
import vis from 'vis-timeline/standalone/umd/vis-timeline-graph2d.min.js';
import 'vis-timeline/styles/vis-timeline-graph2d.min.css';
export default {
    mounted() {
        this.initializeTimeline();
    },
    data() {
        return {
            stations: [
                { id: 0, content: 'Station 1', value: 'station-one' },
                { id: 1, content: 'Station 2', value: 'station-two' },
                { id: 2, content: 'Station 3', value: 'station-three' },
            ],
            jobs: [
                { id: 0, group: 0, content: '#23458-75', start: new Date(2023, 8, 24, 9, 30), end: new Date(2023, 8, 24, 12, 30) },
                { id: 1, group: 0, content: '#23478-80', start: new Date(2023, 8, 24, 13, 0), end: new Date(2023, 8, 24, 16, 0) },
                { id: 2, group: 1, content: '#22338-50', start: new Date(2023, 8, 24, 9, 30), end: new Date(2023, 8, 24, 11, 30) },
                { id: 3, group: 2, content: '#24555-150', start: new Date(2023, 8, 24, 9, 30), end: new Date(2023, 8, 24, 15, 0) },
                { id: 5, group: 2, content: '#24558-100', start: new Date(2023, 8, 24, 15, 30), end: new Date(2023, 8, 24, 19, 0) },
                { id: 6, group: 1, content: '#23458-75', start: new Date(2023, 8, 24, 12, 0), end: new Date(2023, 8, 24, 20, 0) }

            ],
            form: {
                qty: 0,
                rate: 0,
                ptpuim: '',
                assignee: null,
                start: null, // Changed from 'start' to 'start_date'
                end: null,   // Changed from 'end' to 'due_date'
            },
        }
    },
    computed: {
        users() {
            return this.$store.getters.getUsers;
        },
        filteredUsers() {
            return this.users.filter(user => (user.dept === 'Stiching' || user.dept === 'Fabricator') && user.post === 'Incharge');
        },
    },
    methods: {
        initializeTimeline() {
            const groups = new vis.DataSet(this.stations);

            const items = new vis.DataSet(this.jobs);

            const container = document.getElementById('visualization');
            const options = {
                groupOrder: (a, b) => a.value - b.value,
                editable: true
            };

            this.timeline = new vis.Timeline(container);
            this.timeline.setOptions(options);
            this.timeline.setGroups(groups);
            this.timeline.setItems(items);

            // Event listeners for DataSet events
            items.on('add', this.onDataSetAdd);

        },
        submitForm() {
            // Create a new job object based on the form data
            const newJob = {
                id: this.jobs.length, // Generate a new job ID
                group: 0,            // Adjust the group as needed
                content: this.form.ptpuim,
                start: new Date(this.form.start), // Use the start_date value from the form
                end: new Date(this.form.end),     // Use the due_date value from the form
            };

            // Add the new job to the jobs array
            this.jobs.push(newJob);

            // Reset the form
            this.form = {
                qty: 0,
                rate: 0,
                ptpuim: '',
                assignee: null,
                start: null,
                end: null,
            };
        },
        onDataSetAdd(event, items) {
            console.log('Items added:', items);
        },
    }
};
</script>
  
<style scoped>
/* Add any custom styles for your component here */
#visualization {
    box-sizing: border-box;
    width: 100%;
    height: 300px;
}
</style>
  