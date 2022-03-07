<template>
    <footer>
        <p>Copyright &copy; 2022</p>
        <router-link to="/about" v-show="aboutPage"> About Page </router-link>
    </footer>
</template>

<script>
    export default {
        computed: {
            aboutPage () {
                if (this.$route.path === '/about') {
                    return false
                } else {
                    return true
                }
            }
        }
    }
</script>

<style scoped>
    a {
        color: #333;
    }
    footer {
        margin-top: 30px;
        text-align: center;
    }
</style>