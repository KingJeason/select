<template>
<div id="app">
  <div>
    <bl-select v-model="value" :data="dataArray"></bl-select>
  </div>
</div>
</template>

<script>
import BlSelect from './components/bl-select'
import BlTag from './components/bl-tag'
export default {
  data: function() {
    return {
      value: ['0', '3'],
      dataArray: [{
        label: '变更中',
        value: '0',
      }, {
        label: '未生效',
        value: '1'
      }, {
        label: '作废',
        value: '2'
      }, {
        label: '正常',
        value: '3'
      }, {
        label: '审核',
        value: '4'
      }]
    }
  },
  components: {
    BlSelect,
    BlTag
  },
  watch: {
    value(oldnew) {
      console.log('v-model', oldnew)
    },
  },
  methods: {}
}
</script>

<style>
.class_finisned {
  text-decoration: underline;
}
</style>
