<template>
  <nav>
    <button :class="{ active: toggle == 'main' }" @click="toggle = 'main'">Bosh Sahifa</button>
    <button :class="{ active: toggle == 'menu' }" @click="toggle = 'menu'">Menu</button>
    <button :class="{ active: toggle == 'order' }" @click="toggle = 'order'">Buyurtmalar</button>
  </nav>

  <div v-show="toggle == 'main'">
    <Posts :posts="posts" />
  </div>

  <div v-show="toggle == 'menu'">
    <card v-for="food, index of foods" :key="index" :food="food" @zakaz="({ count }) => {
      orderNow(index, count)
    }" />
  </div>
  <div v-show="toggle == 'order'">
    <Table :orders="orders"></Table>
  </div>
</template>

<script>
import card from '@/components/card.vue';
import Table from './components/table.vue';
import axios from 'axios'
import Posts from './components/posts.vue';
export default {
  components: {
    card,
    Table,
    Posts
  },
  data() {
    return {
      person: 'Bobur',
      toggle: 'main',
      orders: [],
      foods: [
        {
          title: 'Osh',
          text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Debitis placeat, aperiam nesciunt            consequatur at distinctio delectus odit nihil molestias? Cum facere obcaecati esse eligendi odio.',
          price: 37000
        },
        {
          title: 'Lagmon',
          text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Debitis placeat, aperiam nesciunt            consequatur at distinctio delectus odit nihil molestias? Cum facere obcaecati esse eligendi odio.',
          price: 17000
        },
        {
          title: 'Shorva',
          text: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Debitis placeat, aperiam nesciunt            consequatur at distinctio delectus odit nihil molestias? Cum facere obcaecati esse eligendi odio.',
          price: 22000
        },
      ],
      posts: []
    }
  },
  methods: {
    orderNow(index, count) {
      // this.orders.unshift({
      //   title: this.foods[index].title,
      //   price: this.foods[index].price,
      //   date: new Date(),
      //   count
      // })
      const newOrder = {
        title: this.foods[index].title,
        price: this.foods[index].price,
        date: new Date(),
        count
      }
      this.orders = [newOrder, ...this.orders]
    },
    getPosts() {
      axios.get('https://jsonplaceholder.typicode.com/posts').then(list => {
        this.posts = [...list.data]
      })
    }
  },
  mounted() {
    this.getPosts()
  }
}
</script>

<style lang="scss">
@import '@/styles/main.scss';
</style>