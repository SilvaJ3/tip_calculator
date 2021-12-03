<template>
  <div class="rounded-2xl shadow-lg bg-white flex justify-center items-center w-3/4 p-4">
    <!-- LEFT PART -->
    <div class="flex flex-col p-4 w-1/2 h-80" id="leftCalculator">
      <!-- Bill -->
      <h1 class="font-bold">Bill</h1>
      <div class="bill mt-3">
        <input type="number" step="0.01" placeholder="0" v-model="bill" class="text-right rounded-md p-1 w-full">
      </div>
      <!-- Select Tip -->
      <h1 class="font-bold my-3">Select Tip %</h1>
      <div class="grid grid-cols-3 gap-4 mb-3">
        <div v-for="(item, index) in tipPercentage" :key="index" class="tipBtn py-1 flex justify-center rounded-md cursor-pointer" @click="tips(item)" :class="item === tip ? 'active' : ''">
          <span class="text-white font-bold pointer-events-none">{{item}}%</span>
        </div>
        <div>
          <input type="number" class="font-bold customBtn py-1 text-center rounded-md" @keypress.enter="(event) => tips(event.target.value)" placeholder="Custom">
        </div>
      </div>
      <!-- Number of People -->
      <h1 class="font-bold">Number of People</h1>
      <div class="people mt-3">
        <input type="number" placeholder="0" v-model="people" class="text-right rounded-md p-1 w-full">
      </div>
    </div>

    <!-- RIGHT PART -->
    <div class="flex flex-col justify-between p-6 w-1/2 h-80 rounded-md" id="rightCalculator">
      <div>
        <div class="flex justify-between mt-5">
          <div>
            <p class="text-white tipTitle mb-0">Tip Amount</p>
            <span class="perPerson">/ person</span>
          </div>
          <h1 class="amount font-bold text-3xl">${{tipSplit}}</h1>
        </div>
        <div class="flex justify-between mt-8">
          <div>
            <p class="text-white tipTitle mb-0">Total Amount</p>
            <span class="perPerson">/ person</span>
          </div>
          <h1 class="amount font-bold text-3xl">${{total}}</h1>
        </div>
      </div>

      <div class="reset w-full rounded-md py-1 cursor-pointer" @click="reset">
        <p class="text-center pointer-events-none">RESET</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tipPercentage: [5, 10, 15, 25, 50],
      bill: null,
      people: null,
      tip: null,
      tipAmountPerPerson: 0.00,
      totalAmount: 0.00
    }
  },
  methods: {
    tips(value) {
      this.tip = value;
    },
    totalCalculator() {
      if (this.tip && this.bill && this.people) {
      this.totalAmount = ((parseInt(this.bill) + parseInt((this.bill/100) * this.tip)) / parseInt(this.people)).toFixed(2);
      } else if (this.bill) {
        this.totalAmount = this.bill;
      }
    },
    tipPerPerson() {
      if (this.tip && this.bill && this.people) {
        this.tipAmountPerPerson = (parseInt((this.bill/100) * this.tip) / parseInt(this.people)).toFixed(2);
      }
    },
    reset(){
      this.bill = null;
      this.people = null;
      this.tip = null;
      this.tipAmountPerPerson = 0.00;
      this.totalAmount = 0.00;
    }
  },
  computed: {
    total: function() {
      this.totalCalculator();
      return this.totalAmount
    },
    tipSplit: function () {
      this.tipPerPerson();
      return this.tipAmountPerPerson
    }
  }
}
</script>

<style>
#leftCalculator .bill input{
  background-color: hsl(189, 41%, 97%);
  background-image: url("../assets/icon-dollar.svg");
  background-repeat: no-repeat;
  background-position-x: 5%;
  background-position-y: 50%;
  color: hsl(183, 100%, 15%)
}

#leftCalculator .people input{
  background-color: hsl(189, 41%, 97%);
  background-image: url("../assets/icon-person.svg");
  background-repeat: no-repeat;
  background-position-x: 5%;
  background-position-y: 50%;
  color: hsl(183, 100%, 15%)
}

.tipBtn, .customBtn {
  width: 80px;
}

.tipBtn {
  background-color: hsl(183, 100%, 15%)
}

.tipBtn.active {
  background-color:  hsl(172, 67%, 45%);
}

.tipBtn.active span {
  color: hsl(183, 100%, 15%);  
}

.customBtn {
  color: hsl(183, 100%, 15%)
}

#rightCalculator {
  background-color: hsl(183, 100%, 15%);
}

.tipTitle {
  font-size: 12px
}

.perPerson {
  color: hsl(189, 41%, 97%);
  font-size: 10px;
}

.amount {
  color: hsl(172, 67%, 45%)
}

.reset {
  background-color:  hsl(172, 67%, 45%);
}
</style>