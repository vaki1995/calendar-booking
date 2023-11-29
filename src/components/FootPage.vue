<template>
    <div class="border-t border-current pt-2">
        <div class="sm:flex justify-between items-end text-lg font-semibold">
            <div>
                Sub-total
            </div>
            <div>
                25.00$
            </div>
        </div>
        <div class="sm:flex justify-between items-end text-lg font-semibold mt-1">
            <div>
                Savings
            </div>
            <div class="text-green-600">
                25.00$
            </div>
        </div>
        <button class="mt-3 w-full sm:flex justify-center items-end bg-orange-500 px-2 py-4 rounded hover:bg-teal-400">
            <svg class="w-5 h-5 text-white dark:text-white mb-1" aria-hidden="true" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 18 20">
                <path stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 5h4m-2 2V3M6 15a2 2 0 1 0 0 4 2 2 0 0 0 0-4Zm0 0h8m-8 0-1-4m9 4a2 2 0 1 0 0 4 2 2 0 0 0 0-4Zm.938-11H17l-2 7H5m0 0L3 4m0 0h2M3 4l-.792-3H1"/>
            </svg>
            <span class="pl-2 text-white text-base font-semibold">Add To Cart</span>
        </button>
    </div>
</template>

<script>
    export default {
        name: "FootPage",
    }
</script>

<style scoped>

</style>