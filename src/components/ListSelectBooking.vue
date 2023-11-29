<template>
    <div class="mb-4">
        <ul>
            <li v-for="(item, index) in listBooking" :key="index"> 
                <div>Choose your time of visit <span class="font-semibold">( {{ item.room_name }} )</span></div>
                <SelectBooking :infoBooking="item.options" :selectOption="item.options[0]" />
            </li>
        </ul> 
    </div>
</template>

<script>
import SelectBooking from './SelectBooking.vue'
    export default {
        name: "ListSelectBooking",
        components: {
            SelectBooking
        },
        props: {
            listBooking: {
                type: Object,
                required: true
            }
        }
    }
</script>

<style scoped>

</style>