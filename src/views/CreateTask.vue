<template>
    <form @submit.prevent="handelSubmit">
        <label for="title">Title:</label>
        <input type="text" v-model="title" required>
        <label for="details">Details:</label>
        <textarea  v-model="details" required></textarea>
        <button>Create Task</button>
    </form>
</template>
<script>
export default {
    data(){
        return {
            title: '',
            details:''
        }
    },
    methods:{
        handelSubmit(){
            let task = {
                title: this.title,
                details: this.details,
                complete: false,
            };
            fetch('http://localhost:3000/tasks', {
                method: 'POST',
                headers: {'content-type':'appplication/json'},
                body:JSON.stringify(task)
            }).then(()=>{
                this.$router.push('/')
            }).catch(err => console.log(err.message))

        }
    }

}
</script>
<style>
    form {
        background: white;
        padding: 20px;
        border-radius: 10px;
    }
    label{
        display: block;
        color: #bbb;
        text-transform: uppercase;
        font-size: 14px;
        font-weight: bold;
        margin: 20px 0 10px 0;
        letter-spacing: 1px;
    }
    input{
        padding: 10px;
        border: 0;
        border-bottom: 1px solid #ddd;
        width: 100%;
        box-sizing: border-box;
    }

    textarea{
        border: 1px solid #ddd;
        padding: 10px;
        width: 100%;
        height: 100px;
        box-sizing: border-box;

    }
    form button{
        display: block;
        margin: 20px auto 0;
        background: #00ce89;
        color: white;
        padding: 10px;
        border: 0;
        border-radius: 6px;
        font-size: 16px;
    }
</style>