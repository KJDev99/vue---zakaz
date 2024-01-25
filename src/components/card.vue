<template>
    <div class="card">
        <div class="title">{{ food.title }}</div>
        <div class="text">{{ food.text }}</div>
        <div class="bottom">
            <div class="price">{{ food.price?.toLocaleString() || 0 }} so'm</div>
            <div class="order">
                <div class="summa">{{ summa?.toLocaleString() }} so'm</div>
                <button @click="setCount(1)">+</button>
                {{ count }}
                <button @click="setCount(-1)">-</button>
                <button :disabled="toggleDisable" @click="order()" class="call">Buyurtma</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['food'],
    data: () => ({
        count: 0,
        summa: 0,
        toggleDisable: true,
    }),
    methods: {
        order() {
            if (this.count == 0) return false
            this.$emit('zakaz', { count: this.count })
            this.count = 0
            this.summa = 0
            this.toggleDisable = true
        },
        setCount(val) {
            if (this.count == 0 && val == -1) return false
            this.count += val
            this.toggleDisable = this.count == 0
            this.summa = this.count * this.food.price
        }
    }
}
</script>

<style lang="scss">
@import '@/styles/card.scss';
</style>