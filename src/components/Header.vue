<template>
    <div class='Header'>
    <p> Quiz Category: <b>{{ category }}</b> </p>
       <!--{{ infoForHeader }} -->
    <p> Total Questions in Quiz: <b>{{ totalQsinQuiz }}</b> </p>
    <p> Counter: <b>{{ numCorrect }} / {{ numTotal }}</b> </p>
    </div>
</template>

<script>
export default {
  name: 'Header',
  props:[
    //'infoForHeader',
    'totalQsinQuiz',
    'numCorrect',
    'numTotal',
    'category'
  ]
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>