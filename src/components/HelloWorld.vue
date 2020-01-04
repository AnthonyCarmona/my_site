<template>
  <v-content>
        <v-container>
          <v-row>
            <v-col>
          <v-form>
          <input v-model="interest" placeholder="interest rate">
          <input v-model="monthly" placeholder="monthly payment">
          <input v-model="age" placeholder="Current age">
          <input v-model="retAge" placeholder="Retirement age">
          <input v-model="income" placeholder="Desired Income">
          <input v-model="lifeExpectancy" placeholder="Life expectancy">
          </v-form>
          </v-col>
           <v-col>
            <div>
                <p>monthly interest: {{monthlyInterest}}</p>
                <p>years till retirment: {{yearsTill}}</p>
                <p>present value at retirement: {{presentValueAtRet}}</p>
                <p>aAngleN: {{aAngleN}}</p>
                <p>sAngleN: {{sAngleN}}</p>
                <p>yearly payments: {{yearlyPayment}}</p>
            </div>
            </v-col>
            </v-row>

          
            
       
        </v-container>
      </v-content>
</template>

<script>
export default {
  
      
    data() {
        return {
            interest: '', age: '', retAge: '', income: '', monthlySavings: '', lifeExpectancy: ''
        }
     },
    computed: {
      monthlyInterest: function(){
        return ( ((1+this.interest/100) ** (1/12) -1) * 100 )
        },
          yearsTill: function() {
              return (this.retAge - this.age)
          },
          aAngleN: function() {
              let i = this.interest/100;
              let v = 1/(1 + i);
              let yearsOfRetirement = this.lifeExpectancy - this.retAge;
              return ( (1 - v ** yearsOfRetirement) / i )
          },
          presentValueAtRet: function() {
             
              return ( this.income * this.aAngleN )
          },
          sAngleN: function() {
              let i = this.interest / 100
              let accu = (1 + i);
              return ( (accu ** this.yearsTill - 1) / i );
          }, 
          yearlyPayment: function() {
            return (this.presentValueAtRet / this.sAngleN) 
          }, 
          
          }
}
</script>
