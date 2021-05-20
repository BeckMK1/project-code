<template>
  <div class="setting-wrapper">
    <div class="setting-tab">
      <div class="content">
        <div class="title-wrapper">
          <p>Localization options</p>
          <p>Details that help us get in touch with you.</p>
        </div>
        <SettingsDropdown label="language" v-model="settingsData.lang" @UpdataCountry="emitdrop($event)">
          <option value="da">DA</option>
          <option value="en">EN</option>
          <option value="ge">GE</option>
          <option value="nl">NL</option>
        </SettingsDropdown>
        <SettingsDropdown label="currency" v-model="settingsData.curr" @UpdataCountry="emitdrop($event)">
          <option value="DKK">DKK</option>
          <option value="GBP">GBP</option>
          <option value="EURO">EURO</option>
        </SettingsDropdown>
        <label>time and date fromatting</label>
        <div class="time-date">
          <SettingsDropdown v-model="settingsData.time" @UpdataCountry="emitdrop($event)">
            <option value="24h">24H</option>
            <option value="12h">12H</option>
          </SettingsDropdown>
          <SettingsDropdown @UpdataCountry="emitdrop($event)" v-model="settingsData.date">
            <option value="d/m/y">D/M/Y</option>
            <option value="m/d/y">M/D/Y</option>
          </SettingsDropdown>
        </div>
      </div>
      <div class="line"></div>
    </div>
    <div class="setting-tab">
      <div class="content">
        <div class="title-wrapper">
          <p> Rent and lent options</p>
          <p>Details that help us get in touch with you.</p>
        </div>
        <div class="inputs">
          <ToggleButton :defaultToggle="settingsData.toggleVat" label="show vat on prices" discription="display prices with or without vat " @toggleValue="toggleSet1($event)" />
          <ToggleButton
            :defaultToggle="settingsData.toggleVaction"
            label="Vacation"
            discription="disables notifications "
            @toggleValue="toggleSet2($event)" />
        </div>
        <div class="ind-biss">
          <div>
            <p>Type of renter/Lender</p>
            <p>chose what type of user you are</p>
          </div>
          <div class="inputs">
            <div @click="settingsData.isInd=true,settingsData.isBiss=false">
              <SingleSelect :isSelected="settingsData.isInd" typeOfSelect="single" label="I am an Individual" />
            </div>
            <div @click="settingsData.isInd=false, settingsData.isBiss=true">
              <SingleSelect :isSelected="settingsData.isBiss" typeOfSelect="single" label="I am a Business" />
            </div>
          </div>
        </div>
        <div class="working">
          <div>
            <p>work hours and days </p>
            <p>chose hours and days that yor are lenting out gear</p>
          </div>
          <div>
            <p>Work hours</p>
          </div>
          <div class="from-to-wrapper">
            <div class="from-to">
              <div class="select">
                <SettingsDropdown v-if="settingsData.time =='12h'" desing="settings" @UpdataCountry="emitdrop($event)" v-model="settingsData.usTimeFrom">
                  <option value="am">am</option>
                  <option value="pm">pm</option>
                </SettingsDropdown>
              </div>
              <div class="input">
                <BaseInput design="settings" v-model="settingsData.timeForm" v-if="settingsData.time =='12h'" label="from" />
                <BaseInput design="profile" v-model="settingsData.timeFrom" v-if="settingsData.time =='24h'" label="from" />
              </div>
            </div>
            <div class="from-to">
              <div class="select">
                <SettingsDropdown v-if="settingsData.time =='12h'" desing="settings" @UpdataCountry="emitdrop($event)" v-model="settingsData.usTimeTo">
                  <option value="am">am</option>
                  <option value="pm">pm</option>
                </SettingsDropdown>
              </div>
              <div class="input">
                <BaseInput design="settings" v-model="settingsData.timeTo" v-if="settingsData.time =='12h'" label="to" />
                <BaseInput design="profile" v-model="settingsData.timeTo" v-if="settingsData.time =='24h'" label="to" />
              </div>
            </div>
          </div>
        </div>
        <div class="days-working">
          <div>
            <p>what days do you typically work</p>
            <p>
              chose when you are availeble to lent gear.<br>
              <em>(If you want to chose more specfick days, use the calendar)</em>
            </p>
          </div>
          <div class="inputs">
            <div @click="settingsData.isWeekdays=!settingsData.isWeekdays">
              <MultiSelect :isSelected="settingsData.isWeekdays" label="weekdays" />
            </div>
            <div @click="settingsData.isWeekends=!settingsData.isWeekends">
              <MultiSelect :isSelected="settingsData.isWeekends" label="weekends" />
            </div>
          </div>
        </div>
        <div class="show-calendar" @click="isCalendar=!isCalendar">
          <span>show Calendar</span>
          <span>></span>
        </div>
        <div v-show="isCalendar" class="calendar">
          <!-- insert help icon -->
          <p>
            <em>days marked in green are days you are working.<br>
              the mark a day click on a unmark day. to unmark a day click on a marked
            </em>
          </p>
          <Calendar @click="setDays($event)" :weekend="settingsData.isWeekends" :weekday="settingsData.isWeekdays" />
        </div>
      </div>
      <div class="line"></div>
    </div>
    <div class="setting-tab">
      <div class="content">
        <div class="title-wrapper">
          <p>Other options</p>
          <p>Details that help us get in touch with you.</p>
        </div>
        <div class="cc-email ind-biss">
          <div class="">
            <p>cc-emails</p>
            <p>cc emails form Wedio </p>
          </div>
          <div class="email" id="addsEmails">
            <BaseInput label="cc-email" design="profile" v-model="settingsData.email1" :disabled="!isCc" />
            <BaseInput label="cc-email" design="profile" v-model="settingsData.email2" :disabled="!isCc" v-if="settingsData.cc2" />
            <BaseInput label="cc-email" design="profile" v-model="settingsData.email3" :disabled="!isCc" v-if="settingsData.cc3" />
            <BaseInput label="cc-email" design="profile" v-model="settingsData.email4" :disabled="!isCc" v-if="settingsData.cc4" />
          </div>
          <div class="add-save">
            <div class="wedio-button primary" @click="isAdd=true, isCc=false, hideCc()" v-if="!isAdd">save</div>
            <div class="wedio-button primary " @click="ccIs(), isAdd=false, isCc=true" v-if="isAdd">add and edit emails</div>
          </div>
        </div>
        <div class="account-delete">
          <div>
            <p>permenly delete your account</p>
            <div class="delete-btn">
              <div class="wedio-button wedio-red " @click="isModal=true">delete</div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="delete-modal" v-if="isModal">
      <div class="black-background"></div>
      <div class="modal-wrapper">
        <div class="modal-title">
          <p>account deletion</p>
        </div>
        <div class="modal-text">
          <p>
            Confirm that you want to delete your account.<br>
            <em> We will send you an email to be sure, that you wish to delete your account </em>
          </p>
        </div>
        <div class="buttons">
          <div class="wedio-button wedio-red">delete</div>
          <div class="wedio-button outline-dark" @click="isModal= false">Cancel</div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import SettingsDropdown from '~/components/dashboard/SettingsDropdown';
