<template>
    <div id='header'>
        <h1>todos</h1>
        <input type ='text' class='new-todo' placeholder='What needs to be done?' v-model='newTask' @keyup.enter='addTask' >
    </div>
</template>
 
<script>
export default {
    props:{
        tasks:{
            type: Array
        }
    },

    data(){
        return{
            newTask: '',
        }
    },

    methods:{
        addTask() {
            if (this.newTask) {
                this.tasks.push({
                    title: this.newTask,
                    completed: false
                });
                this.newTask = '';
            }
        },
    }
}
</script>
 
<style>
    .todoapp input::-webkit-input-placeholder {
        font-style: italic;
        font-weight: 300;
        color: #e6e6e6;
    }

    .todoapp input::-moz-placeholder {
        font-style: italic;
        font-weight: 300;
        color: #e6e6e6;
    }

    .todoapp input::input-placeholder {
        font-style: italic;
        font-weight: 300;
        color: #e6e6e6;
    }

    .new-todo {
        position: relative;
        margin: 0;
        width: 100%;
        font-size: 24px;
        font-family: inherit;
        font-weight: inherit;
        line-height: 1.4em;
        border: 0;
        color: inherit;
        padding: 6px;
        border: 1px solid #999;
        box-shadow: inset 0 -1px 5px 0 rgba(0, 0, 0, 0.2);
        box-sizing: border-box;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
    }

    .new-todo {
        padding: 16px 16px 16px 60px;
        border: none;
        background: rgba(0, 0, 0, 0.003);
        box-shadow: inset 0 -2px 1px rgba(0,0,0,0.03);
    }
</style>
