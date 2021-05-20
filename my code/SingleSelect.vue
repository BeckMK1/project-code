<template>
  <div class="select">
    <div class="single">
      <div>
        <label :for="_uid + label">{{ label }}</label>
      </div>
      <div :id="_uid + label" :class="{on:isSelected}" class="single-select"></div>
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
    isSelected: {
      type: Boolean,
      default: false
    },
    discription: {
      type: String,
      default: ''
    }
  }

};
</script>
<style lang="scss" scoped>
.single-select {
  width: 20px;
  height: 20px;
  background: white;
  border: gray solid 1px;
  position: relative;
  z-index: 1;
  margin-left: auto;
  margin-top: 4px;
  border-radius: 100%;
}
.on::after {
  content: "";
  position: absolute;
  width: 12px;
  height: 12px;
  background: #00b2a9;
  z-index: 2;
  border-radius: 100%;
  left: 3px;
  top: 3px;
}
label {
  font-size: 11px;
  margin-right: 8px;
}
.single {
  display: flex;
  flex-direction: row;
}
</style>