import ToggleButton from '~/components/dashboard/ToggleButton';
import SingleSelect from '~/components/dashboard/SingleSelect';
import MultiSelect from '~/components/dashboard/MultiSelect';
import BaseInput from '~/components/BaseInput';
import Calendar from '~/components/dashboard/Calendar';
export default {
  components: {
    SettingsDropdown,
    ToggleButton,
    SingleSelect,
    MultiSelect,
    BaseInput,
    Calendar
  },
  layout: 'dashboard',
  data () {
    return {
      settingsData: {
        isWeekdays: false,
        isWeekends: false,
        toggleVat: true,
        toggleVaction: false,
        isInd: true,
        isBiss: false,
        cc2: false,
        cc3: false,
        cc4: false,
        canlenderDays: {},
        lang: 'da',
        curr: 'DKK',
        date: 'd/m/y',
        time: '24h',
        usTimeTo: 'am',
        usTimeFrom: 'am',
        email1: '',
        email2: '',
        email3: '',
        email4: '',
        timeTo: '',
        timeFrom: ''
      },
      isCc: false,
      isCalendar: false,
      isModal: false,
      isAdd: true
    };
  },
  mounted () {
  },
  methods: {
    toggleSet1 (isToggle) {
      this.settingsData.toggleVat = isToggle;
    },
    toggleSet2 (isToggle) {
      this.settingsData.toggleVaction = isToggle;
    },
    setDays (isDays) {
      this.settingsData.canlenderDays = isDays;
    },
    ccIs () {
      this.settingsData.cc2 = true;
      this.settingsData.cc3 = true;
      this.settingsData.cc4 = true;
    },
    hideCc () {
      if (this.settingsData.email2 === '') {
        this.settingsData.cc2 = false;
      }
      if (this.settingsData.email3 === '') {
        this.settingsData.cc3 = false;
      }
      if (this.settingsData.email4 === '') {
        this.settingsData.cc4 = false;
      }
    }
  }
};
</script>
<style lang="scss" scoped>
@import "~assets/styles/components/wedio-buttons.scss";
.title-wrapper {
  margin-bottom: 38px;
  p:first-child {
    font-size: 20px;
    font-weight: bold;
  }
  p:last-child {
    font-size: 14px;
  }
}
.setting-tab {
  margin-top: 38px;
}
.content {
  margin-right: auto;
  margin: auto;
  width: 325px;
}
.line {
  border-bottom: #9ea5a5 solid 1px;
  opacity: 66%;
  margin-left: auto;
  margin-right: auto;
  width: 100%;
  height: 1px;
  margin-top: 16px;
}
label {
  font-size: 12px;
  font-weight: bold;
  margin-bottom: 4px;
  text-transform: uppercase;
}
.account-delete {
  p {
    font-size: 14px;
    font-weight: bold;
    text-transform: uppercase;
    margin-bottom: 8px;
  }
}
.delete-btn {
  display: flex;
  justify-content: center;
  margin-bottom: 24px;
  div {
    margin-right: auto;
    margin-left: auto;
  }
}
.working {
  margin-top: 24px;
  p:first-child {
    font-weight: bold;
    font-size: 14px;
    text-transform: uppercase;
  }
  p:nth-child(2) {
    margin-bottom: 8px;
  }
  p {
    font-size: 11px;
  }
}
.ind-biss,
.days-working {
  display: flex;
  p:first-child {
    font-weight: bold;
    font-size: 14px;
    text-transform: uppercase;
  }
  p {
    font-size: 11px;
  }
}
.inputs {
  margin-left: auto;
}
.cc-email {
  display: flex;
  flex-direction: column;
}
.add-save {
  display: flex;
  justify-content: center;
  margin-left: auto;
  margin-right: auto;
}
.show-calendar {
  display: flex;
  text-align: center;
  flex-direction: column;
  span {
    font-size: 14px;
    color: #00b2a9;
    font-weight: bold;
    cursor: pointer;
    text-transform: uppercase;
    user-select: none;
  }
  span:last-child {
    position: relative;
    z-index: -1;
    transform: rotate(90deg);
    font-size: 12px;
  }
}
.calendar {
  p {
    font-size: 11px;
  }
}
.time-date {
  display: flex;
  flex-direction: row;
  align-items: flex-end;
  width: 100%;
}
.time-date div:first-child {
  width: 60%;
  margin-right: 8px;
}
.time-date div:last-child {
  width: 100%;
}
.from-to-wrapper {
  display: flex;
  flex-direction: row;
}
.from-to {
  display: flex;
  flex-direction: row-reverse;
  align-items: flex-end;
  justify-content: flex-end;
  .input {
    width: 40%;
  }
  .select {
    margin-left: -1px;
    width: 40%;
  }
}
.cc-email {
  margin-bottom: 24px;
}
.delete-modal {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100vw;
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 10;
}
.black-background {
  position: absolute;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100vw;
  z-index: 10;
  background: black;
  opacity: 50%;
}
.modal-wrapper {
  position: relative;
  width: 500px;
  height: 300px;
  background: white;
  z-index: 11;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  border-radius: 8px;
}
.buttons {
  display: flex;
  justify-content: space-between;
  width: 436px;
}
.wedio-red {
  margin-right: 16px;
}
.modal-text {
  margin: 32px;
}
.modal-title p {
  font-weight: bold;
  text-transform: uppercase;
}
</style>
