<template>
    <div>
        <h3>Cart</h3>
        <ul v-if="items" class="list-group">
            <li v-for="(item, index) in items" :key="item.id" class="list-group-item">
                {{ item.title }} x <span>{{ item.quantity }}</span>
                <button type="button" class="btn-close" aria-label="Remove dietary item"></button>
            </li>
        </ul>
        <button class="btn btn-primary">Checkout</button>
    </div>
</template>

<script>
export default {
    props: {
        items: Array,
    },
}
</script>
