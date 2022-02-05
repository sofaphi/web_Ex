<template>
    <div>
        <ul>
            <li v-for="(sale, index) of sales" :key="index">
              <p>Тип: {{sale.type}}</p>
              <p>Город отправки: {{sale.departure_city}}</p>
              <p>Адрес отправки: {{sale.departure_address}}</p>
              <p>Город назначения: {{sale.destination_city}}</p>
              <p>Адрес назначения: {{sale.destination_address}}</p>
              <p>Вес товара: {{sale.weight}}</p>
              <p>Объём товара: {{sale.volume}}</p>
            </li>
        </ul>
    </div>
</template>

<script>

export default {
  async fetch({store}) {
    if (store.getters['orders/sales'].length === 0) {
      await store.dispatch('orders/fetch')
    }
  },
  computed: {
    sales() {
        return this.$store.getters['orders/sales'];
    }
  }
}
</script>