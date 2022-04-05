<template>
  <div id="app">
    <Converter :currencies="currencies" />
  </div>
</template>

<script>
import Converter from "./components/Converter.vue";

export default {
  name: "App",

  components: {
    Converter,
  },

  data: () => ({
    currencies: [
      {
        text: "Евро",
        value: "eur",
        exchangeRate: 20.3,
      },
      {
        text: "Американский доллар",
        value: "usd",
        exchangeRate: 18.35,
      },
      {
        text: "Российский рубль",
        value: "rub",
        exchangeRate: 0.22,
      },
      {
        text: "Молдавский лей",
        value: "mdl",
        exchangeRate: 1,
      },
      {
        text: "Украинская гривна",
        value: "uah",
        exchangeRate: 0.62,
      },
    ],
  }),
};
</script>
