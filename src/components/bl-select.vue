<template>
<div>
  <div class="bl-select">
    <div class="bl-tags-wrapper"   :class="[visible ? 'tags-wrappers-foucs' : '']" @click.stop="toggleMenu">
      <img v-if="tagsArray.length !== 0" @click="removeAllTags" class="bl-close" src="../assets/icons/select-close.png">
      <bl-tag v-for="(item,index) in tagsArray" :key="item" @close="removeTag($event, index)" closable>{{item}}</bl-tag>
      <input type="text" readonly class="bl-select__input" :value="value" @input="updateValue($event.target.value)">
    </div>
    <div class="bl-dropdown" v-show="visible">
      <li @click="clickOption(index)" v-for="(item,index) in data" :key="item.value" class="bl-select-dropdown__item" :class="[item.select ? 'bl-select-dropdown__item-select' : '']">
        <img v-if="item.select" src="../assets/icons/select-ed.png">
        <img v-if="!item.select" src="../assets/icons/select.png"> {{item.label}}
      </li>
      <p class="bl-select-dropdown__empty" v-if="emptyText">
        {{ emptyText }}
      </p>
    </div>
  </div>
</div>
</template>
<script>
import BlTag from './bl-tag'
export default {
  data: function() {
    return {
      visible: false
    }
  },
  components: {
    BlTag
  },
  watch: {

  },
  props: {
    data: Array, // 原始数组
    value: Array // v-model对应的值数组
  },
  computed: {
    // 原始数组为空时显示
    emptyText() {
      if (this.data.length) {
        return null
      } else {
        return '暂无数据'
      }
    },
    tagsArray() {
      let arrayData = []
      this.value.map((item, index, array) => {
        let obj = this.data.find((itemObj) => {
          return itemObj.value === item;
        })
        arrayData.push(obj.label)
      })
      return arrayData
    }
  },
  created() {
    this._setSelect()
  },
  methods: {
    // 点击option触发
    clickOption(index) {
      let valueData = this.value.slice(0)
      // console.log(valueData,';1')
      let valueIndex = this.value.findIndex((item) => {
        return item === this.data[index].value
      })
      // console.log(valueIndex, 'valueIndex')
      if (this.data[index].select) {
        this.$set(this.data[index], 'select', false)
        if (valueIndex !== -1) {
          valueData.splice(valueIndex, 1)
          this.$emit('input', valueData)
        }
      } else {
        this.$set(this.data[index], 'select', true)
        if (valueIndex === -1) {
          // console.log('111')
          valueData.push(this.data[index].value)
          this.$emit('input', valueData)
        }
      }
    },
    toggleMenu() {
      this.visible = !this.visible;
    },
    _setSelect() {

      this.value.map((item, index, array) => {
        let obj = this.data.findIndex((itemObj) => {
          return itemObj.value === item;
        })
        this.clickOption(obj)
      })
    },

    removeTag(event, index) {
      let optionIndex = this.data.findIndex((obj) => {
        return obj.value === this.value[index]
      })
      this.clickOption(optionIndex)
      event.stopPropagation();
    },
    removeAllTags(event) {
      this.$emit('input', [])
      for (let i = 0; i < this.data.length; i++) {
        this.data[i].select = false
      }
      event.stopPropagation()
    }
  }
}
</script>

<style>
.tags-display {
  width: 200px;
  height: 30px;
  border: 1px solid black;
}

.bl-select {
  display: flex;
  width: 250px;
  position: relative
}

.bl-tags-wrapper {
  cursor: pointer;
  position: relative;
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
  align-items: center;
  width: 100%;
  position: relative;
  font-size: 14px;
  background-color: #fff;
  background-image: none;
  border-radius: 4px;
  border: 1px solid #dcdfe6;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  color: #606266;
  font-size: inherit;
  min-height: 35px;
  line-height: 1;
  outline: 0;
  padding: 5px 5px;
  -webkit-transition: border-color .2s cubic-bezier(.645, .045, .355, 1);
  transition: border-color .2s cubic-bezier(.645, .045, .355, 1);
}
.tags-wrappers-foucs{
  border-color: #409eff;
}

.bl-select__input {
  position: absolute;
  top: 0;
  left: 0;
  visibility: hidden;
  border: none;
  outline: 0;
  padding: 0;
  margin-left: 15px;
  color: #666;
  font-size: 14px;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  height: 28px;
  background-color: transparent
}

.bl-tags-wrapper .bl-close {
  width: 20px;
  height: 20px;
  cursor: pointer;
  position: absolute;
  top: 50%;
  right: 5px;
  transform: translateY(-50%);
}

.bl-dropdown {
  width: 100%;
  min-height: 34px;
  top: 100%;
  max-height: 274px;
  overflow: auto;
  position: absolute;
  z-index: 1001;
  border: 1px solid #e4e7ed;
  border-radius: 4px;
  background-color: #fff;
  -webkit-box-shadow: 0 2px 12px 0 rgba(0, 0, 0, .1);
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, .1);
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  margin: 5px 0
}

.bl-select-dropdown__item {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  font-size: 14px;
  padding: 0 20px;
  position: relative;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  color: #606266;
  height: 34px;
  line-height: 34px;
  -webkit-box-sizing: border-box;
  box-sizing: border-box;
  cursor: pointer;
  list-style: none;
}

.bl-select-dropdown__item-select {
  color: #2873df
}

.bl-select-dropdown__item>img {
  width: 20px;
  height: 20px;
  margin-right: 20px;
}

.bl-select-dropdown__item.hover,
.bl-select-dropdown__item:hover {
  background-color: #f5f7fa
}

.bl-select-dropdown__empty {
  padding: 10px 0;
  margin: 0;
  text-align: center;
  color: #999;
  font-size: 14px
}
</style>
