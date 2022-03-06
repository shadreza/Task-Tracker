<template>
    <div>
        <header>
            <!-- <h1>Task Tracker</h1> -->
            <h1>{{ title }}</h1>
            <Button @toggle-show-add-task="toggleShowAddTask" :text='text' :color="color"/>
        </header>
    </div>
</template>

<script>

    import Button from "@/components/Button.vue";

    export default {
        name: 'Header', 
        props: {
            title : String,
            showAddTask : Boolean,
        }, 
        data () {
            return {
                text : 'Add Task',
                color : 'black',
            }
        },
        components: {
            Button
        },
        methods: {
            toggleShowAddTask() {
                this.text = this.showAddTask ? 'Add Task' : "Close"
                this.color = this.showAddTask ? 'black' : "red"
                this.$emit('toggle-show-add-task')
            }
        },
    }
</script>

<style scoped>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        margin-bottom: 20px;
    }
</style>