<template>
  <div class="converter">
    <div class="first-rate" v-if="firstCurrency">
      1 {{ firstCurrency.text }} равно
    </div>
    <div class="second-rate" v-if="secondCurrency">
      {{
        (firstCurrency.exchangeRate / secondCurrency.exchangeRate).toFixed(2)
      }}
      {{ secondCurrency.text }}
    </div>
    <div class="first-rate-container">
      <input
        v-model="firstRate.value"
        type="number"
        @input="changeFirstRate()"
      />
      <select v-model="firstRate.currency" @change="changeFirstRate()">
        <option
          :key="index"
          :value="JSON.stringify(currency)"
          v-for="(currency, index) in filterFirstCurrencies"
        >
          {{ currency.text }}
        </option>
      </select>
    </div>
    <div class="first-rate-container">
      <input
        v-model="secondRate.value"
        type="number"
        @input="changeSecondRate()"
      />
      <select v-model="secondRate.currency" @change="changeSecondRate()">
        <option
          :key="index"
          :value="JSON.stringify(currency)"
          v-for="(currency, index) in filterSecondCurrencies"
        >
          {{ currency.text }}
        </option>
      </select>
    </div>
  </div>
</template>

<script>
export default {
  name: "vConverter",

  props: {
    currencies: Array,
  },

  data: () => ({
    firstRate: {
      value: "",
      currency: "",
    },
    secondRate: {
      value: "",
      currency: "",
    },
  }),

  computed: {
    firstCurrency() {
      if (this.firstRate.currency) {
        return JSON.parse(this.firstRate.currency);
      }
      return "";
    },
    secondCurrency() {
      if (this.secondRate.currency) {
        return JSON.parse(this.secondRate.currency);
      }
      return "";
    },
    filterFirstCurrencies() {
      if (this.secondCurrency) {
        return this.currencies.filter(
          (item) => item.value !== this.secondCurrency.value
        );
      }

      return this.currencies;
    },
    filterSecondCurrencies() {
      if (this.firstCurrency) {
        return this.currencies.filter(
          (item) => item.value !== this.firstCurrency.value
        );
      }

      return this.currencies;
    },
  },

  mounted() {
    this.firstRate.currency = JSON.stringify(this.currencies[0]);
    this.secondRate.currency = JSON.stringify(this.currencies[1]);

  },

  methods: {
    changeFirstRate() {
      this.secondRate.value = (
        this.firstRate.value *
        (this.firstCurrency.exchangeRate / this.secondCurrency.exchangeRate)
      ).toFixed(2);
    },
    changeSecondRate() {
      this.firstRate.value = (
        this.secondRate.value *
        (this.secondCurrency.exchangeRate / this.firstCurrency.exchangeRate)
      ).toFixed(2);
    },
  },
};
</script>

<style scoped>
.converter {
  width: 400px;
  padding: 40px;
  border: 1px solid black;
  border-radius: 16px;
  margin: 200px auto;
  background-color: aliceblue;
  font-family: Verdana, Arial, sans-serif;
}

.first-rate {
  font-size: 16px;
  margin-bottom: 12px;
}

.second-rate {
  font-size: 20px;
  margin-bottom: 20px;
  font-weight: bold;
}

.first-rate-container {
  margin-bottom: 12px;
  display: flex;
}

.first-rate-container input {
  width: 50%;
  border-radius: 8px;
  border: 1px solid grey;
  padding: 4px;
}

.first-rate-container select {
  width: 50%;
  height: 36px;
  border-radius: 8px;
  border: 1px solid grey;
  margin-left: 8px;
  padding: 4px;
}
</style>
