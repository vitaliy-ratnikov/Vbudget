<template>
  <div class="budget-list-wrap">
    <template>
      <ElCard :header="header">
        <BudgetListItem
          :list="list"
          @deleteItem="deleteItemList"
          :typeTbs="typeTbs"
          :visibleList="visibleList"
          v-if="alertVisible"
        />
        <ElAlert type="info" :title="emptyTitle" v-else :closable="false" />
      </ElCard>
    </template>
  </div>
</template>

<script>
import BudgetListItem from "./BudgetListItem.vue";

export default {
  components: {
    BudgetListItem,
  },
  name: "BudgetList",
  data: () => ({
    header: "Budget List",
    emptyTitle: "Нет данных",
  }),
  props: {
    list: {
      type: Object,
      default: () => ({}),
    },
    typeTbs: {
      type: String,
    },
    alertVisible: {
      type: Boolean,
    },
    visibleList: {
      type: Boolean,
    },
  },
  methods: {
    deleteItemList(id) {
      this.$delete(this.list, id);
    },
  },
};
</script>

<style lang="scss">
.budget-list-wrap .el-card__body {
  max-height: 300px;
  overflow-y: auto;
}
</style>
