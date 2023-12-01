<template>
    <div class="border-t border-current pt-2">
        <div class="flex justify-between items-end text-lg font-semibold">
            <div>
                Sub-total
            </div>
            <div>
                {{sub_total.toFixed(2)}}$
            </div>
        </div>
        <div class="flex justify-between items-end text-lg font-semibold mt-1">
            <div>
                Savings
            </div>
            <div class="text-green-600">
                {{savings.toFixed(2)}}$
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: "FootPage",
        props: {
            sub_total: {
                type: Number,
                required: true,
            },
            savings: {
                type: Number,
                required: true,
            }
        },
        methods: {
            handleAddToCartClick() {
                const data = {
                    sub_total: this.sub_total,
                    savings: this.savings
                };
                console.log(data);
            },
        }
    }
</script>

<style scoped>

</style>