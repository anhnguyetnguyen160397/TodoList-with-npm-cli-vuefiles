<template>

    <div>
        <headerSection v-bind:tasks='tasks'></headerSection>
        <mainBodySection :tasks='tasks' 
                         :taskCompletedNum='taskCompletedNum' 
                         :visibility='visibility' 
                         :filterTask='filterTask' 
                         @taskCompletedNum='taskCompletedNumEmit'>
        </mainBodySection>
        <footerSection :tasks='tasks' 
                       :taskCompletedNum='taskCompletedNum' 
                       :visibility='visibility' 
                       @changedVisibility='changedVisibility' 
                       @completedTasksRemoved='completedTasksRemoved' 
                       @refreshTaskCompletedNum='refreshTaskCompletedNum'>
        </footerSection>

    </div>
</template>

<script>
import headerSection from './headerSection.vue'
import mainBodySection from './mainBodySection.vue'
import footerSection from './footerSection.vue'
export default {
    components:{
        headerSection,
        mainBodySection,
        footerSection
    },
    data(){
        return{
            taskCompletedNum:[],
            visibility:'all',
            tasks:[]
        }
    },

    computed: {

        active: function(){
            return this.tasks.filter(function(task){
                return !task.completed
            });
        },

        filterTask: function(){
            if(this.visibility == 'all'){
                return this.tasks
            }else if(this.visibility == 'active'){
                return this.tasks.filter(function(task){
                    return !task.completed
                });
            }else{
                return this.tasks.filter(function (task) {
                    return task.completed;
                });
            }
        }

    },

    methods: {

        changedVisibility (value) {
            this.visibility = value;
        },

        completedTasksRemoved(value){
            this.tasks = value;
        },

        refreshTaskCompletedNum(value){
            this.taskCompletedNum = value;
        },

        taskCompletedNumEmit(value){
            this.taskCompletedNum = value;
        }
    },
}
</script>
 
<style>


    html,
    body {
        margin: 0;
        padding: 0;
    }

    button {
        margin: 0;
        padding: 0;
        border: 0;
        background: none;
        font-size: 100%;
        vertical-align: baseline;
        font-family: inherit;
        font-weight: inherit;
        color: inherit;
        -webkit-appearance: none;
        appearance: none;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
    }

    body {
        font: 14px 'Helvetica Neue', Helvetica, Arial, sans-serif;
        line-height: 1.4em;
        background: #f5f5f5;
        color: #4d4d4d;
        min-width: 230px;
        max-width: 550px;
        margin: 0 auto;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        font-weight: 300;
    }

    :focus {
        outline: 0;
    }

    .todoapp h1 {
        position: absolute;
        top: -155px;
        width: 100%;
        font-size: 100px;
        font-weight: 100;
        text-align: center;
        color: rgba(175, 47, 47, 0.15);
        -webkit-text-rendering: optimizeLegibility;
        -moz-text-rendering: optimizeLegibility;
        text-rendering: optimizeLegibility;
    }


    .completed {
        color: #d9d9d9;
        text-decoration: line-through;
    }


    @media screen and (-webkit-min-device-pixel-ratio:0) {
        .toggle-all,
        .todo-list li .toggle {
            background: none;
        }

        .todo-list li .toggle {
            height: 40px;
        }
    }

    @media (max-width: 430px) {
        .footer {
            height: 50px;
        }

        .filters {
            bottom: 10px;
        }
    }

</style>