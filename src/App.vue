<template>
<div class="container">
    <Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask"/>
    <div v-if="showAddTask">
        <AddTask @add-task="addTask" />
    </div>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
</div>
</template>

<script>
import Header from './components/Header'
import Tasks from './components/Tasks'
import AddTask from './components/AddTask'

export default {
    name: 'App',
    components: {
        Header,
        Tasks,
        AddTask,
    },
    data() {
        return {
            tasks: [],
            showAddTask: false, // used to toggle add-task form
        }
    },
    methods: {
        toggleAddTask() {
            this.showAddTask = !this.showAddTask
        },
        addTask(newTask) {
            this.tasks = [...this.tasks, newTask]
        },
        deleteTask(id) {
            if (confirm('Are you sure?')) {
                // we want every task back except that task
                this.tasks = this.tasks.filter((task) => task.id !== id)
            }
        },
        toggleReminder(id) {
            this.tasks = this.tasks.map((task) =>
                // find task that was clicked and keeping the other properties, toggle only the reminder prop
                (task.id === id) ? {
                    ...task,
                    reminder: !task.reminder
                } : task
            )
        },
    },
    created() {
        this.tasks = [{
                id: 1,
                text: 'Doctors Appointment',
                day: 'March 1st at 2:30pm',
                reminder: true,
            },
            {
                id: 2,
                text: 'Meeting at School',
                day: 'March 6th at 11:00am',
                reminder: true,
            },
            {
                id: 3,
                text: 'Work Conference',
                day: 'April 2nd at 9am',
                reminder: false,
            },
            {
                id: 4,
                text: 'Rent Due',
                day: 'March 1st at 12:00pm',
                reminder: true,
            },
            {
                id: 5,
                text: 'Family Reunion',
                day: 'March 12th at 12:30',
                reminder: false,
            },
        ]
    }
}
</script>

// Global fonts here

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: 'Poppins', sans-serif;
}

.container {
    max-width: 500px;
    margin: 30px auto;
    overflow: auto;
    min-height: 300px;
    border: 1px solid steelblue;
    padding: 30px;
    border-radius: 5px;
}

.btn {
    display: inline-block;
    background: #000;
    color: #fff;
    border: none;
    padding: 10px 20px;
    margin: 5px;
    border-radius: 5px;
    cursor: pointer;
    text-decoration: none;
    font-size: 15px;
    font-family: inherit;
}

.btn:focus {
    outline: none;
}

.btn:active {
    transform: scale(0.98);
}

.btn-block {
    display: block;
    width: 100%;
}
</style>
