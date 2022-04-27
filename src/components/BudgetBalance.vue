<template>
  <div class="total-balance" :value="total">
    <template v-if="total === 0">
      <div class="default">Баланс: {{ total }}</div>
    </template>
    <template v-if="total > 0">
      <div class="green">Баланс: {{ total }}</div>
    </template>
    <template v-if="total < 0">
      <div class="red">Баланс: {{ total }}</div>
    </template>
  </div>
</template>

<script>
export default {
  name: "BudgetBalance",
  data: () => ({
    value: 0,
  }),
  props: {
    total: {
      type: Number,
      default: 0,
    },
  },
};
</script>

<style lang="scss">
.total-balance {
  font-size: 26px;
  text-transform: uppercase;
  padding: 20px;
  text-align: center;
}
.default {
  color: #fff;
}
.green {
  color: green;
}
.red {
  color: red;
}
</style>
