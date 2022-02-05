<template>
    <div>
        <form 
            accept-charset="UTF-8"
            v-on:submit.prevent="onSubmit()"
            method="POST"
        >
                    <div>
                    <input v-model="departure_address" placeholder="departure_address">
                    </div>
                    <div>
                    <input v-model="destination_address" placeholder="destination_address">
                    </div>
                    <div>
                    <input v-model="weight" placeholder="weight">
                    </div>
                    <div>
                    <input v-model="volume" placeholder="volume">
                    </div>
                    <div>
                    <select v-model="type">
                        <option>truck</option>
                        <option>train</option>
                        <option>ship</option>
                        <option>plain</option>
                    </select>
                    </div>
                    <div>
                    <select v-model="departure_city">
                        <option>Москва</option>
                        <option>Санкт-Петербург</option>
                        <option>Новосибирск</option>
                        <option>Екатеринбург</option>
                        <option>Казань</option>
                        <option>Нижний Новгород</option>
                        <option>Челябинск</option>
                        <option>Самара</option>
                        <option>Омск</option>
                        <option>Ростов-на-Дону</option>
                        <option>Уфа</option>
                        <option>Красноярск</option>
                        <option>Воронеж</option>
                        <option>Пермь</option>
                        <option>Волгоград</option>
                        <option>Краснодар</option>
                        <option>Саратов</option>
                        <option>Тюмень</option>
                        <option>Тольятти</option>
                        <option>Ижевск</option>
                    </select>
                    </div>
                    <div>
                    <select v-model="destination_city">
                        <option>Москва</option>
                        <option>Санкт-Петербург</option>
                        <option>Новосибирск</option>
                        <option>Екатеринбург</option>
                        <option>Казань</option>
                        <option>Нижний Новгород</option>
                        <option>Челябинск</option>
                        <option>Самара</option>
                        <option>Омск</option>
                        <option>Ростов-на-Дону</option>
                        <option>Уфа</option>
                        <option>Красноярск</option>
                        <option>Воронеж</option>
                        <option>Пермь</option>
                        <option>Волгоград</option>
                        <option>Краснодар</option>
                        <option>Саратов</option>
                        <option>Тюмень</option>
                        <option>Тольятти</option>
                        <option>Ижевск</option>
                    </select>
                    </div>
            <button class="submit-btn" type="submit">Отправить</button>
        </form>
    </div>
</template>

<style scoped>
    .submit-btn {
        background: #fefefe;
        padding: 10px;
        color: #000;
        border-radius: 10px;
    }

    select {
        background: #fff;
        padding: 5px;
        border-radius: 10px;
    }

    .form-line {
        margin-bottom: 15px
    }

    input {
        background: #fff;
        color: #000;
        padding: 10px;
        border-radius: 10px;
    }
</style>

<script>
export default {
  async fetch({store}) {
    await store.dispatch('orderForm/fetch')
  },
  computed: {
    orderForm() {
      return this.$store.getters['orderForm/orderForm']
    }
  },
  data() {
      return {
        type: '',
        departure_city: '',
        departure_address: '',
        destination_city: '',
        destination_address: '',
        weight: '',
        volume: ''
    }
  },
  methods: {
      async onSubmit() {
        const data = {
            type: this.type,
            departure_city: this.departure_city,
            departure_address: this.departure_address,
            destination_city: this.destination_city,
            destination_address: this.destination_address,
            weight: this.weight,
            volume: this.volume
        }  
        if (
            data.type === '' ||
            data.departure_city === '' ||
            data.departure_address === '' ||
            data.destination_city === '' ||
            data.destination_address === '' ||
            data.weight === '' ||
            data.volume === '' 
        ) {
            alert('Заполните все поля формы')
        } else {
            await this.$store.dispatch('orderForm/postForm', data)
            await this.$store.dispatch('refresh')
        }
      }
  }
}
</script>