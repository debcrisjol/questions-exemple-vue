<template>
  <div id="app">
   <HeaderBox
   :numCorrect="numCorrect"
   :numTotal="numTotal" />

   <div class="container text-center">
  <div class="row">
    <div class="col-sm-6 offset-3 w-75 m-5">
      <QuestionBox 
      v-if= "questions.length"
      :currentQuestion= "questions[index]"
      :next= "next"
       :increment="increment" />
    </div>
  </div>
</div>

   
  </div>
</template>

<script>
import HeaderBox from './components/HeaderBox.vue'
import QuestionBox from './components/QuestionBox.vue'

export default {
  name: 'app',
  components: {
    HeaderBox,
    QuestionBox,
  },
  data(){return{
   questions:[],
   index:0,
   numCorrect :0,
   numTotal:0
  }},
 methods:{
  next(){
    this.index++
  },
  increment(isCorrect){
    if (isCorrect){
   this.numCorrect++
    }
    this.numTotal++
  }
 },
  mounted: function(){
    fetch('https://opentdb.com/api.php?amount=10&category=27&type=multiple',{
      method:'get'})
     .then((response) => {
       return response.json()})
       .then((jsonData) =>{
        this.questions=jsonData.results
       })
     }
    }
  
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
