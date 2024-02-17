<template>
    <div>
        <div id="visualization"></div>
    
        <button @click="showAddForm">Add Item</button>

        <div v-if="showForm">
            <h3>Add New Item</h3>
            <form @submit.prevent="addItemWithForm">
                <label for="content">Content:</label>
                <input v-model="newItem.content" id="content" type="text" required><br>
                <label for="start">Start Date:</label>
                <input v-model="newItem.start" id="start" type="date" required><br>
                <label for="end">End Date:</label>
                <input v-model="newItem.end" id="end" type="date"><br>
                <button type="submit">Add</button>
                <button @click="cancelAddForm">Cancel</button>
            </form>
        </div>
    </div>
</template>
  
  
  
  
  
<script>
import vis from 'vis-timeline/standalone/umd/vis-timeline-graph2d.min.js';
import 'vis-timeline/styles/vis-timeline-graph2d.min.css';

export default {
    data() {
        return {
            timelineItems: [
                { id: 1, content: 'item 1', start: '2023-04-20' },
                { id: 2, content: 'item 2', start: '2023-04-14' },
                { id: 3, content: 'item 3', start: '2023-04-18' },
                { id: 4, content: 'item 4', start: '2023-04-16', end: '2023-04-19' },
                { id: 5, content: 'item 5', start: '2023-04-25' },
                { id: 6, content: 'item 6', start: '2023-04-27', type: 'point' },
            ],
            showForm: false,
            newItem: {
                content: '',
                start: '',
                end: '',
            },
        };
    },
    mounted() {
        this.initializeTimeline();
    },
    methods: {
        initializeTimeline() {
            const container = document.getElementById('visualization');
            this.items = new vis.DataSet(this.timelineItems);

            const options = {
                onItemClicked: this.onItemClicked,
            };

            this.timeline = new vis.Timeline(container, this.items, options);
        },
       
        showAddForm() {
            this.showForm = true;
            this.newItem = {
                content: '',
                start: '',
                end: '',
            };
        },
        cancelAddForm() {
            this.showForm = false;
        },
        addItemWithForm() {
            // Validate the form input here if needed
            const newId = Math.max(...this.timelineItems.map(item => item.id)) + 1;
            this.timelineItems.push({
                id: newId,
                content: this.newItem.content,
                start: this.newItem.start,
                end: this.newItem.end,
            });
            this.items.clear();
            this.items.add(this.timelineItems);
            this.showForm = false;
        },
       
    },
};
</script>
  
  
<style scoped>
/* Add any custom styles for your component here */
#visualization {
    width: 600px;
    height: 400px;
    border: 1px solid lightgray;
}
</style>
  