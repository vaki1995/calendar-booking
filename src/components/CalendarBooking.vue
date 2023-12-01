<script setup>
import { onMounted, defineEmits } from 'vue';
import moment from 'moment';
import Datepicker from 'flowbite-datepicker/Datepicker';

const emits = defineEmits(['dateCellClick']);

onMounted(() => {
  const datepickerEl = document.getElementById('datepickerId');
  new Datepicker(datepickerEl, {
    format: 'yyyy-mm-dd',
    language: 'en',
  });
  // Get all date cells within the datepicker
  const dateCells = datepickerEl.querySelectorAll('.datepicker-cell');
  dateCells.forEach((cell) => {
    cell.addEventListener('click', (event) => {
      handleDateCellClick(event);
    });
  });
});
const handleDateCellClick = (event) => {
  const booking_date = formatTimestamp(event.currentTarget.dataset.date/1000);
  emits('dateCellClick', booking_date);
};

const formatTimestamp = (timestamp) => {
  const date = moment.unix(timestamp).format('YYYY-MM-DD');
  return date;
};

</script>

<template>
<div class="mt-3 mb-5 w-full-datepicker bg-selected-custom" id="datepickerId" inline-datepicker :data-date="data_date"></div>
</template>

<script>
export default {
  props: {
    data_date: {
      type: String,
    },
  },
};
</script>

<style>
  .w-full-datepicker .datepicker-picker,
  .w-full-datepicker .datepicker-grid,
  .w-full-datepicker .days {
    width: 100% !important;
  }
  .bg-selected-custom .datepicker-cell.selected{
    background-color: rgb(249 115 22) !important;
  }
</style>

