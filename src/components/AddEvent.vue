<template>
    <div>
        <p class="homeText">
            Syötä tehtävä
        </p>
        <form @submit.prevent="addTask">
            <label for="course">Course</label>
            <div>
                <input id="course" type="text" v-model="course" required autofocus>
            </div>

            <label for="task">Task</label>
            <div>
                <input id="task" type="text" v-model="task" required>
            </div>

            <label for="deadline">Password</label>
            <div>
                <input id="deadline" type="date" v-model="date" required>
            </div>

            <div>
                <input type="radio" name="done" id="one" value=true v-model="picked">
                <label for="one">done</label>
                <br>
                <input type="radio" name="done" id="two" value=false v-model="picked">
                <label for="two">not done yet</label>
            </div>

            <button>Add new task</button>
        </form>
    </div>
</template>
<script>
    import axios from 'axios';
    const baseURL = "http://localhost:3000/notes";

    export default {
        name: 'AddEvent',
        data() {
            return {
                options: [
                    {
                        value: true,
                        text: "yes"
                    },
                    {
                        value: false,
                        text: "no"
                    }],
                selected: 'no',
                course: '',
                task: '',
                date: '',
                done: false,
                newTask: {
                    course: '',
                    task: '',
                    date: '',
                    done: false,
                },
                picked: ''
            }

        },
        methods:{
            async addTask(){
                this.newTask.course=this.course;
                this.newTask.task=this.task;
                this.newTask.date= this.date;
                this.newTask.done= Boolean(JSON.parse(this.picked));
                axios.post(baseURL, this.newTask)
                    .then(res=>{
                        console.log(res);
                        this.course='';
                        this.task='';
                        this.date='';
                    console.log(this.task)}
                    )
            }
        }

    };
</script>
<style scoped>
    .homeText {
        font-size: 35px;
        color: red;
        text-align: center;
        position: relative;
        top: 30px;
        text-shadow: 2px 2px 2px gray;
    }
</style>
