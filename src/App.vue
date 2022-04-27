<template>
  <div id="app" v-cloak>
    <base-container>
      <div class="budget">
        <BudgetForm @submitForm="onSubmit" />
        <BudgetList
          :list="list"
          :typeTbs="typeTbs"
          :alertVisible="alertVisible"
          :visibleList="visibleList"
        />
      </div>
      <BudgetBalance :total="totalBalance" />
      <BudgetTabs @clickBtnTab="clickBtnTab" />

      <el-dialog
        title="Внимание!"
        :visible.sync="centerDialogVisible"
        width="30%"
        center
        closable="false"
      >
        <span>Введите отрицательное число</span>
        <span slot="footer" class="dialog-footer">
          <el-button type="primary" @click="centerDialogVisible = false"
            >Ок</el-button
          >
        </span>
      </el-dialog>
    </base-container>
  </div>
</template>

<script>
import BudgetBalance from "@/components/BudgetBalance.vue";
import BudgetTabs from "@/components/BudgetTabs.vue";
import BudgetForm from "@/components/BudgetForm.vue";
import BudgetList from "./components/BudgetList.vue";
import BaseContainer from "@/components/BaseContainer";

export default {
  name: "App",
  components: {
    BaseContainer,
    BudgetBalance,
    BudgetForm,
    BudgetList,
    BudgetTabs,
  },
  data: () => ({
    text: "Budget",
    typeTbs: "",
    visibleList: true,
    centerDialogVisible: false,
    alertVisible: true,
    list: {
      1: {
        type: "Income",
        value: 100,
        comment: "Какой то доход",
        id: 1,
        styled: "color: green el-icon-top",
        isNotActive: false,
      },
      2: {
        type: "Outcome",
        value: -50,
        comment: "Какая то трата 1",
        id: 2,
        styled: "color: red el-icon-bottom",
        isNotActive: false,
      },
    },
  }),
  computed: {
    totalBalance() {
      const balance = Object.values(this.list).reduce(
        (acc, item) => acc + item.value,
        0
      );
      return balance;
    },
  },
  methods: {
    onSubmit(data) {
      const newObj = {
        ...data,
        id: String(Math.random()),
      };
      if (newObj.type === "Income") {
        newObj.styled = "color: green el-icon-top";
      } else {
        newObj.styled = "color: red el-icon-bottom";
      }
      if (newObj.value > 0 && newObj.type === "Outcome") {
        this.centerDialogVisible = !this.centerDialogVisible;
        return this.list;
      }
      this.$set(this.list, newObj.id, newObj);
    },
    clickBtnTab(btnClass) {
      Object.values(this.list).forEach((item) => {
        if (btnClass === item.type) {
          this.typeTbs = btnClass;
          this.visibleList = item.isNotActive;
        } else if (btnClass === "All") {
          this.typeTbs = btnClass;
        }
        Object.values(this.list);
        if (
          Object.keys(this.list).length === 1 &&
          (btnClass === "Income" || btnClass === "Outcome")
        ) {
          this.alertVisible = !this.alertVisible;
        }
        return this.alertVisible;
      });
    },
  },
};
</script>

<style lang="scss">
[v-cloak] {
  display: none;
}
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background: #161110;
}

#app {
  font-family: system-ui, -apple-system, "Segoe UI", Roboto, "Helvetica Neue",
    Arial, "Noto Sans", "Liberation Sans", sans-serif, "Apple Color Emoji",
    "Segoe UI Emoji", "Segoe UI Symbol", "Noto Color Emoji";
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #fff;
  margin-top: 60px;
}

.budget {
  display: grid;
  grid-template-columns: repeat(2, minmax(450px, 550px));
  gap: 20px;
  justify-content: center;
}

@media (max-width: 991px) {
  .budget {
    grid-template-columns: repeat(2, minmax(350px, 450px));
  }
}

@media (max-width: 768px) {
  .budget {
    grid-template-columns: repeat(1, minmax(250px, 450px));
  }

  .budget .el-card__body {
    padding: 10px;
  }
}
</style>
