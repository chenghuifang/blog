---
title: vue组件--滑块
---

1.使用
template:(value为滑块初始化的值)
``` javascript
slider(title="滑块名称", :min="0", :max="100", :value="50", @value-change="getValue")
```
methods:
``` javascript
getValue = function (data) {
  console.log(value, "从组件内传出来的值，也就是滑块的值")
}
```

2.组件
``` javascript
<script>
export default {
  props: {
    title: {
      type: String,
      required: true
    },
    min: {
      type: Number,
      default: 0
    },
    max: {
      type: Number,
      default: 100
    },
    type: {
      type: String,
      default: 'int'
    },
    value: {
      type: Number
    },
    showValue: {
      type: Boolean,
      default: true
    },
    disabled: {
      type: Boolean,
      default: false
    }
  },
  data () {
    return {
      dragging: false,
      sliderWidth: 0,
      sliderOffsetLeft: 0,
      moveWidth: 0,
      oMoveWidth: 0
    }
  },
  computed: {
    title2Lines () {
      return this.title.split('@')
    },
    posStyle () {
      return this.moveWidth + 'px'
    },
    viewValue () {
      if (this.moveWidth === this.oMoveWidth) return
      this.oMoveWidth = this.moveWidth
      switch (this.type) {
        case 'int':
          let value = (this.min + this.moveWidth * (this.max - this.min) / this.sliderWidth).toFixed(0)
          this.$emit('value-change', value)
          return value
      }
    }
  },
  watch: {
    value (nv) {
      if (this.value) this.moveWidth = this.sliderWidth * (this.value - this.min) / (this.max - this.min)
    }
  },
  methods: {
    clickSlider (event) {
      if (this.dragging || this.disabled) return
      this.moveWidth = event.clientX - this.sliderOffsetLeft
    },
    onDragStart () {
      this.dragging = true
    },
    onDragging (event) {
      let moveWidth = event.clientX - this.sliderOffsetLeft
      if (moveWidth > this.sliderWidth) {
        this.moveWidth = this.sliderWidth
        this.onDragEnd()
      } else if (moveWidth < 0) {
        this.moveWidth = 0
        this.onDragEnd()
      } else {
        this.moveWidth = moveWidth
      }
    },
    onDragEnd (event) {
      if (this.dragging) {
        window.removeEventListener('mousemove', this.onDragging)
        window.removeEventListener('mouseup', this.onDragEnd)
        this.dragging = false
      }
    },
    buttonDown (event) {
      if (this.disabled) return
      window.addEventListener('mousemove', this.onDragging)
      window.addEventListener('mouseup', this.onDragEnd)
      this.onDragStart()
    }
  },
  mounted () {
    this.sliderWidth = this.$refs.slider.offsetWidth
    this.sliderOffsetLeft = this.$refs.slider.getBoundingClientRect().left
    if (this.value) this.moveWidth = this.sliderWidth * (this.value - this.min) / (this.max - this.min)
  }
}
</script>

<template>
<div class="slider-body form-group">
  <label class="form-label">
    <span>{{title2Lines[0]}}</span><br/>
    <span v-if="title2Lines[1]">{{title2Lines[1]}}</span>
  </label>
  <div class="slider-container" onselectstart="return false">
    <div class="slider" ref="slider" onselectstart="return false" @click="clickSlider($event)">
      <span class="number" :class="{'hide': !showValue}" :style="{'left': posStyle}">{{viewValue}}</span>
      <div class="progress" :class="{'disabled': disabled}" :style="{'width': posStyle}"></div>
      <div class="handle-icon" :class="{'hide': disabled,'dragging': dragging}" :style="{'left': posStyle}" @mousedown="buttonDown($event)"></div>
    </div>
    <div class="number-labels clear-float">
      <span class="float-left">{{min}}</span>
      <span class="float-right">{{max}}</span>
    </div>
  </div>
</div>
</template>

<style lang="less" scoped>
.form-group {
  padding-left: 6em;
  .form-label {
    font-size: 14px;
    width: 60px;
    color: #fff;
  }
}
.slider-body {
  color: #fff;
  margin-top: 20px;
  >label {
    top: -2px;
    left: 12px;
  }
  .slider-container {
    width: 100%;
    border-radius: 4px;
    display: inline-block;
    user-select: none;
    .slider {
      width: 100%;
      height: 6px;
      background: #969a9d;
      position: relative;
      margin: 0;
      .number {
        position: absolute;
        left: 0;
        top: -24px;
        width: 90px;
        margin-left: -45px;
        text-align: center;
        display: block;
        color: #007dc9;
      }
      .progress {
        height: 100%;
        width: 0;
        background: #007dc9;
      }
      .handle-icon {
        width: 14px;
        height: 14px;
        border-radius: 50%;
        background: #fff;
        position: absolute;
        top: -2px;
        top: -4px;
        left: 0;
        margin-left: -7px;
        cursor: pointer;
        &:hover, &.dragging {
          transform: scale(1.2)
        }
      }
    }
    .float-left {
      float: left;
    }
    .float-right {
      float: right;
    }
  }
}
</style>
```
