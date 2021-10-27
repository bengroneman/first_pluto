<template>
  <tr>
    <td>{{ item.title }}</td>
    <td>{{ item.cost }}</td>
    <td>{{ item.unit }}</td>
    <td class="text-truncate mw-150">{{ item.shelf_life }}</td>
    <td>{{ item.category }}</td>
    <td>
      <button
        class="btn btn-outline-secondary"
        type="button"
        @click="$emit('add-to-cart', item)"
      >
        Add to Cart
      </button>
    </td>
  </tr>
</template>

<script>
export default {
    props: {
        item: {},
    },
    emits: ['add-to-cart']
}
</script>

<style lang="css">
.mw-150 {
    max-width: 150px;
}
</style>
