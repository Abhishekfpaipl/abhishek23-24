<template>
    <div>

        <!-- <div class="mt-4">
            <h2>Create New Job</h2>
            <form @submit.prevent="addJob" class="row g-3">
                <div class="col-md-4">
                    <label for="jobContent" class="form-label">Content</label>
                    <input v-model="newJob.content" type="text" class="form-control" id="jobContent" required>
                </div>
                <div class="col-md-4">
                    <label for="jobPtpuim" class="form-label">PTPUIM</label>
                    <input v-model="newJob.ptpuim" type="text" class="form-control" id="jobPtpuim" required>
                </div>
                <div class="col-md-4">
                    <label for="jobProduction" class="form-label">Production</label>
                    <input v-model="newJob.production" type="text" class="form-control" id="jobProduction" required>
                </div>
                <div class="col-md-4">
                    <label for="jobStart" class="form-label">Start</label>
                    <input v-model="newJob.start" type="datetime-local" class="form-control" id="jobStart" required>
                </div>
                <div class="col-md-4">
                    <label for="jobEnd" class="form-label">End</label>
                    <input v-model="newJob.end" type="datetime-local" class="form-control" id="jobEnd" required>
                </div>
                <div class="col-md-4">
                    <label for="jobGroup" class="form-label">Group</label>
                    <select v-model="newJob.group" class="form-select" id="jobGroup" required>
                        <option v-for="(station, index) in stations" :key="index" :value="station.id">{{ station.content }}
                        </option>
                    </select>
                </div>
                <div class="col-12">
                    <button v-if="selectedJob" @click="updateJob" class="btn btn-success">Update Job</button>
                    <button type="submit" @click="addJob" class="btn btn-primary">Create Job</button>
                </div>

            </form>
        </div> -->

        <div class="mt-4">
            <h2>{{ selectedJob ? 'Edit Job' : 'Create New Job' }}</h2>
            <form @submit.prevent="selectedJob ? updateJob() : addJob()" class="row g-3">
                <div class="col-md-4">
                    <label for="jobContent" class="form-label">Content</label>
                    <input v-model="newJob.content" type="text" class="form-control" id="jobContent" required>
                </div>
                <div class="col-md-4">
                    <label for="jobPtpuim" class="form-label">PTPUIM</label>
                    <input v-model="newJob.ptpuim" type="text" class="form-control" id="jobPtpuim" required>
                </div>
                <div class="col-md-4">
                    <label for="jobProduction" class="form-label">Production</label>
                    <input v-model="newJob.production" type="text" class="form-control" id="jobProduction" required>
                </div>
                <div class="col-md-4" v-if="selectedJob">
                    <label for="jobStart" class="form-label">Start</label>
                    <input v-model="newJob.start" type="datetime-local" class="form-control" id="jobStart">
                </div>
                <!-- <div class="col-md-4" v-if="selectedJob">
                    <label for="jobEnd" class="form-label">End</label>
                    <input v-model="newJob.end" type="datetime-local" class="form-control" id="jobEnd">
                </div> -->
                <div class="col-md-4" v-if="selectedJob">
                    <label class="form-label">End</label>
                    <input :value="calculateEndTime()" type="text" class="form-control" disabled>
                </div>
                <div class="col-md-4" v-if="selectedJob">
                    <label for="jobGroup" class="form-label">Group</label>
                    <select v-model="newJob.group" class="form-select" id="jobGroup">
                        <option v-for="(station, index) in stations" :key="index" :value="station.id">{{ station.content }}
                        </option>
                    </select>
                </div>
                <div class="col-12">
                    <button v-if="selectedJob" @click="updateJob" class="btn btn-success">Update Job</button>
                    <button type="submit" v-else class="btn btn-primary">Create Job</button>
                    <button v-if="selectedJob" @click="cancelEdit" class="btn btn-danger">Cancel</button>
                </div>
            </form>
        </div>



        <div id="visualization"></div>
        <hr>

        <div class="row">
            <div class="col-md-6" v-for="(job, index) in jobs" :key="index">
                <div class="card" @click="editJob(job)">
                    <div class="card-body d-flex">
                        <img src="https://t3.ftcdn.net/jpg/00/96/74/82/360_F_96748234_L1OpQlE8LQJmmjGpeQZvcOVOkhxCPzCa.jpg"
                            alt="" style="height:50px;object-fit: cover;" class="px-3">
                        <div class="d-flex flex-column flex-fill">
                            <div class="d-flex justify-content-between align-items-center fw-bold">
                                <span>{{ job.content }}</span>
                                <span class="fw-bold">{{ getProductionCount(job) }} pcs</span>
                                <span class="fw-bold">{{ getProductionTime(job) }} min </span>
                                <span>{{ getStationName(job.group) }}</span>
                            </div>
                            <div class="d-flex justify-content-between align-items-center small">
                                <span>{{ getDateFormat(job.start) }}</span>
                                <i class="bi bi-arrow-right"></i>
                                <span>{{ getDateFormat(job.end) }}</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
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
            newJob: {
                content: '',
                ptpuim: '',
                production: '',
                start: '',
                end: '',
                group: ''
            },
            items: new vis.DataSet([]), // Initialize with an empty array
            groups: new vis.DataSet([]), // Initialize with an empty array
            selectedJob: null,
            stations: [
                { id: 0, content: 'Station 1', name: 'Bipin', value: 'station-one' },
                { id: 1, content: 'Station 2', name: 'Aroop', value: 'station-two' },
                { id: 2, content: 'Station 3', name: 'Sadhan', value: 'station-three' },
                { id: 3, content: 'Station 4', name: 'Ravi', value: 'station-four' },
                { id: 4, content: 'Station 5', name: 'Rahul', value: 'station-five' },
                { id: 5, content: 'Station 6', name: 'Ranjeet', value: 'station-six' },
            ],
            jobs: [
                { id: 0, group: 0, content: '#23458', production: '4', ptpuim: '4', start: new Date(2023, 8, 24, 9, 30), end: new Date(2023, 8, 24, 12, 30) },
                { id: 1, group: 0, content: '#23478', production: '150', ptpuim: '3.5', start: new Date(2023, 8, 24, 13, 0), end: new Date(2023, 8, 24, 16, 0) },
                { id: 2, group: 1, content: '#22338', production: '80', ptpuim: '2.5', start: new Date(2023, 8, 24, 9, 30), end: new Date(2023, 8, 24, 11, 30) },
                { id: 3, group: 2, content: '#24555', production: '85', ptpuim: '4.5', start: new Date(2023, 8, 24, 9, 30), end: new Date(2023, 8, 24, 15, 0) },
                { id: 5, group: 2, content: '#24560', production: '96', ptpuim: '5', start: new Date(2023, 8, 24, 15, 30), end: new Date(2023, 8, 24, 19, 0) },
                { id: 6, group: 1, content: '#23470', production: '200', ptpuim: '3', start: new Date(2023, 8, 24, 12, 0), end: new Date(2023, 8, 24, 20, 0) }
            ]
        }
    },
    methods: {
        getStationName(groupId) {
            const foundStation = this.stations.find(station => station.id === groupId);
            return foundStation ? foundStation.name : null;
        },
        getProductionCount(job) {
            // Difference in milliseconds
            const timeDifference = job.end - job.start;

            // Convert milliseconds to hours
            const hours = timeDifference / (1000 * 60 * 60);

            // Multiply the time by job.ptpuim and round to the nearest whole number
            const production = Math.round((hours * 60) / parseFloat(job.ptpuim));

            return production;
        },
        getProductionTime(job) {
            // Calculate the total time required in minutes
            const totalTimeInMinutes = job.production * job.ptpuim;

            // Convert the total time to hours and minutes
            const totalHours = Math.floor(totalTimeInMinutes / 60);
            const remainingMinutes = totalTimeInMinutes % 60;

            // Round the total hours to 1 decimal place
            const roundedTotalHours = totalHours.toFixed(1);
            const roundedTotalMinutes = remainingMinutes.toFixed(1);

            return parseFloat(roundedTotalHours * 60) + parseFloat(roundedTotalMinutes);
        },
        calculateEndTime() {
            if (this.newJob.start && this.newJob.production && this.newJob.ptpuim) {
                const startTime = new Date(this.newJob.start);
                const production = parseFloat(this.newJob.production);
                const ptpuim = parseFloat(this.newJob.ptpuim);

                // Calculate the total time required in minutes
                const totalTimeInMinutes = production / ptpuim;
                
                // Calculate the end time by adding the total time to the start time
                const endTime = new Date(startTime.getTime() + totalTimeInMinutes * 60 * 1000 );
                console.log(startTime)
                console.log(endTime)
                // Format the end time as "YYYY-MM-DD HH:mm"
                const formattedEndTime = endTime.toISOString().slice(0, 16);

                // Set the end date in the newJob object
                this.newJob.end = formattedEndTime;

                return formattedEndTime;
            }

            return '';
        }
        ,
        getDateFormat(dateObject) {
            const options = {
                // weekday: 'long',
                day: 'numeric',
                month: 'short',
                year: 'numeric',
                hour: 'numeric',
                minute: 'numeric',
                // timeZoneName: 'short'
            };
            return dateObject.toLocaleString('en-US', options);
        },
        initializeTimeline() {
            this.groups = new vis.DataSet(this.stations);
            this.items = new vis.DataSet(this.jobs);

            const container = document.getElementById('visualization');
            const options = {
                groupOrder: (a, b) => a.value - b.value,
                editable: true,
            };

            this.timeline = new vis.Timeline(container);
            this.timeline.setOptions(options);
            this.timeline.setGroups(this.groups);

            // Bind the items DataSet to the timeline
            this.timeline.setItems(this.items);

            // Event listeners for DataSet events
            this.items.on('update', this.onDataSetUpdate);

            // Callbacks for add, move, moving, update, and remove actions
            this.items.on('remove', this.onRemove);
        },

        onDataSetUpdate(event, items) {
            const dataItems = items.data;
            dataItems.forEach(itemData => {
                let jobIndex = this.jobs.findIndex(job => job.id === itemData.id);

                if (jobIndex !== -1) { // Check if job with given id exists
                    this.jobs[jobIndex].group = itemData.group;
                    this.jobs[jobIndex].start = new Date(itemData.start); // Convert to Date object if needed
                    this.jobs[jobIndex].end = new Date(itemData.end); // Convert to Date object if needed
                }
            });
            // Update the timeline with the modified dataset
            const updatedItems = new vis.DataSet(this.jobs);
            // this.timeline.setItems(updatedItems);
            updatedItems.on('update', this.onDataSetUpdate);
        },

        onRemove(event, itemData) {
            const removedItemId = itemData.items[0];
            const jobIndex = this.jobs.findIndex(job => job.id === removedItemId);

            if (jobIndex !== -1) {
                const confirmation = window.confirm("Are you sure you want to remove this job?");

                if (confirmation) {
                    // Remove the job from the jobs array
                    this.jobs.splice(jobIndex, 1);

                    // Remove the job from the items DataSet
                    this.items.remove(removedItemId);

                    // Update the timeline directly
                    this.timeline.setItems(this.items);
                }
            }
        },
        editJob(job) {
            this.selectedJob = { ...job };
            this.newJob = {
                id: job.id,
                content: job.content,
                ptpuim: job.ptpuim,
                production: job.production,
                start: job.start.toISOString().slice(0, -1),
                end: job.end.toISOString().slice(0, -1),
                group: job.group,
            };
        },
        addJob() {
            // Convert start and end to Date objects
            this.newJob.start = new Date(this.newJob.start);
            this.newJob.end = new Date(this.newJob.end);

            // Check if start, end, and group are empty and handle them as needed
            if (!this.newJob.start || !this.newJob.end || !this.newJob.group) {
                // Handle empty fields here, for example, set default values
                this.newJob.start = new Date(); // Set to the current date and time
                this.newJob.end = new Date();   // Set to the current date and time
                this.newJob.group = this.stations[0].id; // Set to the first station by default
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
                this.jobs.push({ ...this.newJob }); // Clone the object
                this.items.add(this.newJob); // Add the item to DataSet
            }
            // Reset the form fields
            this.newJob = {
                content: '',
                ptpuim: '',
                production: '',
                start: '',
                end: '',
                group: ''
            };
        },
        updateJob() {
            if (this.selectedJob) {
                const updatedJobIndex = this.jobs.findIndex(job => job.id === this.selectedJob.id);
                if (updatedJobIndex !== -1) {
                    this.jobs[updatedJobIndex] = { ...this.newJob };

                    // Update the item in the items DataSet
                    this.items.update({ ...this.newJob });

                    // Clear the selected job
                    this.selectedJob = null;

                    // Reset the form fields
                    this.newJob = {
                        content: '',
                        ptpuim: '',
                        production: '',
                        start: '',
                        end: '',
                        group: ''
                    };
                }
            }
        }




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
  