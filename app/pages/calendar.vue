<script setup>
  import moment from 'moment-timezone';

  const today = computed(() => moment());
  let curdt = ref(moment());
  let lastdayOfMonth = computed(() => curdt.value.clone().endOf('month').date());
  let days = computed(() => {
    let mdays = [];
    let wd = curdt.value.weekday();
    for (let w=0; w < wd; w++) mdays.push('*');
    for (let d=1; d <= lastdayOfMonth.value; d++) {
        mdays.push(d);
    }
    return mdays;
  });
  let startyr;
  let years = computed(() => {
    let arr = [];
    startyr = curdt.value.year() - curdt.value.year() % 10 + 1;
    for (let y=0; y < 10; y++) {
        arr.push(startyr+y);
    }
    return arr;
  })
  const setstartyear = (delta) => {
    const yr = curdt.value.clone().year()
    curdt.value = curdt.value.clone().year(yr+delta);
  }
  const setmonth = (m) => {
    curdt.value = curdt.value.clone().month(m);
  }
  const setyear = (y) => {
    curdt.value = curdt.value.clone().year(y);
  }
</script>

<template>
    <div class="dflex align-center">
        <h2 class="mr-md">Calendar</h2>
        <div class="dflex"><strong>{{curdt.format("MMMM YYYY")}}</strong> &raquo; <button @click="curdt=moment()">Today</button></div>
    </div>
    <div style="line-height: 2;">
        <label>Select year:</label>
        <div style="margin:1vh auto;display: flex;flex-wrap:wrap;gap:1rem;">
            <button @click="setstartyear(-20)">&laquo;</button>
            <button @click="setstartyear(-10)">&lsaquo;</button>
            <button @click="setyear(y)" v-for="y in years">{{y}}</button>
            <button @click="setstartyear(10)">&rsaquo;</button>
            <button @click="setstartyear(20)">&raquo;</button>
        </div>
        <div style="margin:1vh auto;display:flex;flex-wrap: wrap;gap:1rem;">
            <button v-for="(mo,idx) in moment.months()" @click="setmonth(idx)">{{mo}}</button>
        </div>
        <div style="display: grid;grid-template-columns: repeat(7,1fr);gap:1rem;">
            <span class="weekday" v-for="mo in ['Sun','Mon','Tue','Wed','Thu','Fri','Sat']">{{mo}}</span>
        </div>
        <div style="display: grid;grid-template-columns: repeat(7,1fr);gap:1rem;text-align: center;">
            <span v-for="d in days">{{d}}</span>
        </div>
    </div>
</template>

<style>
    button {
        padding: 0.25rem 0.5rem;
    }
    .weekday {
        text-align: center;
        padding: 0.5rem;
        gap: 1rem;
        background-color: lightblue;
    }
</style>