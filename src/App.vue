<template>
    <div id="app">
        <h2>
            Vue To Do List
            Simple Todo List with adding and filter by diff status.
        </h2>
         <CreateForm @addNewToDo="handleAddNewToDo"></CreateForm>
        <div id="list">
            <ul>
                <li v-for="(item,index) in filteredTodoList" :key="index">
                    <input type="checkbox" @click="changeStatus(item)" />{{item.content}}
                </li>
            </ul>
        </div>
        <div id="filter">
            当前状态：{{currentFilter}}
            <button :class="{selected: type == 0}" @click="handleStatusUpdate('all')">All</button>
            <button :class="{selected: type == 1}" @click="handleStatusUpdate('active')">Active</button>
            <button :class="{selected: type == 2}" @click="handleStatusUpdate('completed')">Completed</button>
        </div>
       
    </div>
</template>

<script>
    import CreateForm from "./components/CreateForm.vue";
    export default {
       
        name: 'app',
        components: {
           CreateForm
        },
        data: function () {
            return {
                /**
                 * 定义了 todo item 中属性为 {content:'吃饭',status:'active'}
                 * 定义了 todo 的两种状态 completed、active，默认为 active
                 */
                todoList: [
                    // {content:"吃饭", status:'completed'},
                    // {content:"看电影", status:'active'},
                    // {content:"撸猫", status:'active'}
                ],
                currentFilter: 'active',
            }
        },
        methods:{
            handleStatusUpdate:function(status){
                this.currentFilter = status;
            },
            handleAddNewToDo: function(inputtingText){
                this.todoList.push({
                    content: inputtingText,
                    status: "active"
                });
                
           },
           changeStatus: function(item){
               item.status = 'completed'
           }
            
        },
        computed:{
            filteredTodoList:function(){
                let fileredList = [];
                console.log("66",this.currentFilter);
                console.log("67",this.todoLis)
                // for (let index = 0; index < this.todoList.length; index++) {
                //     const element = this.todoList[index];
                //     if(element.status === this.currentFilter || this.currentFilter === "all"){

                //         fileredList.push(element);
                //     }
                        
                // }
                return this.todoList.filter(element => element.status===this.currentFilter || this.currentFilter === "all");
                // return fileredList;
            }

        }
    }
</script>

<style>
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }

    .items {
        list-style: none;
        text-align: left;
        line-height: 30px;
    }

    .items li.completed {
        text-decoration: line-through;
    }

    .filter a {
        margin: 0 10px;
        line-height: 30px;
    }

    .filter a.active {
        color: #f60;
        border: 1px solid #ccc;
        border-radius: 2px;
        padding: 3px;
        cursor: pointer;
    }
    .bottom div {
        padding: 10px;
        margin: 5px 10px;
        color: #fc999b;
    }
    .bottom div:hover  {
        border: 1px solid;
        border-radius: 3px;
        cursor: pointer;
    }
    .selected {
        border: 1px solid;
        border-radius: 3px;
        cursor: pointer;
    }
</style>
