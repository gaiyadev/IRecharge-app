<template>
  <div class="contianer">
    <div class="row">
      <div class="col-md-2"></div>
      <div class="col-md-8">
        <div class="card shadow p-3 mb-5 bg-white rounded" style="margin-top:40px; ">
          <div class="card-body">
            <h5 class="card-title text-uppercase text-center text-primary">iRecharge</h5>
            <div v-show="show" class="alert alert-success alert-dismissible fade show" role="alert">
              <strong>Yeah!</strong> Airtime purchased successfully
              <button
                type="button"
                class="close"
                data-dismiss="alert"
                aria-label="Close"
              >
                <span aria-hidden="true">&times;</span>
              </button>
            </div>

            <div
              v-show="error"
              class="alert alert-danger alert-dismissible fade show"
              style="margin-top: 20px;"
              role="alert"
            >
              <strong>Sorry!</strong> Please fill all fields
              <button
                type="button"
                class="close"
                data-dismiss="alert"
                aria-label="Close"
              >
                <span aria-hidden="true">&times;</span>
              </button>
            </div>

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

              <button id="buy" type="submit" class="btn btn-primary">Submit</button>
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
axios.defaults.crossDomain = true;

//axios.defaults.headers.common["Authorization"] = AUTH_TOKEN;
//axios.defaults.headers.post["Content-Type"] = "Content-Type: application/json";
export default {
  data() {
    return {
      show: false,
      error: false,
      PhoneNumber: "",
      Amount: "",
      Code: "",
      SecretKey: "hfucj5jatq8h",

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
      if (this.PhoneNumber === "" || this.Code === "" || this.Amount === "") {
        return (this.error = true);
      } else {
        const url = "https://sandbox.wallets.africa/bills/airtime/purchase";
        const proxyurl = "https://cors-anywhere.herokuapp.com/";
        const publicKey = "uvjqzm5xl6bw";

        axios
          .post(
            proxyurl + url,
            {
              PhoneNumber: this.PhoneNumber,
              Code: this.Code,
              Amount: this.Amount,
              SecretKey: this.SecretKey
            },
            {
              headers: {
                "Content-Type": "application/json",
                Authorization: `Bearer ${publicKey}`
              }
            }
          )
          .then(() => {
            this.show = true;
            console.log("Airtime purchased successfully");
          })
          .catch(err => console.log(err));
      }
    }
  }
};

// var optionAxios = {
//   headers: {
//     "Content-Type": "application/json",
//     "Access-Control-Allow-Origin": "http://localhost:8080/",
//     // "Access-Control-Allow-Headers":
//     //   "Origin, X-Requested-With, Content-Type, Accept",
//     "Access-Control-Allow-Methods": "POST",
//     "Access-Control-Allow-Credentials": true,
//     Authorization: "Bearer uvjqzm5xl6bw",
//     credentials: "same-origin",
//     "Access-Control-Allow-Headers": "Authorization"
//   }
// };
</script>

<style scoped>
</style>