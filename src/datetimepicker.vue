<template>
  <span>
    <input type="text" class="form-control form-input" :disabled="disabled" :placeholder="placeholder" :value="date">
  </span>
</template>

<script>
import "./format.js";
import "./bootstrap-datetimepicker/js/bootstrap-datetimepicker.min.js";
// 需要切换中文时需引入
import "./bootstrap-datetimepicker/js/bootstrap-datetimepicker.zh-CN.js";

export default {
  name: "datetimepicker",
  data() {
    return {
      date: ""
    };
  },
  model:{
    event: 'change'
  },
  props: {
    placeholder: {
      type: String,
      default: ""
    },
    disabled: {
      type: Boolean,
      default: false
    },
    format: {
      type: String,
      default: "yyyy-mm-dd hh:ii:ss"
    },
    minView: {
      type: Number,
      default: 0
    },
    startView: {
      type: Number,
      default: 2
    },
    maxView: {
      type: Number,
      default: 4
    },
    startDate: {
      type: Date,
      default: null
    },
    endDate: {
      type: Date,
      default: null
    },
    value: {
      type: String,
      default: ''
    },
    timestamp: {
      type: Boolean,
      default: false
    }
  },
  mounted() {
    this.date = this.timestamp ? this.value.format('yyyy-mm-dd hh:ii:ss') : this.value
    /*
     0 or 'hour' for the hour view
     1 or 'day' for the day view 0-24h
     2 or 'month' for month view (the default)
     3 or 'year' for the 12-month overview
     4 or 'decade' for the 10-year overview. Useful for date-of-birth datetimepickers.
     */
    $(this.$el)
      .find("input")
      .datetimepicker({
        language: "zh-CN",
        format: this.format,
        autoclose: true,
        startView: this.startView,
        minView: this.minView,
        maxView: this.maxView,
        startDate: this.startDate,
        endDate: this.endDate
      })
      .on("hide", ev => {
        this.date = $(ev.target).val();
        const value = this.timestamp ? new Date(this.date).getTime() / 1000 : this.date;
        this.$emit("change", value);
      });
  },
  beforeDestroy() {
    $(this.$el)
      .find("input")
      .datetimepicker("remove");
  }
};
</script>
<style scope>
@import "./bootstrap-datetimepicker/css/bootstrap-datetimepicker.css";
.dropdown-menu {
    position: absolute;
    top: 100%;
    left: 0;
    z-index: 1000;
    display: none;
    float: left;
    min-width: 160px;
    padding: 5px 0;
    margin: 2px 0 0;
    font-size: 14px;
    text-align: left;
    list-style: none;
    background-color: #fff;
    -webkit-background-clip: padding-box;
    background-clip: padding-box;
    border: 1px solid #ccc;
    border: 1px solid rgba(0,0,0,0.15);
    border-radius: 4px;
    -webkit-box-shadow: 0 6px 12px rgba(0,0,0,0.175);
    box-shadow: 0 6px 12px rgba(0,0,0,0.175);
}
</style>