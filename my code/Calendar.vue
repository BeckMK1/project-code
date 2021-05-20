<template>
  <div class="celender-wrapper">
    <div class="row">
      <div class="tile lt-coner">mo</div>
      <div class="tile">tu</div>
      <div class="tile">we</div>
      <div class="tile">th</div>
      <div class="tile">fr</div>
      <div class="tile">sa</div>
      <div class="tile rt-coner">su</div>
    </div>
    <div class="row">
      <div :id="_uid + 'days'" @click="$event.target.classList.toggle('working'), days.day1=!day1,sendDays ()" class="tile weekday">1</div>
      <div @click="$event.target.classList.toggle('working'), days.day2=!day2,sendDays ()" class="tile weekday">2</div>
      <div @click="$event.target.classList.toggle('working'), days.day3=!day3,sendDays ()" class="tile weekday">3</div>
      <div @click="$event.target.classList.toggle('working'), days.day4=!day4,sendDays ()" class="tile weekday">4</div>
      <div @click="$event.target.classList.toggle('working'), days.day5=!day5,sendDays ()" class="tile weekday">5</div>
      <div @click="$event.target.classList.toggle('working'), days.day6=!day6,sendDays ()" class="weekend tile">6</div>
      <div @click="$event.target.classList.toggle('working'), days.day7=!day7,sendDays ()" class="weekend tile">7</div>
    </div>
    <div class="row">
      <div @click="$event.target.classList.toggle('working'), days.day8=!day8,sendDays ()" class="tile weekday">8</div>
      <div @click="$event.target.classList.toggle('working'), days.day9=!day9,sendDays ()" class="tile weekday">9</div>
      <div @click="$event.target.classList.toggle('working'), days.day10=!day10,sendDays ()" class="tile weekday">10</div>
      <div @click="$event.target.classList.toggle('working'), days.day11=!day11,sendDays ()" class="tile weekday">11</div>
      <div @click="$event.target.classList.toggle('working'), days.day12=!day12,sendDays ()" class="tile weekday">12</div>
      <div @click="$event.target.classList.toggle('working'), days.day13=!day13,sendDays ()" class="weekend tile">13</div>
      <div @click="$event.target.classList.toggle('working'), days.day14=!day14,sendDays ()" class="weekend tile">14</div>
    </div>
    <div class="row">
      <div @click="$event.target.classList.toggle('working'), days.day15=!day15,sendDays ()" class="tile weekday">15</div>
      <div @click="$event.target.classList.toggle('working'), days.day16=!day16,sendDays ()" class="tile weekday">16</div>
      <div @click="$event.target.classList.toggle('working'), days.day17=!day17,sendDays ()" class="tile weekday">17</div>
      <div @click="$event.target.classList.toggle('working'), days.day18=!day18,sendDays ()" class="tile weekday">18</div>
      <div @click="$event.target.classList.toggle('working'), days.day19=!day19,sendDays ()" class="tile weekday">19</div>
      <div :id="_uid + 'day'" @click="$event.target.classList.toggle('working'), days.day20=!day20,sendDays ()" class="weekend tile">20</div>
      <div @click="$event.target.classList.toggle('working'), days.day21=!day21,sendDays ()" class="weekend tile">21</div>
    </div>
    <div class="row">
      <div @click="$event.target.classList.toggle('working'), days.day22=!day22,sendDays ()" class="tile weekday">22</div>
      <div @click="$event.target.classList.toggle('working'), days.day23=!day23,sendDays ()" class="tile weekday">23</div>
      <div @click="$event.target.classList.toggle('working'), days.day24=!day24,sendDays ()" class="tile weekday">24</div>
      <div @click="$event.target.classList.toggle('working'), days.day25=!day25,sendDays ()" class="tile weekday">25</div>
      <div @click="$event.target.classList.toggle('working'), days.day26=!day26,sendDays ()" class="tile weekday">26</div>
      <div :id="_uid + 'day'" @click="$event.target.classList.toggle('working'), days.day27=!day27,sendDays () " class="weekend tile">27</div>
      <div :id="_uid + 'day'" @click="$event.target.classList.toggle('working'), days.day28=!day28,sendDays ()" class="weekend tile">28</div>
    </div>
    <div class="row">
      <div @click="$event.target.classList.toggle('working'), days.day29=!day29,sendDays ()" class="weekday tile lb-coner">29</div>
      <div @click="$event.target.classList.toggle('working'), days.day30=!day30,sendDays ()" class="tile weekday">30</div>
      <div @click="$event.target.classList.toggle('working'), days.day31=!day31,sendDays ()" class="tile weekday">31</div>
      <div @click="$event.target.classList.toggle('working'), days.day1=!day1,sendDays ()" class="tile weekday">1</div>
      <div @click="$event.target.classList.toggle('working'), days.day1=!day2,sendDays ()" class="tile weekday">2</div>
      <div @click="$event.target.classList.toggle('working'), days.day1=!day3,sendDays ()" class="weekend tile">3</div>
      <div @click="$event.target.classList.toggle('working'), days.day1=!day4,sendDays ()" class="weekend tile rb-coner">4</div>
    </div>
  </div>
</template>
<script>
export default {
  props: {
    weekend: {
      type: Boolean,
      default: false
    },
    weekday: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      days: {
        day1: false,
        day2: false,
        day3: false,
        day4: false,
        day5: false,
        day6: false,
        day7: false,
        day8: false,
        day9: false,
        day10: false,
        day11: false,
        day12: false,
        day13: false,
        day14: false,
        day15: false,
        day16: false,
        day17: false,
        day18: false,
        day19: false,
        day20: false,
        day21: false,
        day22: false,
        day23: false,
        day24: false,
        day25: false,
        day26: false,
        day28: false,
        day29: false,
        day30: false,
        day31: false
      }
    };
  },
  watch: {
    weekend () {
      if (this.weekend) {
        document.querySelectorAll('.weekend').forEach(work =>
          work.classList.add('working'));
      } else {
        document.querySelectorAll('.weekend').forEach(work =>
          work.classList.remove('working'));
      }
    },
    weekday () {
      if (this.weekday) {
        document.querySelectorAll('.weekday').forEach(work =>
          work.classList.add('working'));
      } else {
        document.querySelectorAll('.weekday').forEach(work =>
          work.classList.remove('working'));
      }
    }
  },
  methods: {
    sendDays () {
      this.$emit('click', this.days);
    }
  }
};
</script>
<style lang="scss" scoped>
.celender-wrapper {
  width: 330px;
}
.row {
  font-size: 12px;
  display: flex;
  flex-direction: row;
  font-weight: bold;
  width: fit-content;
}
.tile {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 46px;
  border: #275353 solid 1px;
  height: 46px;
  user-select: none;
  text-transform: uppercase;
}
.lt-coner {
  border-top-left-radius: 16px;
}
.lb-coner {
  border-bottom-left-radius: 16px;
}
.rb-coner {
  border-bottom-right-radius: 16px;
}
.rt-coner {
  border-top-right-radius: 16px;
}
.work-cancelled {
  position: relative;
  background: #9ea5a5;
  color: white;
}
.working {
  background: #00b2a9;
  color: white;
}
</style>
