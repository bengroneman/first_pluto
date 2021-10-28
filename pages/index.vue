<template>
 <div class="container">
    <h1 class="py-4">Dietary Ordering System</h1>
    <div class="row justify-content-md-center">
        <aside class="col col-lg-3">
            <Cart
                :items="cart"
                @checkout="checkoutItems"
            >
            </Cart>
        </aside>
        <aside class="col-md-auto">
            <!-- Filters -->
            <Filters
              @facilityChanged="updateFacility"
              @departmentChanged="updateDepartment"
            ></Filters>

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
      filters: {
        'department': String,
        'facility': String,
      },
    };
  },

  async mounted() {
    await this.fetchDietaryItems();
  },

  methods: {
    async fetchDietaryItems() {
      const items = await this.$axios.$get('http://localhost:8000/dietary/api/v1/items');
      this.dietary_items = items;
    },

    addItemToCart: async function(item) {
      // TODO: determine why the prop data in Cart component is not re-rendering
      const itemInCart = _.findIndex(this.cart, function(i) {
        return i.id == item.id;
      });

      if (itemInCart === -1) {
        item.quantity = 1;
        this.cart.push(item);
      } else {
        // This should force the update in theory..
        await this.$nextTick();
        item.quantity += 1;
      }
    },

    checkoutItems: async function() {
      const itemEndpoint = 'http://localhost:8000/dietary/api/v1/items';
      if (_.isEmpty(this.cart)) {
        console.error('cannot checkout an empty cart');
      }

      const response = this.$axios.$post(itemEndpoint, this.cart);
      if (response.ok) {
        console.log('successful checkout');
      } else {
        console.log('Whoops checkout failed');
      }
    },

    updateFacility: function(newFacility) {
      this.filters.facility = newFacility;
    },

    updateDepartment: function(updateDepartment) {
      this.filters.department = updateDepartment;
    },

    removeItemFromCart: function(item) {
      // TODO: build this based on item id
    },
  },
};
</script>
