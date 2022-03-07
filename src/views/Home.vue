<template>
    <div>
        <div v-if="showAddTask">
            <AddTask @add-task="addTask"/>
        </div>
        <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
    </div>
</template>

<script>

    import Tasks from "@/components/Tasks.vue";
    import AddTask from "@/components/AddTask.vue";

    export default {
        name: 'Home',
        components: {
            Tasks,
            AddTask,
        },
        methods : {
            async deleteTask (id) {
                if (confirm('Are you sure?') ) {
                    const res = await fetch(`api/tasks/${id}`, {
                    method: 'DELETE',
                    })
                    res.status === 200 ? 
                    this.tasks = this.tasks.filter(t => t.id !== id) 
                    : alert('Some Error Occurred During Deletion')
                    
                }
            },
            async toggleReminder (id) {

                const taskToToggle = await this.fetchTask(id)
                taskToToggle.reminder = !taskToToggle.reminder

                const res = await fetch(`api/tasks/${id}`, {
                    method: 'PUT',
                    headers: { 'Content-Type': 'application/json' },
                    body: JSON.stringify(taskToToggle)
                })

                const data = await res.json()

                res.status != 200 ?
                    alert('There was an error while updating the data')
                    :
                    this.tasks.forEach(task => {
                    if(task.id === id) {
                        task.reminder = ! task.reminder
                    }
                    })

            },
            async addTask (task) {
                const res = await fetch('api/tasks', { 
                    method : 'POST',
                    headers : {
                    'Content-Type' : 'application/json',
                    },
                    body : JSON.stringify(task)
                })
                const data = await res.json()
                this.tasks.push(data);
            },
            async fetchTasks () {
                const res = await fetch('api/tasks')
                const data = await res.json()
                return data
            },
            async fetchTask (id) {
                const res = await fetch(`api/tasks/${id}`)
                const data = await res.json()
                return data
            }
        },
        async created () {
            this.tasks = await this.fetchTasks()
        },
        data () {
            return {
                tasks: [],
            }
        },
        props: {
            showAddTask: Boolean,
        }
    }
</script>

<style scoped>

</style>