<template>
  <div id="app">
    <Header
    :numCorrect = "numCorrect"
    :numTotal = "numTotal "
    />
<b-container class="bv-example-row">
  <b-row>
    <b-col sm="8" offset="2"> 
      <QuestionBox 
      v-if="questions.length"
      :theQuestion = "questions[index]" 
      :next = "next"
      :increment = "increment "
      /> 
    </b-col>
  
  </b-row>
</b-container>
   
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'

export default {
  name: 'App',
  components: {
    Header, 
    QuestionBox
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrect : 0,
      numTotal: 0
    }
  },
  methods:{
    next: function () {
      if(this.numTotal<10){
        this.index++
      } else{
        location.reload();
      }
      
    },
    increment(isCorrect ){
      if (isCorrect){
        this.numCorrect ++
      }
      this.numTotal ++

    }
  },

  mounted: function () {
    fetch ('https://opentdb.com/api.php?amount=10&category=14&type=multiple',{
      method: 'get'
    })
      .then((response)=>{
        return response.json()
      })
      .then((jsonData)=>{
        this.questions = jsonData.results
      })

  }
}
</script>

<style>
#app {
  font-family: 'Mulish', Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 60px;
}
body {
  min-height: 100vh;
  background-image: url('https://images.unsplash.com/photo-1543157145-f78c636d023d?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1050&q=80');
  background-size: cover;
  background-position: bottom;
}
</style>
