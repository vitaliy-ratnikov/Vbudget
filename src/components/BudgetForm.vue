<template>
  <ElCard class="card-form">
    <ElForm :model="formData" ref="addItemForm" :rules="rules">
      <ElFormItem label="Тип">
        <ElSelect v-model="formData.type">
          <ElOption label="Доход" value="Income" />
          <ElOption label="Расход" value="Outcome" />
        </ElSelect>
      </ElFormItem>
      <ElFormItem label="Описание" prop="comment">
        <ElInput v-model="formData.comment" />
      </ElFormItem>
      <ElFormItem label="Значение" prop="value">
        <ElInput v-model.number="formData.value" />
      </ElFormItem>
      <ElButton @click="onSubmit" type="primary">Добавить</ElButton>
    </ElForm>
  </ElCard>
</template>

<script>
export default {
  name: "BudgetForm",
  data: () => ({
    formData: {
      type: "Income",
      comment: "",
      value: null,
      styled: "",
    },
    rules: {
      comment: [
        {
          required: true,
          message: "Добавьте комментарий",
          trigger: "change",
        },
      ],
      value: [
        {
          required: true,
          message: "Добавьте значение",
          trigger: "change",
        },
      ],
    },
  }),
  props: {
    centerDialogVisible: {
      type: Boolean,
    },
  },
  methods: {
    onSubmit() {
      const strCheck = {
        type: "number",
        message: "Значение не должно быть строкой",
        trigger: "change",
      };
      const zeroCheck = {
        message: "Значение не может быть 0",
        trigger: "change",
      };
      if (this.formData.value === 0) {
        this.$set(this.rules.value, 1, zeroCheck);
      } else if (typeof this.formData.value === "string") {
        this.$set(this.rules.value, 2, strCheck);
      } else {
        this.rules.value.splice(1, 1);
        this.rules.value.splice(1, 2);
      }
      this.$refs.addItemForm.validate((valid) => {
        if (valid) {
          this.$emit("submitForm", { ...this.formData });
          this.$refs.addItemForm.resetFields();
        }
      });
    },
  },
};
</script>

<style lang="scss">
.card-form.el-card,
.budget-list-wrap .el-card {
  background-color: #3e0ba1;
  color: #fff;
}
.card-form .el-form-item__label {
  color: #fff;
}

.card-form .el-input__prefix,
.card-form .el-input__suffix {
  top: 17px;
}

.card-form .el-select {
  display: block;
}
</style>
