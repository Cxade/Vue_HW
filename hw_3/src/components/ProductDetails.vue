<template>
  <div class="products">
    <div class="product" v-for="product in products" :key="product.id">
      <h3>{{ product.name }}</h3>
      <button v-if="product.available" @click="toggleDescription(product.id)">
        Available
      </button>
      <p v-else>Out of stock</p>
      <p v-if="showDescriptions.includes(product.id)">
        {{ formattedPrice(product) }}$
      </p>
    </div>
  </div>
</template>
<script>
export default {
  name: "ProductDetails",
  data() {
    return {
      products: [
        {
          id: 1,
          name: "phone",
          price: 99999,
          available: true,
        },
        {
          id: 2,
          name: "razor",
          price: 13000,
          available: false,
        },
        {
          id: 3,
          name: "toy",
          price: 4000,
          available: false,
        },
        {
          id: 4,
          name: "notebook",
          price: 69750,
          available: true,
        },
      ],
      showDescriptions: [],
      dollarExchangeRate: 88.7,
    };
  },
  methods: {
    toggleDescription(id) {
      const findIndex = this.showDescriptions.indexOf(id);
      if (findIndex === -1) {
        this.showDescriptions.push(id);
      } else {
        this.showDescriptions.splice(findIndex, 1);
      }
    },
  },
  computed: {
    formattedPrice() {
      return (product) => {
        const priceInDollars = product.price / this.dollarExchangeRate;
        return priceInDollars.toFixed(2);
      };
    },
  },
};

// Вы разрабатываете приложение для интернет-магазина и у вас есть компонент Vue под названием "ProductDetails". Компонент отображает детали о конкретном продукте, включая его название, цену и статус доступности.
// Внутри компонента "ProductDetails" создайте свойство "product" с объектом, представляющим информацию о продукте. Объект должен иметь свойства "name" (название продукта), "price" (цена продукта) и "available" (флаг, указывающий на доступность продукта).
// Используя вычисляемое свойство, назовите его "formattedPrice", которое будет возвращать форматированную цену продукта со знаком валюты. Например, если цена равна 99.99, вычисляемое свойство должно вернуть строку "$99.99".
// В компоненте "ProductDetails" отобразите название продукта, его форматированную цену и статус доступности.
// Если продукт доступен, отобразите текст "Available", в противном случае - "Out of stock".
</script>
<style lang="scss" scoped>
.products {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
}
.product {
  width: 150px;
  border: 1px solid orange;
  border-radius: 30px;
  padding: 10px;
}
</style>
