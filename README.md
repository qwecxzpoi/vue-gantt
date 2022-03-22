#### Vue3甘特图插件
> 基于Vue3的甘特图组件

![avatar](https://blog.ddamy.com/assets/img/gantt.jpeg)

### 使用方式
```js
import Gantt from 'vue3-gantt'
```

### 组件接收参数

| 参数名 | 类型 | 默认值 | 可选值 | 说明 |
| ------ | ------ | -------- | -- | ------------ |
| data | Array[Object] | [] | - | 甘特图数据 |
| dateRangeList | Array | [] | - | 当前图表内的日期区间，此数组长度为2，内容为起始时间, 格式为'YYYY-MM-DD' |
| scheduleClick | Function | null | - | 点击日程的回调事件，接收一个日程详情参数 |
| scrollXEnd | Function | null | - | 横向滚动条滚动到底部的事件 |
| itemText | String | null | - | 表头描述文字 |
| dateText | String | null | - | 表头描述文字 |
| activeDate | String | 今天 | - | 当前时间轴高亮显示的一天，（不会覆盖日程样式），'YYYY-MM-DD'格式时间字符串 |
| repeatMode | Object | 见下方 | - | 重叠日程展示模式配置 |
| itemWidth | Number | 40 | - | 日期格子的宽度，最小40 |
| itemHeight | Number | 40 | - | 日期格子的高度度，最小40 |
| scheduleTitle | Function | null | - | 日程上面展示的文本，function接收日程信息为参数，最终使用该方法返回值渲染 |

### data配置 Array[Object]

| 参数名 | 取值  |说明 |
| ------ | ------ | ------ |
| type | 'alike'\|\|'normal' | 项目类型 |
| color | css颜色格式 | 当前项目背景色, type为'alike'时生效 |
| name | String | 当前项目名称 |
| schedule | Array[Object] | 项目日程 |

### schedule 项目日程配置

> 为了便于业务开发，可以在以下基础上任意拓展字段

| 参数名 |说明 |
| ------ | -------------------- |
| id | 日程全局唯一id |
| name | 日程名称 |
| desc | 日程描述 |
| backgroundColor | 日程背景色 |
| textColor | 日程名称展示文字颜色 |
| days | 日程日期列表`Array`, 数组内容为合法的连续的日期，日期格式为 `YYYY-MM-DD` |

### repeatMode配置 Object

| 参数名 | 可选值 | 默认值 | 说明 |
| ------ | ------ | -------- | ---------- |
| mode | 'cover'\|\|'extract' | 'cover' | 重叠日程的处理方式，正常覆盖或者单独提取重复日程再组合 |
| backgroundColor | css颜色格式 | '#FFFFCC' | extract模式下的背景色 |
| textColor | css颜色格式 | '#336666' | extract模式下的文字颜色 |
| name | `String`\|\|`Function` | '重叠日程' | 重叠日程的展示文字，Function接收一个list参数，参数为重叠日程Array |
| desc | `String`\|\|`Function` | '这是多个日程' | 重叠日程的描述文字，Function接收一个list参数，参数为重叠日程Array |


### 组件实例对外暴露的方法

#### 导出当前甘特图的完整快照图片

```html
<Gantt
    ref="gantt"
    ...
/>
<button @click="exportImg">下载图片</button>
```
```js
const gantt = ref(null)

const exportImg = () => {
  gantt.value.exportImg()
}
```