<template>
  <div>
    <div
      v-for="(item, index) in list"
      :key="index"
      v-show="visibleList || typeTbs == 'All' || typeTbs == item.type"
    >
      <i class="list-item" :class="[item.styled]">
        <span class="budget-comment">
          {{ item.comment }}
        </span>
        <span class="budget-value">
          {{ item.value }}
        </span>
        <el-button type="danger" size="mini" @click="onDeleteItem(item.id)">
          Удалить
        </el-button>
      </i>
    </div>
  </div>
</template>

<script>
export default {
  name: "BudgetListItem",
  props: {
    list: {
      type: Object,
      default: () => ({}),
    },
    notView: {
      type: Boolean,
    },
    typeTbs: {
      type: String,
    },
    visibleList: {
      type: Boolean,
    },
  },
  methods: {
    onDeleteItem(id) {
      this.$emit("deleteItem", id);
    },
  },
};
</script>

<style lang="scss">
.budget-list-wrap .list-item {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 15px;
}
.budget-value {
  font-weight: bold;
  margin-left: auto;
  margin-right: 20px;
}
.green {
  color: #00ff00;
}
.red {
  color: #ffeb00;
}
</style>
