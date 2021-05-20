<template>
  <div class="currency-wrapper" :design="desing">
    <label :for="_uid + label">{{ label }}</label>
    <div class="select-arrow">
      <select :id="_uid + label" @input="updateValue" v-model="localCountry">
        <slot></slot>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    label: {
      type: String,
      default: ''
    },
    design: {
      validator: prop => [
        'settings'
      ].includes(prop),
      default: 'line'
    },
    value: {
      type: String,
      default: ''
    },
    countryValue: {
      type: String,
      default: ''
    }
  },
  computed: {
    localCountry: {
      get () { return this.value; },
      set (countryValue) { this.$emit('input', countryValue); }
    }
  },
  methods: {
    updateValue (countryValue) {
      this.$emit('input', countryValue);
    }
  }

};
</script>
<style lang="scss" scoped>
.currency-wrapper {
  position: relative;
  display: flex;
  flex-direction: column;
  @include from($desktop) {
    margin-right: 0;
    margin-left: 0;
  }
  label {
    font-size: 12px;
    font-weight: bold;
    margin-bottom: 4px;
    text-transform: uppercase;
  }
}

.select-arrow {
  width: 100%;
  position: relative;
  select {
    border: 1px solid #9ea5a5;
    border-radius: 6px;
    font-size: 14px;
    padding-left: 10px;
    height: 38px;
    margin-bottom: 12px;
    -webkit-appearance: none;
    width: 100%;
    -moz-appearance: none;
    outline: none;
    appearance: none;
    z-index: 2;
    background: transparent;
    &[disabled="disabled"] {
      background-color: #f2f2f2;
      border: 1px solid transparent;
      color: $black;
      -webkit-text-fill-color: $black;
      opacity: 1;
      -webkit-appearance: none;
    }
    &:focus {
      border: 1px solid transparent;
      box-shadow: 0 0 0 2px $black;
      -webkit-box-shadow: 0 0 0 2px $black;
      outline: none;
      -webkit-appearance: none;
    }
  }
}
.select-arrow::after {
  content: ">";
  font-family: "Consolas", monospace;
  font-size: 20px;
  top: 15%;
  z-index: -1;
  font-weight: bold;
  -webkit-transform: rotate(90deg);
  -moz-transform: rotate(90deg);
  -ms-transform: rotate(90deg);
  transform: rotate(90deg);
  color: #00b2a9;
  right: 11px;
  position: absolute;
}
.currency-wrapper[desing="settings"] {
  .select-arrow {
    select {
      border-radius: 0 6px 6px 0;
    }
  }
}
</style>
