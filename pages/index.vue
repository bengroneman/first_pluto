<template>
 <div class="container">
    <h1 class="py-4">Dietary Ordering System</h1>
    <div class="row justify-content-md-center">
        <aside class="col col-lg-3">
            <Cart :items="cart"></Cart>
        </aside>
        <aside class="col-md-auto">
            <!-- Filters -->
            <Filters></Filters>

            <!-- Search -->
            <Search></Search>

            <!-- Dietary Item Table -->
            <DietaryItemTable>
                <DietaryItemRow
                    v-for="dietary_item in dietary_items"
                    :key="dietary_item.id"
                    :item="dietary_item"
                    @add-to-cart="addItemToCart"
                >
                </DietaryItemRow>
            </DietaryItemTable>
        </aside>
    </div>
  </div>
</template>

<script>
export default {
    // TODO: DRY up the HTML
    data() {
        return {
            dietary_items: [],
            cart: [],
        }
    },

    async mounted() {
        await this.fetchDietaryItems()
    },

    methods: {
        async fetchDietaryItems() {
            const items = await this.$axios.$get('http://localhost:8000/dietary/api/v1/items')
            this.dietary_items = items
        },

        addItemToCart: function (item) {
            // TODO: determine why the prop data in Cart component is not re-rendering the quantity
            const item_in_cart = _.findIndex(this.cart, function(i) { return i.id == item.id })
            console.log(item_in_cart)

            if (item_in_cart === -1) {
                item.quantity = 1
                this.cart.push(item)
            } else {
                item.quantity += 1 
            }
        },
        
        removeItemFromCart: function(item) {
            // TODO: build this based on item id
        },
    },
}
</script>
