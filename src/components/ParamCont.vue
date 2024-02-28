<template>
    <div class="inputContainer">
            <div class="firstSector">
                <div class="selector">
                    <select v-model="selectedDay">
                        <option disabled value="">Выберите день недели</option>
                        <option v-for="day in daysOfWeek" :key="day" :value="day">
                            {{ day }}
                        </option>
                    </select>
                    <!-- <p>Выбранный день: {{ selectedDay }}</p> -->
                </div>
                <div class="selector">
                    <select v-model="selectedPriority">
                        <option disabled value="">Выберите день важность</option>
                        <option v-for="lvl in PriorityLvl" :key="lvl" :value="lvl">
                            {{ lvl }}
                        </option>
                    </select>
                    <!-- <p>Уровень важности: {{ selectedPriority }}</p> -->
                </div>
            </div>
            <div class="secondSector">
                <div class="taskDescription">
                    <input type="text" v-model="taskText">
                </div>
                <div class="btnCont">
                    <button @click="addNewTask" >Создать</button>
                </div>
            </div>
    </div>
</template>

<script>
    export default{
        data() {
    return {
      selectedDay: '',
      daysOfWeek: ['Понедельник', 'Вторник', 'Среда', 'Четверг', 'Пятница', 'Суббота', 'Воскресенье'],
      selectedPriority:'',
      PriorityLvl:['Важно!','Не важно'],
      taskText:'',
      taskObject:{day:'',priority:'',text:''}
    }
  },
  emits:[
    'newTaskCreated'
  ],
  methods:{
    addNewTask(){
        this.taskObject.day = this.selectedDay
        this.taskObject.priority = this.selectedPriority
        this.taskObject.text = this.taskText
        this.$emit('newTaskCreated', this.taskObject)
        this.taskObject = {day:'',priority:'',text:''}
    },
  },
}
</script>

<style scoped>
    select{
        font-size: 20px;
    }
    button{
        font-size: 20px;
        font-family: 'Inter', sans-serif;
    }
    .inputContainer{
        width: 1088px;
        height: 179px;
        border-radius: 20px;
        background-color: #ECF0F1;
        border: 1px solid black;
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        margin-top: 79px;
    }
    .firstSector{
        width: 963px;
        height: 45px;
        display: flex;
        flex-direction: row;
        margin-bottom: 24px;
    }
    .secondSector{
        width: 963px;
        display: flex;
        flex-direction: row;
        justify-content: space-between;
    }
    .selector{
        width:257px ;
        margin-right: 34px;
    }
    select{
        width: 257px;
        height: 45px;
    }
    .taskDescription{
        width: 548px;
        height: 45px;
        background-color: white;
    }
    input{
        width: 530px;
        height: 45px;
        border: 1px solid black;
        padding-left: 17px;
        font-size: 20px;
    }
    .btnCont{
        width: 163px;
        height: 45px;
        display: flex;
        align-items: center;
    }
    button{
        width: 163px;
        height: 45px;
        background-color: #1ABC9C;
        border-radius: 23px;
        color: white;
    }
</style>