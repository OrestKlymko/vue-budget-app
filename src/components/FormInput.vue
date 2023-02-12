<template>
  <h1>Budget calculator</h1>
  <form @submit.prevent class="form">
    <div class="group">
      <select v-model="$props.formInput.typeOfIncome">
        <option>Income</option>
        <option>Outcome</option>
      </select>
    </div>
    <div class="group">
      <input
        type="text"
        placeholder="My salary"
        v-model="$props.formInput.comment"
      />
      <span class="bar"></span>
      <label class="form-input">Comments</label>
    </div>
    <div class="group">
      <input type="number" placeholder="0" v-model="$props.formInput.value" />
      <span class="bar"></span>
      <label class="form-input">Value</label>
    </div>
    <button class="border-button" type="submit" @click="addNewType">
      Add payment
    </button>
  </form>
</template>

<script>
export default {
  name: "FormInput",
  props: {
    formInput: {
      typeOfIncome: String,
      comment: String,
      value: Number,
    },
  },
  data: () => ({}),
  methods: {
    addNewType() {
      let newArray = {
        typeOfIncome: this.formInput.typeOfIncome,
        comment: this.formInput.comment,
        value: this.formInput.value,
      };
      if (newArray.typeOfIncome == "Outcome") {
        newArray.value = -newArray.value;
      }
      this.$emit("addNewType", newArray);
    },
  },
};
</script>

<style scoped>
.form {
  border: 2px solid darkgrey;
  display: flex;
  flex-direction: column;
  width: 300px;
  padding: 15px 25px;
  box-shadow: 6px 4px 8px 0px rgba(34, 60, 80, 0.2);
}

.form-input {
  padding-top: 10px;
  padding-bottom: 10px;
}
.border-button {
  text-decoration: none;

  display: inline-block;
  position: relative;
  padding: 15px 30px;
  border: 1px solid;
  border-image: linear-gradient(180deg, #ff3000, #ed0200, #ff096c, #d50082);
  border-image-slice: 1;
  margin: 10px 20px;
  font-family: "Montserrat", sans-serif;
  text-transform: uppercase;
  overflow: hidden;
  letter-spacing: 2px;
  transition: 0.8s cubic-bezier(0.165, 0.84, 0.44, 1);
  cursor: pointer;
}
.border-button:before {
  content: "";
  position: absolute;
  left: 0;
  top: 0;
  height: 0;
  width: 100%;
  z-index: -1;
  color: white;
  background: linear-gradient(180deg, #ff3000, #ed0200, #ff096c, #d50082);
  transition: 0.8s cubic-bezier(0.165, 0.84, 0.44, 1);
}
.border-button:hover {
  background: rgba(255, 255, 255, 0);
}
.border-button:hover:before {
  bottom: 0%;
  top: auto;
  height: 100%;
}

select {
  width: 100%;
  padding: 5px 5px;
  border: none;
}

.group {
  position: relative;
  margin-bottom: 30px;
}

input {
  font-size: 16px;
  padding: 15px;
  display: block;
  width: 250px;
  border: none;
  border-bottom: 1px solid #ccc;
}
input:focus {
  outline: none;
}
/* LABEL ======================================= */
label {
  color: #999;
  font-size: 18px;
  position: absolute;
  pointer-events: none;
  left: 10px;
  top: -10px;
  transition: 0.2s ease all;
  -moz-transition: 0.2s ease all;
  -webkit-transition: 0.2s ease all;
}

/* active state */
input:focus ~ label,
input:valid ~ label {
  top: -20px;
  font-size: 14px;
  color: #5264ae;
}

/* BOTTOM BARS ================================= */
.bar {
  position: relative;
  display: block;
  width: 320px;
}
.bar:before,
.bar:after {
  content: "";
  height: 2px;
  width: 0;
  bottom: 0;
  position: absolute;
  background: #5264ae;
  transition: 0.2s ease all;
  -moz-transition: 0.2s ease all;
  -webkit-transition: 0.2s ease all;
}
.bar:before {
  left: 50%;
}
.bar:after {
  right: 50%;
}

/* active state */
input:focus ~ .bar:before,
input:focus ~ .bar:after {
  width: 50%;
}
</style>
