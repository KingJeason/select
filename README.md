# 多选下拉框
### 用例
```
<bl-select v-model="value" :data="dataArray"></bl-select>
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

```

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
