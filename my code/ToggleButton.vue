<template>
  <div class="toggle-button">
    <div>
      <label :for="label + _uid">{{ label }}</label>
      <p>{{ discription }}</p>
    </div>
    <div :id="_uid + label" class="toggle" @click="toggle = !toggle,toggleVat(), emitToggle() "></div>
  </div>
</template>
<script>
export default {
  props: {
    label: {
      type: String,
      default: ''
    },
    discription: {
      type: String,
      default: ''
    },
    defaultToggle: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      toggle: this.defaultToggle
    };
  },
  mounted () {
    this.toggleVat();
  },
  methods: {
    toggleVat () {
      if (this.toggle === true) {
        document.getElementById(this._uid + this.label).classList.add('on');
        document.getElementById(this._uid + this.label).classList.remove('off');
      } else {
        document.getElementById(this._uid + this.label).classList.add('off');
        document.getElementById(this._uid + this.label).classList.remove('on');
      }
    },
    emitToggle () {
      this.$emit('toggleValue', this.toggle);
    }
  }
};
</script>
<style lang="scss" scoped>
.toggle {
  width: 100px;
  height: 38px;
  border-radius: 20px;
  position: relative;
  z-index: 1;
}
.toggle::after {
  content: "";
  position: absolute;
  width: 28px;
  height: 28px;
  border-radius: 100%;
  z-index: 2;
  top: 5px;
}
.toggle.on::after {
  background: white;
  right: 5px;
}
.toggle.on {
  background: #00b2a9;
  margin-bottom: 16px;
}
.toggle.off {
  background: #f2f2f2;
  margin-bottom: 16px;
}
.toggle.off::after {
  background: gray;
  left: 5px;
}
label {
  font-weight: bold;
  font-size: 14px;
  text-transform: uppercase;
}
.toggle-button {
  display: flex;
  p {
    font-size: 11px;
  }
}
.toggle-button div:nth-child(2) {
  margin-left: auto;
}
</style>
