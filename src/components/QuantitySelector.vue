<template>
    <div class="sm:flex items-center justify-between mb-2 px-1 py-2 border rounded border-cyan-500">
        <button @click="subtractQuantity" class="sm:flex pb-1 justify-center items-center h-5 w-5 border rounded-full border-cyan-500 font-medium text-cyan-500 hover:border-orange-600 hover:text-orange-600">
        -
        </button>
        <input 
        v-model="quantity"
        @input="handleInput"
        :min="min_quantity"
        :max="max_quantity"
        class="w-10 text-center font-bold text-xl" 
        />
        <button @click="addQuantity" class="sm:flex pb-1 justify-center items-center h-5 w-5 border rounded-full border-cyan-500 font-medium text-cyan-500 hover:border-orange-600 hover:text-orange-600">
        +
        </button>
    </div>
    <div class="text-right text-xs mb-4">
        Quantity: Min {{ min_quantity }} - Max {{ max_quantity }}
    </div>
</template>

<script>
    export default {
        name: "QuantitySelector",
        inject: {
            min_quantity: {
                type: Number,
                required: true,
            },
            max_quantity: {
                type: Number,
                required: true,
            }
        },
        data() {
            return {
                quantity: 1,
            };
        },
        methods: {
            addQuantity() {
                if(this.quantity < this.max_quantity) {
                    this.quantity += 1;
                }
            },
            subtractQuantity() {
                if (this.quantity > this.min_quantity) {
                    this.quantity -= 1;
                }
            },
            handleInput() {
                if (this.quantity < this.min_quantity) {
                    this.quantity = this.min_quantity;
                } else if (this.quantity > this.max_quantity) {
                    this.quantity = this.max_quantity;
                }
            },
        },
    }
</script>

<style scoped>

</style>