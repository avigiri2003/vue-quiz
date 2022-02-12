<template>
  <div id="app">
    <Header 
      v-if="QList.length"
      :infoForHeader="headerInfo"
      :totalQsinQuiz="QList.length"
      :numCorrect="numCorrect"
      :numTotal="numTotal"
      :category="QList[index].category"
    />
    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3"> 
          <QuestionBox 
            v-if="QList.length"
            :currentQuestion="QList[index]"
            :nextQ="nextQ"
            :Qnum="index+1"
            :incrementCounter="incrementCounter"
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
  name: 'app',
  components: {
    Header,
    QuestionBox
  },
  data(){
    return{
      QList:[],
      index: 0,
      headerInfo: "testInfo",
      numCorrect: 0,
      numTotal: 0,
    }
  },
  methods:{
    nextQ(){
      this.index++
    },
    incrementCounter(isAnswerCorrect){
      if(isAnswerCorrect === 1){
        this.numCorrect++;
      }
      this.numTotal++;
    }
  },
  mounted: function(){
    fetch('https://opentdb.com/api.php?amount=10&category=18&type=multiple', {
      method: 'get'
    })
    .then((response) => {
      return(response.json());
    })
    .then((jsonData) => {
      this.QList = jsonData.results;
    })

  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
