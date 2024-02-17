<template>
    <div>
        <div class="mt-4">
            <h2>Create New Job</h2>
            <form @submit.prevent="addJob()" class="row g-3">
                <div class="col-md-4">
                    <label for="jobContent" class="form-label">Content</label>
                    <input v-model="newJob.content" type="text" class="form-control" id="jobContent" required>
                </div>
                <div class="col-md-4">
                    <label for="jobPtpuim" class="form-label">PTPUIM</label>
                    <input v-model="newJob.ptpuim" type="text" class="form-control" id="jobPtpuim" required>
                </div>
                <div class="col-md-4">
                    <label for="jobfabric" class="form-label">fabric</label>
                    <input v-model="newJob.fabric" type="text" class="form-control" id="jobfabric" required>
                </div>
                <div class="col-md-4">
                    <label for="jobStart" class="form-label">Start</label>
                    <input v-model="newJob.start" type="datetime-local" class="form-control" id="jobStart">
                </div>
                <div class="col-md-4">
                    <label for="jobEnd" class="form-label">End</label>
                    <input v-model="newJob.end" type="datetime-local" class="form-control" id="jobEnd">
                </div>
                <div class="col-md-4">
                    <label for="jobGroup" class="form-label">Group</label>
                    <select v-model="newJob.group" class="form-select" id="jobGroup">
                        <option v-for="(station, index) in stations" :key="index" :value="station.id">{{ station.content }}
                        </option>
                    </select>
                </div>
                <div class="col-12">
                    <button type="submit" class="btn btn-primary">Create Job</button>
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
                                <span class="fw-bold">{{ getfabricCount(job) }} pcs</span>
                                <span class="fw-bold">{{ getfabricTime(job) }} min </span>
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
                fabric: '',
                start: '',
                end: '',
                group: ''
            },
            items: new vis.DataSet([]), // Initialize with an empty array
            groups: new vis.DataSet([]), // Initialize with an empty array
            selectedJob: null,
        }
    },
    computed: {
        stations() {
            return this.$store.getters.getStation
        },
        jobs() {
            return this.$store.getters.getStationJob
        },
    },
    methods: {
        getStationName(groupId) {
            const foundStation = this.stations.find(station => station.id === groupId);
            return foundStation ? foundStation.name : null;
        },
        getfabricCount(job) {
            // Difference in milliseconds
            const timeDifference = job.end - job.start;

            // Convert milliseconds to hours
            const hours = timeDifference / (1000 * 60 * 60);

            // Multiply the time by job.ptpuim and round to the nearest whole number
            const fabric = Math.round((hours * 60) / parseFloat(job.ptpuim));

            return fabric;
        },
        getfabricTime(job) {
            // Calculate the total time required in minutes
            const totalTimeInMinutes = job.fabric * job.ptpuim;

            // Convert the total time to hours and minutes
            const totalHours = Math.floor(totalTimeInMinutes / 60);
            const remainingMinutes = totalTimeInMinutes % 60;

            // Round the total hours to 1 decimal place
            const roundedTotalHours = totalHours.toFixed(1);
            const roundedTotalMinutes = remainingMinutes.toFixed(1);

            return parseFloat(roundedTotalHours * 60) + parseFloat(roundedTotalMinutes);
        },
        calculateEndTime() {
            if (this.newJob.start && this.newJob.fabric && this.newJob.ptpuim) {
                const startTime = new Date(this.newJob.start);
                const fabric = parseFloat(this.newJob.fabric);
                const ptpuim = parseFloat(this.newJob.ptpuim);

                // Calculate the total time required in minutes
                const totalTimeInMinutes = fabric / ptpuim;

                // Calculate the end time by adding the total time to the start time
                const endTime = new Date(startTime.getTime() + totalTimeInMinutes * 60 * 1000);
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
                editable: {
                    add: true, // Allow adding new items
                    updateTime: false, // Disable editing item ranges directly
                    updateGroup: true, // Allow editing the group
                    remove: false, // Disable removing items
                },
                // editable: true,
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

        handleTimingChange(updatedJob) {
            // Show a confirmation dialog to the user
            const confirmation = window.confirm("You cannot adjust the timing from here.");

            if (confirmation) {
                // Redirect the user to the form to adjust timing
                // You can implement the redirection logic here
            } else {
                // Revert the timing change by updating the item in the items DataSet
                const existingJob = this.jobs.find(job => job.id === updatedJob.id);
                if (existingJob) {
                    this.items.update(existingJob); // Revert the timing change
                }
            }
        },

        onDataSetUpdate(event, items) {
            const dataItems = items.data;
            dataItems.forEach(itemData => {
                let jobIndex = this.jobs.findIndex(job => job.id === itemData.id);

                if (jobIndex !== -1) { // Check if job with given id exists
                    this.jobs[jobIndex].group = itemData.group;
                    this.jobs[jobIndex].start = new Date(itemData.start); // Convert to Date object if needed
                    this.jobs[jobIndex].end = new Date(itemData.end); // Convert to Date object if needed
                    this.handleTimingChange(this.jobs[jobIndex]); // Call the timing change handler
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
                fabric: job.fabric,
                start: job.start.toISOString().slice(0, -1),
                end: job.end.toISOString().slice(0, -1),
                group: job.group,
            };
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
                this.jobs.push({ ...this.newJob }); // Clone the object
                this.items.add(this.newJob); // Add the item to DataSet
            }

            // Reset the form fields
            this.newJob = {
                content: '',
                ptpuim: '',
                fabric: '',
                start: '',
                end: '',
                group: ''
            };
        }
        ,

        // addJob() {
        //     // Convert start and end to Date objects
        //     this.newJob.start = new Date(this.newJob.start);
        //     this.newJob.end = new Date(this.newJob.end);

        //     // Check if start, end, and group are empty and handle them as needed
        //     if (!this.newJob.start || !this.newJob.end || !this.newJob.group) {
        //         // Handle empty fields here, for example, set default values
        //         this.newJob.start = new Date(); // Set to the current date and time
        //         this.newJob.end = new Date();   // Set to the current date and time
        //         this.newJob.group = this.stations[0].id; // Set to the first station by default
        //     }

        //     if (this.newJob.id !== undefined) {
        //         // Update existing job
        //         const updatedJobIndex = this.jobs.findIndex(job => job.id === this.newJob.id);
        //         if (updatedJobIndex !== -1) {
        //             this.jobs[updatedJobIndex] = { ...this.newJob }; // Clone the object
        //             this.items.update(this.newJob); // Update the item in DataSet
        //         }
        //     } else {
        //         // Add new job
        //         this.newJob.id = this.jobs.length + 1; // Assign a unique ID
        //         this.jobs.push({ ...this.newJob }); // Clone the object
        //         this.items.add(this.newJob); // Add the item to DataSet
        //     }
        //     // Reset the form fields
        //     this.newJob = {
        //         content: '',
        //         ptpuim: '',
        //         fabric: '',
        //         start: '',
        //         end: '',
        //         group: ''
        //     };
        // },
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
                        fabric: '',
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
  