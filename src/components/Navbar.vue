<template>
    <div class="main-nav">
        <router-link :to="{ name: 'home'}">Tasks</router-link>
        <router-link :to="{ name: 'addTask'}">Create new task</router-link>
    </div>
</template>

<script>
export default {

}
</script>

<style>
.main-nav{
    text-align: center;
    margin: 40px auto ;
}
.main-nav a{
    display: inline-block;
    text-decoration: none;
    margin: 0 10px;
    color: #999;
    font-size: 18px;

}
.main-nav a.router-link-active {
    border-bottom: 2px solid #00ce89;
    padding-bottom: 4px;
}
</style>