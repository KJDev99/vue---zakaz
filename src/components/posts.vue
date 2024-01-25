<template>
    <table>
        <thead>
            <th>ID</th>
            <th>Sarlavha</th>
            <th>Matn</th>
            <th>Foydalanuvchi ID</th>
        </thead>
        <tbody>
            <tr v-for="post of posts" :key="post.id">
                <td>{{ post.id }}</td>
                <td>{{ post.title }}</td>
                <td>{{ post.body }}</td>
                <td>{{ post.userId }}</td>
            </tr>
        </tbody>
    </table>
</template>

<script>
export default {
    props: ['posts']
}
</script>

<style lang="scss">
@import '@/styles/table.scss'
</style>