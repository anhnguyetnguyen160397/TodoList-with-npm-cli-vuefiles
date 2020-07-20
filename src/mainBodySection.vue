<template>
    <div class='main'>
        <input id='toggle-all' class='toggle-all' type='checkbox' v-model="allDone">
        <label for='toggle-all' @click='allComplete'></label>
        <ul class='todo-list'>
            <li  :class='className(task)' v-for= 'task in filterTask'>
                <input type="checkbox" value="None" class="toggle" v-model="task.completed" name="check" @click='subtract(task)'/>
                <label><span>{{task.title}}</span></label>
                <button class="destroy" @click='removeTask(task)'></button>
            </li>
        </ul>
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
        },

        filterTask:{
            type: Array
        }
    },

    data(){
        return{
            newTask: '',
            toggleAll: false,
        }
    },

    methods:{
        allDone(value){
            this.tasks.forEach(function (task) {
                task.completed = value;
            });
        },

        allComplete(){
            this.taskCompletedNum=[];
            this.toggleAll=!this.toggleAll;
            for (var i = 0; i < this.tasks.length; i++){
                this.tasks[i].completed=this.toggleAll;
                if (this.tasks[i].completed){
                    this.taskCompletedNum.push('add');
                };
                if (!this.tasks[i].completed){
                    this.taskCompletedNum.pop();
                };
            };
            this.$emit('taskCompletedNum', this.taskCompletedNum);

        },

        className(task) {
            let classes=['toggle']
            if (task.completed) {
                classes.push('completed');
            }
            return classes;
        },

        removeTask(task){
            var index = this.tasks.indexOf(task);
            this.tasks.splice(index,1);
            this.taskCompletedNum=[];
        },

        subtract(task){
            if (task.completed){
                this.taskCompletedNum.pop()
            }
            if (!task.completed){
                this.taskCompletedNum.push('add')
            }
        }
    }
}
</script>
 
<style>

   .main {
        position: relative;
        z-index: 2;
        border-top: 1px solid #e6e6e6;
    }

    .toggle-all {
        text-align: center;
        border: none;
        opacity: 0;
        position: absolute;
    }

    .toggle-all + label {
        width: 60px;
        height: 34px;
        font-size: 0;
        position: absolute;
        top: -52px;
        left: -13px;
        -webkit-transform: rotate(90deg);
        transform: rotate(90deg);
    }

    .toggle-all + label:before {
        content: '❯';
        font-size: 22px;
        color: #e6e6e6;
        padding: 10px 27px 10px 27px;
    }

    .toggle-all:checked + label:before {
        color: #737373;
    }


    .todo-list {
        margin: 0;
        padding: 0;
        list-style: none;
    }

    .todo-list li {
        position: relative;
        font-size: 24px;
        border-bottom: 1px solid #ededed;
    }

    .todo-list li:last-child {
        border-bottom: none;
    }

    .todo-list li.editing {
        border-bottom: none;
        padding: 0;
    }

    .todo-list li.editing .edit {
        display: block;
        width: 506px;
        padding: 12px 16px;
        margin: 0 0 0 43px;
    }

    .todo-list li.editing .view {
        display: none;
    }

    .todo-list li .toggle {
        text-align: center;
        width: 40px;
        height: auto;
        position: absolute;
        top: 0;
        bottom: 0;
        margin: auto 0;
        border: none; 
        -webkit-appearance: none;
        appearance: none;
    }

    .todo-list li .toggle {
        opacity: 0;
    }

    .todo-list li .toggle + label {
        background-image: url('data:image/svg+xml;utf8,%3Csvg%20xmlns%3D%22http%3A//www.w3.org/2000/svg%22%20width%3D%2240%22%20height%3D%2240%22%20viewBox%3D%22-10%20-18%20100%20135%22%3E%3Ccircle%20cx%3D%2250%22%20cy%3D%2250%22%20r%3D%2250%22%20fill%3D%22none%22%20stroke%3D%22%23ededed%22%20stroke-width%3D%223%22/%3E%3C/svg%3E');
        background-repeat: no-repeat;
        background-position: center left;
    }


    .todo-list li label {
        word-break: break-all;
        padding: 15px 15px 15px 60px;
        display: block;
        line-height: 1.2;
        transition: color 0.4s;
    }

    .todo-list li .toggle:checked + label {
        background-image: url('data:image/svg+xml;utf8,%3Csvg%20xmlns%3D%22http%3A//www.w3.org/2000/svg%22%20width%3D%2240%22%20height%3D%2240%22%20viewBox%3D%22-10%20-18%20100%20135%22%3E%3Ccircle%20cx%3D%2250%22%20cy%3D%2250%22%20r%3D%2250%22%20fill%3D%22none%22%20stroke%3D%22%23bddad5%22%20stroke-width%3D%223%22/%3E%3Cpath%20fill%3D%22%235dc2af%22%20d%3D%22M72%2025L42%2071%2027%2056l-4%204%2020%2020%2034-52z%22/%3E%3C/svg%3E');
    }

    .todo-list li .destroy {
        display: none;
        position: absolute;
        top: 0;
        right: 10px;
        bottom: 0;
        width: 40px;
        height: 40px;
        margin: auto 0;
        font-size: 30px;
        color: #cc9a9a;
        margin-bottom: 11px;
        transition: color 0.2s ease-out;
    }

    .todo-list li .destroy:hover {
        color: #af5b5e;
    }

    .todo-list li .destroy:after {
        content: '×';
    }

    .todo-list li:hover .destroy {
        display: block;
    }

</style>
