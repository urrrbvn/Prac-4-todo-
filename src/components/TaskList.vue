<template>
    <!-- <button @click="console.log(this.days)" >TEST</button>-->
    <!-- <button @click="console.log(filteredDays)" >TEST</button>  -->

        <div class="dayContainer" v-for="elem in filteredDays" 
                                :key="elem.id"
                                @mouseover="elem.isHovered = true"
                                @mouseleave="elem.isHovered = false">
            <div class="dayTitle">{{ elem.title }}</div>
            <div class="dayTasks">
                <div class="task" v-for="task in elem.tasks"
                 :style="{backgroundColor: task.priority == 'Важно!' ? '#E74C3C' : '#1ABC9C'}"
                 @mouseover="this.taskHovered = true"
                 @mouseleave="this.taskHovered = false">
                    {{ task.text }}
                    <button class="deleteTask"
                    v-show="this.taskHovered"
                    @click="deleteTask(elem.id, task)">
                        +
                    </button>
                </div>
            </div>
            <button class="deleteDay"
                    v-show="elem.isHovered"
                    @click="deleteDay(elem.id)">
                    +</button>  
        </div> 

</template>

<script>
    export default{
        methods:{
            deleteDay(id){
                this.days[id-1].tasks.length = 0
            },
            deleteTask(id, task){
                this.days[id-1].tasks = this.days[id-1].tasks.filter(elem => elem.text == task.text && elem.priority == task.priority && elem.day == task.day )
                console.log(this.days[id-1].tasks)
                console.log(this.filteredDays)
            }
        },
        props:['taskArray'],
        data(){
            return{
                days:[
                    {id:1, title:'ПН', tasks:[], isHovered: false},
                    {id:2, title:'ВТ', tasks:[], isHovered: false},
                    {id:3, title:'СР', tasks:[], isHovered: false},
                    {id:4, title:'ЧТ', tasks:[], isHovered: false},
                    {id:5, title:'ПТ', tasks:[], isHovered: false},
                    {id:6, title:'СБ', tasks:[], isHovered: false},
                    {id:7, title:'ВС', tasks:[], isHovered: false}
                ],
                taskHovered: false
            }
        },
        watch:{
            taskArray:{
                handler(newVal){
                    if(newVal[newVal.length - 1].day == 'Понедельник'){
                        this.days[0].tasks.push(newVal[newVal.length - 1])
                    }else if(newVal[newVal.length - 1].day == 'Вторник'){
                        this.days[1].tasks.push(newVal[newVal.length - 1])
                    }else if(newVal[newVal.length - 1].day == 'Среда'){
                        this.days[2].tasks.push(newVal[newVal.length - 1])
                    }else if(newVal[newVal.length - 1].day == 'Четверг'){
                        this.days[3].tasks.push(newVal[newVal.length - 1])
                    }else if(newVal[newVal.length - 1].day == 'Пятница'){
                        this.days[4].tasks.push(newVal[newVal.length - 1])
                    }else if(newVal[newVal.length - 1].day == 'Cуббота'){
                        this.days[5].tasks.push(newVal[newVal.length - 1])
                    }else if(newVal[newVal.length - 1].day == 'Воскресенье'){
                        this.days[6].tasks.push(newVal[newVal.length - 1])
                    }

                },
                deep: true
            }
        },
        computed:{
            filteredDays(){
                return this.days.filter(day => day.tasks.length !== 0)
            }
        }
    }

</script>

<style>
    .deleteDay{
        border: 0.5px solid black;
        border-radius: 50%;

        font-size: 28px;
        font-weight: 200;
        transform: rotate(45deg);

        position: relative;
        top: -10px;
        right: -10px;
        width: 28px;
        height: 28px;
        background-color: red;

        display: flex;
        align-items: center;
        justify-content: center;

        /* margin: -28px; */
    }
    .deleteTask{
        border: 0.5px solid black;
        border-radius: 50%;

        font-size: 28px;
        font-weight: 200;
        transform: rotate(45deg);

        position: relative;
        top: -10px;
        right: -10px;
        width: 28px;
        height: 28px;
        background-color: red;
        /* background-image: url(../assets/Group\ 13.png); */
        display: flex;
        align-items: center;
        justify-content: center;
    }
    .dayContainer{

        margin-top: 43px;
        width: 1038px; 
        height: fit-content;
        display: flex;
        flex-direction: row;
        background-color: #ECF0F1;
        border-radius: 20px;
        font-family: 'Inter', sans-serif;
    }
    /* .dayContainer::before{
        content: "";
        position: relative;
        top: 20px;
        left: 1110px;
        width: 50px;
        height: 50px;
        margin: -50px;
    } */
    .dayTitle{
        width: 80px;
        /* height: inherit; */
        color: white;
        background-color: #34495E;
        text-align: center;
        border-radius: 20px 0 0 20px;
        display: flex;
        align-items: center;
        justify-content: center;
        font-weight: 400;
        font-size: 30px;
    }
    .dayTasks{
        width: 100%;
        height: fit-content;
        display: flex;
        align-items: center;
        flex-wrap: wrap;
        background-color: #ECF0F1;
        border-radius: 0 20px 20px 0;
        padding-bottom: 15px;

    }
    .task{
        width: fit-content;
        height: 47px;
        padding-left: 17px;
        padding-right: 17px;
        font-size: 30px;
        margin-left: 17px;
        margin-top: 17px;
        /* text-align: center; */
        color: #ECF0F1;
        display: flex;
        align-items: center;
        justify-content: center;
    }
</style>