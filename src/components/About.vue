<template>
    <div class="about">
        <h1>Welcome {{ user_name }}, this is an About page</h1>
        <p>Random lorem shit</p>
    </div>
</template>

<script>
export default {
    name: 'About',
    data(){
        return{
            user_name: this.$route.params.name
        }
    }
}
</script>
