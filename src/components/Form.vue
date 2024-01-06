<template lang="">
  <div class="container">
    <form @submit.prevent="handleSubmit">
      <div class="card">
        <h3>CurrencyConvert To THB</h3>
        <h4>Enter Amount</h4>
        <input type="number" required v-model="bath" />
        <h4>To</h4>
        <select v-model="currency">
          <option value="" selected>Select currency</option>
          <option v-for="item in items">
            {{ item.code }}
          </option>
        </select>
        <button type="submit" class="button button1">Button</button>
        <h5>Result</h5>
        <p>{{bath}} THB = {{valuesconvert}} {{currency}}</p>
      </div>
    </form>
  </div>
</template>
<script>
export default {
  data() {
    return {
      items: [],
      bath: "",
      currency: "",
      valuesconvert: ""
    };
  },
  created() {
    fetch("https://www.floatrates.com/daily/thb.json")
      .then((res) => res.json())
      .then((result) => {
        this.items = result;
      });
  },
  methods: {
    handleSubmit() {
      fetch("https://www.floatrates.com/daily/thb.json")
        .then((res) => res.json())
        .then((result) => {
            Object.values(result).forEach(e => {
                if(this.currency === e.code){
                    this.valuesconvert = this.bath / e.inverseRate
                }
            });
        });
    },
  },
};
</script>
<style scoped>
.card {
  padding: 16px;
  border: 1px solid #000;
}
.container {
  padding: 2px 16px;
  display: block;
  margin: 0 auto;
  margin-top: 20px;
}
h3 {
  text-align: center;
  font-weight: 700;
  font-size: 28px;
}
input {
  width: 100%;
  height: 30px;
}
form {
  background: #ffffff;
  width: 100%;
  height: 500px;
  max-width: 450px;
  margin: 0 auto 100px;
  box-sizing: border-box;
  padding: 50px;
  text-align: center;
}
h4 {
  text-align: left;
  margin-top: 10px;
}
select {
  width: 100%;
  height: 30px;
}
.button {
  background-color: #04aa6d; /* Green */
  border: none;
  color: white;
  padding: 10px 10px;
  text-align: center;
  text-decoration: none;
  font-size: 16px;
  margin-top: 15px;
  cursor: pointer;
  transition: 0.5s;
  width: 100%;
}
.button:hover {
  background-color: #08bb79;
}
h5 {
  font-size: 20px;
  text-align: left;
}
p {
  text-align: left;
}
</style>
