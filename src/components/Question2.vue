<template>
    <b-card>
        <b-form>
            <h6>Question 2</h6>
            <br>
            <b-row>
                <b-col md="auto">
                    <b-form-group>
                    <label>Amount</label>
                    <b-form-input v-model="amount" />
                </b-form-group> 
                </b-col>
                <b-col md="auto">
                    <b-form-group>
                    From
                    <br>
                    <b-form-select 
                    class="form-control"
                    v-model="from"
                    :options="select.currency"
                    required />
                </b-form-group> 
                </b-col>
                <b-col md="auto" id="styleicon">
                    <b-icon icon="arrow-left-right"/>
                </b-col>
                <b-col md="auto">
                    <b-form-group>
                    To
                    <br>
                    <b-form-select 
                    class="form-control"
                    v-model="to"
                    :options="select.currency"
                    required />
                </b-form-group> 
                </b-col>
                <b-col md="auto" id="styleicon">
                   <b-button  variant="warning" size="sm" @click="calculate()">
                       <b-icon icon="chevron-compact-right"/>
                   </b-button> 
                </b-col>
                   
            </b-row>
            <b-row class="text-center">
                <p  v-if="result!=''">{{amount}} {{select.currency.filter(item => item.value==from)[0].text}} = </p>
            </b-row>
            <b-row class="justify-content-md-center">
                <b-col md="auto">
                    <h2  v-if="result!=''">{{result}}</h2>
                </b-col>
                <b-col md="auto" align-self="end">
                    <p v-if="result!=''">{{select.currency.filter(item => item.value==to)[0].text}}</p>
                </b-col>
                
            </b-row>
            <b-row class="justify-content-md-center">
                <b-col md="auto">
                    <p  v-if="result!=''">1 {{from}} = {{current_currency}} {{to}}</p>
                </b-col>
                
            </b-row>
            <b-row class="justify-content-md-center">
                <b-col md="auto">
                    <p  v-if="result!=''">1 {{to}} = {{currencyToFrom}} {{from}}</p>
                </b-col>
                
            </b-row>
        </b-form>
    </b-card>

</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
        url:'https://free.currconv.com/api/v7/convert?apiKey=a8b229ce88704b5d13f1&q=',
        current_currency:'',
        currencycode:'',
        changecurrencycode:'',
        currency: '',
        currencyToFrom: '',
        amount: '',
        from: '',
        to: '',
        result: '',
        select: {
            currency: [
                { value: '', text: 'Please Select'},
                { value: 'EUR', text: 'EUR'},
                { value: 'MYR', text: 'MYR'},
                { value: 'USD', text: 'USD'}
            ]
        }
    }
  },

  created() {
    //   this.calculate()
  },

  methods: {
      getCurrency(currencycode){
          return axios.get(this.url+currencycode);
      },
      calculate(){
          this.currencycode = this.from+'_'+this.to
          this.changecurrencycode = this.to+'_'+this.from
          console.log(this.currencycode)
          this.getCurrency(this.currencycode).then( respond => {

            this.currency = Object.keys(respond.data.results).map((key) => {
                return respond.data.results[key]
            })
            this.current_currency = this.currency[0].val
            this.result = (this.current_currency * this.amount).toFixed(6)

            this.getCurrencyFromTo(this.changecurrencycode)
          })
      },
     getCurrencyFromTo(currencyCode)
     {  
         this.getCurrency(currencyCode).then( respond => {

            let dataCurrency = Object.keys(respond.data.results).map((key) => {
                return respond.data.results[key]
            })
            let currency = dataCurrency[0].val

            this.currencyToFrom = currency
          })
     }
  }
}
</script>

<style>
#styleicon {
  padding-top: 30px;
}


</style>