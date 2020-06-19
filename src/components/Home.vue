<template>
  <div class="contianer">
    <div class="row">
      <div class="col-md-2"></div>
      <div class="col-md-8">
        <div class="card shadow p-3 mb-5 bg-white rounded" style="margin-top:40px; ">
          <div class="card-body">
            <h5 class="card-title">irecharge</h5>

            <form @submit.prevent="onRecharge">
              <div class="form-group">
                <label for="phone">Phone Number</label>
                <input
                  type="text"
                  placeholder="07058399439"
                  v-model="PhoneNumber"
                  class="form-control"
                  name="phoneNumber"
                  id="phone"
                />
              </div>
              <div class="form-group">
                <label for="amount">Amount</label>
                <input
                  type="text"
                  placeholder="1000"
                  v-model="Amount"
                  class="form-control"
                  name="Amount"
                  id="amount"
                />
              </div>

              <!-- <div class="form-group">
                <label for="code">Code</label>
                <input
                  type="text"
                  placeholder="+234"
                  class="form-control"
                  name="code"
                  v-model="code"
                  id="code"
                />
              </div>-->

              <label for="code">Network</label>
              <select name="Code" v-model="Code" class="custom-select custom-select-lg mb-3">
                <option v-for="network in items" :key="network.id">{{network.name}}</option>
              </select>

              <div class="form-group form-check">
                <input type="checkbox" class="form-check-input" id="exampleCheck1" />
                <label class="form-check-label" for="exampleCheck1">Check me out</label>
              </div>

              <button type="submit" class="btn btn-primary">Submit</button>
            </form>
          </div>
        </div>
      </div>
      <div class="col-md-2"></div>
    </div>
  </div>
</template>

<script>
const axios = require("axios").default;

//axios.defaults.headers.common["Authorization"] = AUTH_TOKEN;
//axios.defaults.headers.post["Content-Type"] = "Content-Type: application/json";
export default {
  data() {
    return {
      PhoneNumber: "",
      Amount: "",
      Code: "",
      SecretKey: "hfucj5jatq8h",
      publicKey: "uvjqzm5xl6bw",

      items: [
        {
          name: "Mtn",
          id: 1
        },
        {
          name: "Glo",
          id: 2
        },
        {
          name: "Airtel",
          id: 3
        },
        {
          name: "9Mobile",
          id: 4
        }
      ]
    };
  },

  methods: {
    onRecharge() {
      var optionAxios = {
        headers: {
          "Content-Type": "application/json",
          " Access-Control-Allow-Origin": "http://localhost:8080/"
        }
      };

      const url = "https://sandbox.wallets.africa/bills/airtime/purchase";

      axios
        .post(
          url,
          {
            PhoneNumber: this.PhoneNumber,
            Code: this.Code,
            Amount: this.Amount,
            SecretKey: this.SecretKey
          },
          optionAxios
        )
        .then(function(response) {
          console.log(response);
        })
        .catch(function(error) {
          console.log(error);
        });
      // axios.post(
      //   url,
      //   {
      //     PhoneNumber: this.PhoneNumber,
      //     Code: this.Code,
      //     Amount: this.Amount,
      //     SecretKey: this.SecretKey
      //   }
      // );
    }
  }
};
</script>