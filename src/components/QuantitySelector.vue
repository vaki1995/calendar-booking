<template>
    <div class="flex items-center justify-between mb-2 px-1 py-2 border rounded border-cyan-500">
        <button @click="subtractQuantity" class="flex pb-1 justify-center items-center h-5 w-5 border rounded-full border-cyan-500 font-medium text-cyan-500 hover:border-orange-600 hover:text-orange-600">
        -
        </button>
        <input 
        v-model="inject_quantity"
        @input="handleInput"
        :min="min_quantity"
        :max="max_quantity"
        class="w-10 text-center font-bold text-xl" 
        />
        <button @click="addQuantity" class="flex pb-1 justify-center items-center h-5 w-5 border rounded-full border-cyan-500 font-medium text-cyan-500 hover:border-orange-600 hover:text-orange-600">
        +
        </button>
    </div>
    <div class="text-right text-xs mb-4">
        Quantity: Min {{ min_quantity }} - Max {{ max_quantity }}
    </div>
    <FootPage :sub_total="this.sub_total" :savings="this.savings" />
</template>

<script>
import FootPage from './FootPage.vue'
    export default {
        name: "QuantitySelector",
        components: {
            FootPage
        },
        props: {
            quantity: {
                type: Number,
                required: true,
            },
            min_quantity: {
                type: Number,
                required: true,
            },
            max_quantity: {
                type: Number,
                required: true,
            },
            sale_price: {
                type: Number,
                required: true,
            },
        },

        data() {
            return {
                inject_quantity: this.quantity,
                sub_total: this.min_quantity * this.sale_price,
                savings: this.min_quantity * this.sale_price,
            };
        },
        methods: {
            addQuantity() {
                console.log(this.inject_quantity, this.max_quantity);
                if(this.inject_quantity < this.max_quantity) {
                    this.inject_quantity += 1;
                    this.sub_total = this.inject_quantity * this.sale_price;
                    this.savings = this.inject_quantity * this.sale_price;
                    this.$emit('quantityClick', this.inject_quantity);
                }
            },
            subtractQuantity() {
                if (this.inject_quantity > this.min_quantity) {
                    this.inject_quantity -= 1;
                    this.sub_total = this.inject_quantity * this.sale_price;
                    this.savings = this.inject_quantity * this.sale_price;
                    this.$emit('quantityClick', this.inject_quantity);
                }
            },
            handleInput() {
                if (this.inject_quantity < this.min_quantity) {
                    this.inject_quantity = this.min_quantity;
                } else if (this.inject_quantity > this.max_quantity) {
                    this.inject_quantity = this.max_quantity;
                }
            },
        },
    }
</script>

<style scoped>

</style>