<template>
    <h2 class="text-2xl font-semibold text-cyan-500 pb-3">{{ product_name }}</h2>
    <div class="sm:flex justify-between items-baseline text-slate-600">
        <div class="sm:flex font-normal text-lg">
            <p class="line-through text-red-500">{{ price.toFixed(2) }}$</p>
            <p class="pl-2">{{ sale_price.toFixed(2) }}$</p>
        </div>
        <div class="sm:flex items-end">
            <div class="font-bold text-3xl">{{ sale_price.toFixed(2) }}$</div>
            <div class="px-2 text-sm">each</div>
            <div class="bg-teal-100 text-emerald-600 text-sm py-1 px-2 rounded font-medium">{{ sale_percent }} Off</div>
        </div>
    </div>
    <div class="text-right mt-3">
        <a :href="detail_url" class="underline font-semibold text-rose-400 text-lg hover:text-green-600">See Details</a>
    </div>
</template>

<script>
    export default {
        name: "HeadPage",
        inject: {
            product_name: {
                type: String,
                required: true,
            },
            price: {
                type: Number,
                required: true,
            },
            sale_price: {
                type: Number,
                required: true,
            },
            sale_percent: {
                type: String,
                required: true,
            },
            detail_url: {
                type: String,
                required: true,
            }
        }
    }
</script>

<style scoped>

</style>