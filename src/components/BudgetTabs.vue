<template>
  <div class="budget-tabs">
    <el-button
      v-for="(btn, index) in btns"
      :key="index"
      :type="btn.type"
      :class="[btn.class]"
      class="btn"
      round
      @click="activeTab(btn.class, index)"
    >
      {{ btn.name }}
    </el-button>
  </div>
</template>

<script>
export default {
  name: "BudgetTabs",
  data: () => ({
    btns: {
      1: {
        name: "Все",
        class: "All",
      },
      2: {
        name: "Доход",
        class: "Income",
        type: "success",
      },
      3: {
        name: "Расход",
        class: "Outcome",
        type: "warning",
      },
    },
  }),
  methods: {
    activeTab(btnClass, index) {
      this.$emit("clickBtnTab", btnClass, index);
    },
  },
};
</script>

<style lang="scss">
.btn.el-button.is-round {
  border-radius: 0;
}
</style>
