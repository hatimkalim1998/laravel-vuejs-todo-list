<template>
    <div class="todoListContainer">
        <div class="heading">
            <h2 class="title">Todo List</h2>
            <add-item-from v-on:reloadlist="getList()" />
        </div>
        <list-view :items="items" 
        v-on:reloadlist="getList()"
        />
    </div>
</template>

<script>
import addItemFrom from "./addItemForm.vue"
import listView from './listView.vue'
export default {
    components: {
        addItemFrom,
        listView
    },
    data:function(){
        return {
            items:[]
        }
    },
    methods:{
        getList(){
            axios.get('api/items')
            .then(response=>{
                this.items=response.data
            })
            .catch(error=>{
                console.log(error);
            })
        }
    },
    created(){
        this.getList();
    }
}
</script>

<style scoped>
    .todoListContainer{
        width:500px;
        margin:auto;
        font-family: Arial, Helvetica, sans-serif;
    }
    .heading{
        background-color: #e6e6e6;
        padding: 10px;
    }
    .title{
        text-align: center;
    }
</style>  