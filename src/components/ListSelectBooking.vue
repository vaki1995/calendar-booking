<template>
    <div class="mb-4" id="list-select-booking">
        <div v-if="listBooking.length">
            <ul>
                <li v-for="(item, index) in listBooking" :key="index"> 
                    <div>Choose your time of visit <span class="font-semibold">( {{ item.room_name }} )</span></div>
                    <SelectBooking :infoBooking="item.options" :selectOption="item.options[0]" :roomName="item.room_name" :open="true"/>
                </li>
            </ul> 
        </div>
        <div v-else>
            <p class="text-center py-2 text-current font-semibold text-lg">No data options</p>
        </div>
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