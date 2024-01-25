<template>
    <table>
        <thead>
            <th>N</th>
            <th>Ovqat Nomi</th>
            <th>Ovqat Narxi</th>
            <th>Buyurtma Soni</th>
            <th>Buyurtma vaqti</th>
            <th>Summasi</th>
        </thead>
        <tbody>
            <tr v-for="order, index of orders" :key="index">
                <td>{{ index + 1 }}</td>
                <td>{{ order.title }}</td>
                <td>{{ order.price?.toLocaleString() }} so'm</td>
                <td>{{ order.count }} ta</td>
                <td>{{ order.date.toLocaleString() }}</td>
                <td>{{ (order.count * order.price).toLocaleString() }} so'm</td>
            </tr>
        </tbody>
    </table>
</template>

<script>
export default {
    props: ['orders']
}
</script>

<style lang="scss">
@import '@/styles/table.scss'
</style>