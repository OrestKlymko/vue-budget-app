<template>
  <div class="budgetList">
    <h2>Budget list</h2>
    <ul v-for="(list, index) in budgetList" :key="index">
      <li class="budgetList-list">
        <div class="typeIncome">{{ list.comment }}</div>
        <div class="valueIncome">: {{ list.value }} EUR</div>
        <button @click="deleteItems(index)" class="btn-delete">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "BudgetList",
  props: {
    budgetList: {
      type: Object,
    },
  },
  methods: {
    deleteItems(index) {
      this.$emit("deleteItems", index);
    },
  },
};
</script>

<style scoped>
.budgetList {
  border: 2px solid darkgrey;
  display: flex;
  flex-direction: column;
  width: 300px;
  padding: 15px 25px;
  box-shadow: 6px 4px 8px 0px rgba(34, 60, 80, 0.2);
  display: flex;
}
li {
  list-style-type: none;
}

h2 {
  text-align: center;
}

.budgetList-list {
  display: flex;
  flex-direction: row;
}

.valueIncome {
  margin-right: 10px;
  font-style: italic;
}

.typeIncome {
  font-weight: bolder;
}

.btn-delete {
  margin-left: auto;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 5em;
  height: 1.5em;
  line-height: 1.67;
  vertical-align: middle;
  text-align: center;
  text-decoration: none;
  text-shadow: 0 -1px 1px #777;
  color: #fff;
  outline: none;
  border: 2px solid #880000;
  border-radius: 5px;
  box-shadow: 0 0 0 60px rgba(0, 0, 0, 0) inset, 0.1em 0.1em 0.2em #800;
  background-color: #880000;
}
btn-delete:active {
  top: 0.1em;
  left: 0.1em;
  box-shadow: 0 0 0 60px rgba(0, 0, 0, 0.05) inset;
}
</style>
