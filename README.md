# Vue Datetimepicker Component

## Related Versions

`v-datetime-picker` Component is baseed on these plugins and libs(version):
- [vue2.x](https://vuejs.org/index.html)
- [jQuery](https://jquery.com/)
- [bootstrap-datetimepicker](http://www.bootcss.com/p/bootstrap-datetimepicker/)

## How to use
---
### Install
``` cmd
# npm install
npm install v-datetimepicker-component --save

# if you have not installed jquery
npm install jquery --save
```

### Use as component
1. Import component.

``` javascript
// import DateTimePickerComponent
import Datetimepicker from 'v-datetimepicker-component';

// 1. use as global component
Vue.component('datetimepicker', Datetimepicker);

// 2. use in a single component
export default {
    // declare components
    components: {Datetimepicker}
}
```

2. Template.

``` html
<datetimepicker v-model="your_prop" :startDate="startDate" :endDate="endDate" :timestamp="isTimestamp"
  :maxView="maxView" :minView="minView" :disabled="isDisabled" @change="change($event)" ></datetimepicker>
```

### Options
- `startDate`: `string`
  - date range: start date
- `endDate`: `string`
  - date range: end date
- `maxView`: `string`
  - maxView: default 4
    - 0 or 'hour' for the hour view （hour view）
    - 1 or 'day' for the day view 0-24h （day view）
    - 2 or 'month' for month view (the default) （month view）
    - 3 or 'year' for the 12-month overview （year view）
    - 4 or 'decade' for the 10-year overview. Useful for date-of-birth datetimepickers.
- `minView`: `string`
- `disabled`: `boolean`
  - isDisabled: default false
- `timestamp`: `boolean`
  - isTimestamp: timestamp for v-model, default false(string)
- `@change`
  - callback when datetime selected
