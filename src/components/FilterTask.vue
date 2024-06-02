<template>
    <nav class="filter-nav">
        <button @click="updateFilter('all')" :class="{ active: current === 'all' }" >All Tasks</button>
        <button @click="updateFilter('completed')" :class="{ active: current === 'completed' }" >Completed Tasks</button>
        <button @click="updateFilter('ongoing')" :class="{ active: current === 'ongoing' }" >Ongoing Tasks</button>
    </nav>
</template>

<script>
export default {
    props:['current'],
    data(){
        return{

        }
    },
    methods:{
        updateFilter(by){
            this.$emit('filterChange', by)
        }
    }
}
</script>

<style>
 .filter-nav button{
    background: none;
    color: #bbb;
    font-size: 12px;
    outline: none;
    border: none;
    text-transform: uppercase;
    margin-right: 10px;
    letter-spacing: 1px;
    font-weight: bold;
    cursor: pointer;
 }
 .filter-nav button.active {
    color: #555;
 }
</style>