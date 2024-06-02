<template>
    <div class="task" :class="{ complete: task.complete }">
        <div class="actions" @click="showDetailsToggle">
            <h2> {{ task.title  }}</h2>
            <div class="icons">
               <span class="material-icons">edit</span>
               <span class="material-icons"  @click="deleteTask">delete</span>
               <span class="material-icons tick" @click="compleTask" >done</span>

            </div>
        </div>
        <div class="details" v-if="showDetails" >
            <p> {{ task.details }} </p>
        </div>
    </div>
</template>

<script>
export default {
    props:['task'],
    data() {
        return {
            showDetails: false,
            uri:'http://localhost:3000/tasks/' + this.task.id
        }
    },
    methods:
    {
        showDetailsToggle(){
            this.showDetails = !this.showDetails
        },
        deleteTask(){
            fetch(this.uri, {method: 'DELETE'})
            .then(() =>this.$emit('delete', this.task.id))
            .catch(err => console.log(err.message))
        },
        compleTask(){
            fetch(this.uri, {
                method: 'PATCH',
                headers: { 'content-type': 'application/json'},
                body: JSON.stringify({complete: !this.task.complete})
            } )
            .then(()=>this.$emit('complete', this.task.id))
            .catch(err => console.log(err.message))
        }
    }
}
</script>

<style >
.task{
    margin: 20px auto;
    background: white;
    padding: 10px 20px;
    border-radius: 4px;
    border-left: 4px solid #e90074;
    box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.5);

}
h2 {
    cursor: pointer;
}
.actions {
    display: flex;
    justify-content: space-between;
    align-items: center;
}
.material-icons {
    margin-left:10px ;
    font-size: 24px;
    color: #bbb;
    cursor: pointer;
}
.material-icons:hover{
    color:#777
}
.task.complete {
    border-left: 4px solid #00ce89;
}
.task.complete .tick{
color:  #00ce89;
}

</style>