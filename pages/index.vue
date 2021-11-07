
<template>
  <div>
    <vc-date-picker v-model="date"/>
    <div>
    <span>{{formatDate(date)}}</span>の<input type="number" v-model="adddate"/>日後の日付は
    <p><strong>{{addDate(date, adddate)}}</strong></p>

    <p>履歴</p>
    <ul>
      <li v-for="item in history" v-bind:key="item">{{item}}</li>
    </ul>
    </div>
  </div>
</template>

<script>
import Vue from 'vue';
import VCalendar from 'v-calendar';
import moment from 'moment';

// Use v-calendar & v-date-picker components
Vue.use(VCalendar, {
  componentPrefix: 'vc',  // Use <vc-calendar /> instead of <v-calendar />
});

// moment config
moment.locale("ja");

export default {
  data() {
    return {
      date: new Date(),
      adddate: 1,
      history: []
    }
  },
  methods: {
    addDate: function(date, adddate){
      return moment(date).add(adddate, 'days').format('YYYY年MM月DD日(ddd)');
    }, 
    formatDate: function(date){
      return moment(date).format('YYYY年MM月DD日(ddd)');
    }, 
    addHistory: function(text){
      this.history.unshift(text);
    }
  },
  watch: {
    date: function(newvalue, oldvalue){
      let text = this.formatDate(newvalue)+"の"+this.adddate+"日後は"+this.addDate(newvalue, this.adddate);
      this.addHistory(text);
    }
  }
}
</script>
