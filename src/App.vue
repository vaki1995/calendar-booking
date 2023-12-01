<template>
  <div class="bg-white font-sans">
    <div class="relative isolate px-6 pt-14 lg:px-8">
      <div class="absolute inset-x-0 -top-40 -z-10 transform-gpu overflow-hidden blur-3xl sm:-top-80" aria-hidden="true">
        <div class="relative left-[calc(50%-11rem)] aspect-[1155/678] w-[36.125rem] -translate-x-1/2 rotate-[30deg] bg-gradient-to-tr from-[#ff80b5] to-[#9089fc] opacity-30 sm:left-[calc(50%-30rem)] sm:w-[72.1875rem]" style="clip-path: polygon(74.1% 44.1%, 100% 61.6%, 97.5% 26.9%, 85.5% 0.1%, 80.7% 2%, 72.5% 32.5%, 60.2% 62.4%, 52.4% 68.1%, 47.5% 58.3%, 45.2% 34.5%, 27.5% 76.7%, 0.1% 64.9%, 17.9% 100%, 27.6% 76.8%, 76.1% 97.7%, 74.1% 44.1%)" />
      </div>
      <div class="mx-auto max-w-2xl py-32 sm:py-48 lg:py-56 content-left">
          <HeadPage />
          <CalendarBooking :data_date="selectedDate" @dateCellClick="handleDateCellClick" @chooseOption="handleSelectOption"/>
          <ListSelectBooking :listBooking="dataBooking"/>
          <QuantitySelector 
          :quantity="quantity" 
          :min_quantity="min_quantity" 
          :max_quantity="max_quantity" 
          :sale_price="sale_price"
          @quantityClick="handleQuantityClick"
          />
          <button class="mt-3 w-full flex justify-center items-end bg-orange-500 px-2 py-4 rounded hover:bg-teal-400" @click="handleAddToCartClick" >
            <svg class="w-5 h-5 text-white dark:text-white mb-1" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 18 20">
                <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 5h4m-2 2V3M6 15a2 2 0 1 0 0 4 2 2 0 0 0 0-4Zm0 0h8m-8 0-1-4m9 4a2 2 0 1 0 0 4 2 2 0 0 0 0-4Zm.938-11H17l-2 7H5m0 0L3 4m0 0h2M3 4l-.792-3H1"/>
            </svg>
            <span class="pl-2 text-white text-base font-semibold">Add To Cart</span>
          </button>
      </div>
      <div class="absolute inset-x-0 top-[calc(100%-13rem)] -z-10 transform-gpu overflow-hidden blur-3xl sm:top-[calc(100%-30rem)]" aria-hidden="true">
        <div class="relative left-[calc(50%+3rem)] aspect-[1155/678] w-[36.125rem] -translate-x-1/2 bg-gradient-to-tr from-[#ff80b5] to-[#9089fc] opacity-30 sm:left-[calc(50%+36rem)] sm:w-[72.1875rem]" style="clip-path: polygon(74.1% 44.1%, 100% 61.6%, 97.5% 26.9%, 85.5% 0.1%, 80.7% 2%, 72.5% 32.5%, 60.2% 62.4%, 52.4% 68.1%, 47.5% 58.3%, 45.2% 34.5%, 27.5% 76.7%, 0.1% 64.9%, 17.9% 100%, 27.6% 76.8%, 76.1% 97.7%, 74.1% 44.1%)" />
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';

import HeadPage from './components/HeadPage.vue'
import CalendarBooking from './components/CalendarBooking.vue'
import ListSelectBooking from './components/ListSelectBooking.vue'
import QuantitySelector from './components/QuantitySelector.vue'

import ProductInfo from "./data/product_info.json"
import BookingData from "./data/booking_data.json"

export default {
  name: 'App',
  components: {
    HeadPage,
    CalendarBooking,
    ListSelectBooking,
    QuantitySelector
  },
  setup() {
    const formatDate = (date) => {
      const year = date.getFullYear();
      const month = String(date.getMonth() + 1).padStart(2, '0');
      const day = String(date.getDate()).padStart(2, '0');
      return `${year}-${month}-${day}`;
    };
    const selectedDate = ref(formatDate(new Date()));
    const handleDateSelected = (date) => {
      selectedDate.value = date;
    };
    const filteredServices = () => {
      return BookingData.filter(item => item.date === selectedDate.value)[0]?.services || [];
    };
    const dataBooking = filteredServices()
    const productInfo = ref(ProductInfo)
    const quantity = ref(ProductInfo.min_quantity)
    const min_quantity = ref(ProductInfo.min_quantity)
    const max_quantity = ref(ProductInfo.max_quantity)
    const sale_price = ref(ProductInfo.sale_price)
    const handleQuantityClick = (value) => {
      quantity.value = value
    }
    const subTotal = () => {
      return quantity.value * sale_price.value
    }
    const savings = () => {
      return quantity.value * sale_price.value
    }
    
    return {
      selectedDate,
      handleDateSelected,
      filteredServices,
      handleQuantityClick,
      dataBooking,
      productInfo,
      quantity,
      min_quantity,
      max_quantity,
      sale_price,
      subTotal,
      savings
    };
  },
  methods: {
    handleDateCellClick(bookingDate) {
      this.selectedDate = bookingDate;
      this.dataBooking = this.filteredServices();
    },
    handleSelectOption(option) {
      console.log(option);
    },
    chooseOptionsBookingData(){
      const datepickerEl = document.getElementById('list-select-booking');
      const chooseOptionsBooking = datepickerEl.querySelectorAll('.option-booking-room');
      const chooseOptionsData = []
      chooseOptionsBooking.forEach((data) => {
        const option = {
          room_name: data.getAttribute('data-room-name'),
          time_choose: data.textContent,
        };
        chooseOptionsData.push(option);
      });
      return chooseOptionsData;
    },
    handleAddToCartClick() {
      const dataReturn = {
        product_id: this.productInfo.id,
        choose_options: this.chooseOptionsBookingData(),
        quantity: this.quantity,
        sub_total: this.subTotal(),
        savings: this.savings()
      }
      console.log(dataReturn);
    },
  },
  provide() {
    return {
      product_name: this.productInfo.product_name,
      price: this.productInfo.price,
      sale_price: this.productInfo.sale_price,
      sale_percent: this.productInfo.sale_percent,
      detail_url: this.productInfo.detail_url,
    }
  },
}
</script>

<style>
</style>
