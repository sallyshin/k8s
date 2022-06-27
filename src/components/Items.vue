<template>
    <div :key="item.item_cd" v-for="item in items">
        <Item :item="item" @edit-item="$emit('edit-item', item)" @delete-item="$emit('delete-item', item.item_cd)" />
    </div>
</template>

<script>
import Item from './Item'

export default {
    name: 'Items',
    props: {
        items: Array
    },
    components: {
        Item
    },
    emits: ['edit-item', 'delete-item']
}
</script>