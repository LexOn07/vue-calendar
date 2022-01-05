import { data } from 'autoprefixer';
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
    <div class="body">
      <div v-for="count of getBeforeDaysCount()" :key="'dayItemBefore' + count" class="dayItem">
        <div class="dayItemText">{{getBeforeMounthCount(count)}}</div>
      </div>
      <div v-for="count of getDaysCount()" ref="dayItem" :key="'dayItem' + count" class="dayItem">
        <div class="dayItemText">{{count}}</div>
      </div>
      <div v-for="count of getAfterDaysCount()" :key="'dayItemAfter' + count" class="dayItem">
        <div class="dayItemText">{{count}}</div>
      </div>
    </div>
  </div>
</div>
</template>
<script>
export default {
  name: 'calendar',
  data() {
    return {
      dateObj: null,
      nameDay: ['Воскресенье', 'Понедельник', 'Вторник', 'Среда', 'Четверг', 'Пятница', 'Суббота'],
      nameMinDay: ['Вс', 'Пн', 'Вт', 'Ср', 'Чт', 'Пт', 'Сб'],
      nameMounth: ['Январь', 'Февраль', 'Март', 'Апрель', 'Май', 'Июнь', 'Август', 'Сентябрь', 'Октябрь', 'Ноябрь', 'Декабрь']
    }
  },
  props: {
    date: String,
    startDate: String,
    disableTime: Boolean,
    disableTitle: Boolean,
    enableNavButton: Boolean,
    enableManyDate: Boolean,
    enableHideDate: Boolean
  },
  mounted() {
    if (!this.startDate) this.startDate = this.date
    this.allDateToObj()
  },
  methods: {
    allDateToObj: function() {
      if (!this.date) {
        let date = new Date()
        this.date = date.toISOString()
      }
      this.checkingDisableTime()
      if (this.disableTime) {
        this.dateObj = new Date(this.date.split('-')[0], this.date.split('-')[1], this.date.split('-')[2])
      } else {
        this.dateObj = new Date(this.date)
      }
    },
    checkingDisableTime: function() {
      if (this.date.split('T')[1] && this.disableTime) {
        this.disableTime = false
        console.error('Warning! You use "this.disableTime" property, but the supplied data is yyyy-mm-dd"T"hh:mm:ss format. Use yyyy-mm-dd format!')
      } else if (!this.date.split('T')[1] && !this.disableTime) {
        this.disableTime = true
        console.error('Warning! You is not use "this.disableTime" property, but the supplied data is yyyy-mm-dd format. Use yyyy-mm-dd"T"hh:mm:ss format!')
      }
    },
    getDaysCount: function() {
      let date = new Date(this.dateObj)
      date.setDate(0)
      return date.getDate()
    },
    getBeforeDaysCount: function() {
      let date = new Date(this.dateObj)
      date.setDate(1)
      return date.getDay()
    },
    getAfterDaysCount: function() {
      let date = new Date(this.dateObj)
      let afterDate = new Date(this.dateObj)
      date.setDate(0)
      afterDate.setDate(date.getDate())
      return 6 - afterDate.getDay()
    },
    getBeforeMounthCount: function(iter) {
      let date = new Date(this.dateObj)
      date.setDate(1)
      let day = date.getDay()
      date.setMonth(date.getMonth() - 1)
      date.setDate(0)
      console.log(date.getDate())
      return date.getDate() - day + iter
    }
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
    align-items: center;
    margin-bottom: 10px;
    justify-content: space-between;
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
  }
  .body{
    width: 100%;
    display: flex;
    flex-wrap: wrap;
  }
  .dayTitle{
    color: peru;
    font-size: 16px;
    width: calc(100% / 7);
    margin: 5px 10px;
  }
  .dayItem{
    min-width: calc(100% / 11);
    margin: 5px 10px;
    flex: 1
  }
  .dayItemText{
    width: 30px;
    height: 30px;
    border: #678 solid 1px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
