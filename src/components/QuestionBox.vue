<template>
  <div class="QuestionBox">
    <b-jumbotron>
    <!--<template v-slot:header>-->
    <template>
      <b> Question# {{ Qnum }}</b>
      <br>
      <p v-html="currentQuestion.question"/>
    </template>
    
    <hr class="my-4">
    
    <p>
      <!--<ul v-for="(mydata, index) in currentQuestion.incorrect_answers" :key='index'>
        <li>{{mydata}}</li>
      </ul>
      {{currentQuestion.correct_answer}}
      -->

      <!--<ul v-for="(mydata, index) in answerArray" :key='index'>
        <li>{{answerArray[index]}}</li>
      </ul>
      -->

    <b-list-group>
      <b-list-group-item v-for="(mydata, index) in answerArray" :key='index' 
        @click="selectAnswer(index)"
        :class="[
        !answered && selectedIndex===index ? 'selected' :
        answered && correctIndex===index && isAnswerCorrect === 1 ? 'correct' : 
        answered && selectedIndex===index && correctIndex !== index ? 'incorrect' : ''
        ]">
        {{answerArray[index]}}
      </b-list-group-item>
    </b-list-group>

    </p>

    <b-button @click="submitAnswer" variant="primary" 
      :disabled="selectedIndex === -1 || isAnswerCorrect > -1">
      Submit
    </b-button>
    <b-button @click="nextQ" variant="success"
      :disabled="disableNextBtn || Qnum === 10">
      Next
    </b-button>
    {{ selectedIndex }}
  </b-jumbotron>
  </div>
</template>

<script>

export default {
  name: 'QuestionBox',
  props:{
    currentQuestion: Object,
    nextQ: Function,
    Qnum: Number,
    incrementCounter: Function
  },
  data(){
    return {
      selectedIndex: -1,
      correctIndex: -1,
      answered: false,
      isAnswerCorrect: -1,
      disableNextBtn: true
    }
  },
  watch:{
    currentQuestion: {
      immediate: true,
      handler(){
        this.selectedIndex = -1;
        this.correctIndex = -1;
        this.answered = false;
        this.isAnswerCorrect = -1;
        this.disableNextBtn = true;
      }
    }
    /*currentQuestion(){
      this.selectedIndex = -1
      this.isAnswerCorrect = -1
    }*/
  },
  methods:{
    selectAnswer(index){
      this.selectedIndex = index;
    },
    submitAnswer(){
      this.answered = true;
      this.disableNextBtn = false;
      if(this.currentQuestion.correct_answer === this.answerArray[this.selectedIndex]){
        this.isAnswerCorrect = 1;
        this.correctIndex = this.selectedIndex;
      }
      else{
        this.isAnswerCorrect = 0;
        this.correctIndex = -1;
      }

      this.incrementCounter(this.isAnswerCorrect);
    }
  },
  computed:{
    answerArray(){
      let answerArray = [...this.currentQuestion.incorrect_answers]
      answerArray.push(this.currentQuestion.correct_answer)
      let temp_index = Math.floor(Math.random() * Math.floor(4));
      let temp_val = answerArray[temp_index]
      answerArray[temp_index] = answerArray[3]
      answerArray[3] = temp_val
      return answerArray
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type:none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.list-group{
  margin-bottom: 15px;
}
.list-group-item:hover{
  background-color: lightgray;
}
.btn{
  margin: 0 10px;
}
.selected{
  background-color: lightblue;
}
.correct{
  background-color: lightgreen;
}
.incorrect{
  background-color:orangered;
}
</style>
