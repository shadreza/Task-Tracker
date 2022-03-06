<template>
    <button 
        :style="{background: color}" 
        class="btn" 
        @click="$emit('toggle-show-add-task')"
    >
        {{text}}
    </button>

</template>

<script>
    export default {
        name: 'Button',
        props: {
            text: String,
            color: String,
        },
    }
</script>

<style scoped>

</style>