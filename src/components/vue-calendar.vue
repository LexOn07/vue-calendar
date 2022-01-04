<template>
<div class="calendar">
  <div v-if="!disableTitle" class="calendar__head">
    <h5>Заголовок как пример</h5>
    <div v-if="enableNavButton" class="navigationBlock">
      <span class="navigationButton">{{'⮜'}}</span>
      <span class="navigationButton">{{'⮞'}}</span>
    </div>
  </div>
  <div class="calendar__body">
    <div class="calendar__bodyHead">
      <h6 v-for="(item, index) in nameMinDay" :key="'dayTitle' + index" class="dayTitle">{{item}}</h6>
    </div>
  </div>
</div>
</template>
<script>
export default {
  name: 'calendar',
  data() {
    return {
      date: null,
      nameDay: ['Воскресенье', 'Понедельник', 'Вторник', 'Среда', 'Четверг', 'Пятница', 'Суббота'],
      nameMinDay: ['Вс', 'Пн', 'Вт', 'Ср', 'Чт', 'Пт', 'Сб'],
      nameMounth: ['Январь', 'Февраль', 'Март', 'Апрель', 'Май', 'Июнь', 'Август', 'Сентябрь', 'Октябрь', 'Ноябрь', 'Декабрь']
    }
  },
  props: {
    // eslint-disable-next-line
    date: String,
    disableTime: Boolean,
    disableTitle: Boolean,
    enableNavButton: Boolean,
    enableManyDate: Boolean,
    enableHideDate: Boolean
  }
}
</script>
<style scoped>
  h5{
    font-family: Tahoma, Geneva, Verdana, sans-serif;
    font-weight: 500;
    font-size: 20px;
  }
  .calendar{}
  .calendar__head{
    display: flex;
    width: 100%;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;
  }
  .navigationBlock{
    display:flex
  }
  .navigationButton{
    font-size: 24px;
    cursor: pointer;
    margin: 0 6px;
  }
  .navigationButton:hover{
    color: palegreen;
  }
  .calendar__bodyHead{
    width: 100%;
    display: flex;
    justify-content: space-around;
  }
  .dayTitle{
    color: peru;
    font-size: 16px;
  }
</style>
