<template>
  <div class="main">
    <form-input
      :form-input="formInput"
      :comment="formInput.comment"
      :value="formInput.value"
      :typeOfIncome="formInput.typeOfIncome"
      @addNewType="addNewType"
    />
    <div v-if="totalValueAll > 0" class="totalBalance positive">
      Your estimated budget is {{ totalValueAll }} EUR
    </div>
    <div v-else class="totalBalance negative">
      You have a deficit of {{ totalValueAll }} EUR in the budget. Adjust your
      expenses.
    </div>
    <budget-list :budget-list="budgetList" @deleteItems="deleteItems" />
  </div>
</template>

<script>
import FormInput from "@/components/FormInput.vue";
import BudgetList from "@/components/BudgetList.vue";

export default {
  name: "App",
  components: { BudgetList, FormInput },
  data: () => ({
    formInput: {
      typeOfIncome: "Income",
      comment: "",
      value: Number,
    },
    budgetList: [{ typeOfIncome: "Income", comment: "asd", value: 12 }],
    totalValue: 0,
  }),

  methods: {
    addNewType(newArray) {
      this.budgetList.push(newArray);
      this.formInput.typeOfIncome = "Income";
      this.formInput.comment = "";
      this.formInput.value = Number;
    },
    deleteItems(index) {
      this.budgetList.splice(index, 1);
    },
  },

  computed: {
    totalValueAll() {
      return this.budgetList.reduce((acc, item) => item.value + acc, 0);
    },
  },
};
</script>

<style>
.main {
  display: flex;
  align-items: center;
  flex-direction: column;
  width: 800px;
  margin: auto;
  padding: 15px;
  justify-content: center;
}

.totalBalance {
  display: inline-block;
  margin-top: 20px;
  margin-bottom: 20px;
  font-family: "Times New Roman", Times, serif;
  font-size: 24px;
}
.totalBalance.positive {
  color: darkgreen;
}

.totalBalance.negative {
  color: darkred;
}
</style>
