<template>
  <div class="bg-white font-sans">
    <div class="relative isolate px-6 pt-14 lg:px-8">
      <div class="absolute inset-x-0 -top-40 -z-10 transform-gpu overflow-hidden blur-3xl sm:-top-80" aria-hidden="true">
        <div class="relative left-[calc(50%-11rem)] aspect-[1155/678] w-[36.125rem] -translate-x-1/2 rotate-[30deg] bg-gradient-to-tr from-[#ff80b5] to-[#9089fc] opacity-30 sm:left-[calc(50%-30rem)] sm:w-[72.1875rem]" style="clip-path: polygon(74.1% 44.1%, 100% 61.6%, 97.5% 26.9%, 85.5% 0.1%, 80.7% 2%, 72.5% 32.5%, 60.2% 62.4%, 52.4% 68.1%, 47.5% 58.3%, 45.2% 34.5%, 27.5% 76.7%, 0.1% 64.9%, 17.9% 100%, 27.6% 76.8%, 76.1% 97.7%, 74.1% 44.1%)" />
      </div>
      <div class="mx-auto max-w-2xl py-32 sm:py-48 lg:py-56 content-left">
          <HeadPage />
          <CalenderBooking />
          <ListSelectBooking :listBooking="bookingData[1].services"/>
          <QuantitySelector />
          <FootPage />
      </div>
      <div class="absolute inset-x-0 top-[calc(100%-13rem)] -z-10 transform-gpu overflow-hidden blur-3xl sm:top-[calc(100%-30rem)]" aria-hidden="true">
        <div class="relative left-[calc(50%+3rem)] aspect-[1155/678] w-[36.125rem] -translate-x-1/2 bg-gradient-to-tr from-[#ff80b5] to-[#9089fc] opacity-30 sm:left-[calc(50%+36rem)] sm:w-[72.1875rem]" style="clip-path: polygon(74.1% 44.1%, 100% 61.6%, 97.5% 26.9%, 85.5% 0.1%, 80.7% 2%, 72.5% 32.5%, 60.2% 62.4%, 52.4% 68.1%, 47.5% 58.3%, 45.2% 34.5%, 27.5% 76.7%, 0.1% 64.9%, 17.9% 100%, 27.6% 76.8%, 76.1% 97.7%, 74.1% 44.1%)" />
      </div>
    </div>
  </div>
</template>

<script>
import HeadPage from './components/HeadPage.vue'
import CalenderBooking from './components/Calender.vue'
import ListSelectBooking from './components/ListSelectBooking.vue'
import QuantitySelector from './components/QuantitySelector.vue'
import FootPage from './components/FootPage.vue'
import ProductInfo from "./data/product_info.json"
import BookingData from "./data/booking_data.json"

export default {
  name: 'App',
  components: {
    HeadPage,
    CalenderBooking,
    ListSelectBooking,
    QuantitySelector,
    FootPage
  },
  data() {
    console.log(BookingData[0].services)
    return {
      productInfo: ProductInfo,
      bookingData: BookingData
    }
  },
  provide() {
    return {
      product_name: this.productInfo.product_name,
      price: this.productInfo.price,
      sale_price: this.productInfo.sale_price,
      sale_percent: this.productInfo.sale_percent,
      detail_url: this.productInfo.detail_url,
      min_quantity: this.productInfo.min_quantity,
      max_quantity: this.productInfo.max_quantity,
    }
  }
}
</script>

<style>
</style>
