<template>
    <div class='footer' v-show='tasks.length'>
        <span class='todo-count'>{{number}} items left</span>
        <ul class='filters'>
            <li @click="eventChange('all')" :class='clicked()'>All</li>
			<li @click="eventChange('active')" :class='clickedActive()'>Active</li>
			<li @click="eventChange('complete')" :class='clickedCompleted()'>Completed</li>
        </ul>
        <button class='clear-completed' @click='removeCompleted'>Clear completed</button>
    </div>   
</template>
 
<script>
export default {
    props:{

        tasks:{
            type: Array
        },

        taskCompletedNum:{
            type: Array
        },

        visibility:{
            type: String
        }
    },

    data(){
        return{

        }
    },

    methods:{

        eventChange(val){
            this.visibility=val;
            this.$emit('changedVisibility',this.visibility)
        },

        removeCompleted(){
            this.tasks = this.active;
            this.taskCompletedNum=[];
            this.$emit('completedTasksRemoved',this.tasks);
            this.$emit('refreshTaskCompletedNum',this.taskCompletedNum);
            
        },

        clicked(){
            let classes=[];
            if (this.visibility=='all') {
                classes.push('active');
            }
            return classes;
            },

        clickedActive(){
            let classes=[];
            if(this.visibility=='active'){
                classes.push('active');
            }
            return classes;
        },

        clickedCompleted(){
            let classes=[];
            if(this.visibility=='complete'){
                classes.push('active');
            }
            return classes;
        },

    },
    computed:{
        number: function(){
            return this.tasks.length - this.taskCompletedNum.length ;
        },

        active: function(){
            return this.tasks.filter(function(task){
                return !task.completed
            });
        },  
    }
}
</script>
 
<style>

    .footer {
        color: #777;
        padding: 10px 15px;
        height: 20px;
        text-align: center;
        border-top: 1px solid #e6e6e6;
    }

    .footer:before {
        content: '';
        position: absolute;
        right: 0;
        bottom: 0;
        left: 0;
        height: 50px;
        overflow: hidden;
        box-shadow: 0 1px 1px rgba(0, 0, 0, 0.2),
                    0 8px 0 -3px #f6f6f6,
                    0 9px 1px -3px rgba(0, 0, 0, 0.2),
                    0 16px 0 -6px #f6f6f6,
                    0 17px 2px -6px rgba(0, 0, 0, 0.2);
    }

    .todo-count {
        float: left;
        text-align: left;
    }

    .filters {
        margin: 0;
        padding: 0;
        list-style: none;
        position: absolute;
        right: 0;
        left: 0;
    }

    .filters li {
        display: inline;
        color: inherit;
        margin: 3px;
        padding: 3px 7px;
        text-decoration: none;
        border: 1px solid transparent;
        border-radius: 3px;
    }

    .filters li:hover{
        border-color: rgba(175, 47, 47, 0.1);
    }

    .clear-completed,
    html .clear-completed:active {
        float: right;
        position: relative;
        line-height: 20px;
        text-decoration: none;
        cursor: pointer;
    }

    .clear-completed:hover {
        text-decoration: underline;
    }

    .active {
	    border-color: rgba(175, 47, 47, 0.2) !important;
    }

</style>
