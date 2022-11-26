<template>
    <div class="question-box-container bg-warning p-4">
    
 
    <h4>
    {{ currentQuestion.question }}
    </h4>

    <hr class="my-4">


    <div class="list-group">
    <button type="button" class="list-group-item list-group-item-action"
     v-for="(answer, index ) in answers"
      :key="index"
      @click="selectedAnswer(index)"
      :class="[selectedIndex === index ? 'selected': '']"> {{ answer}}
    </button>
    </div>

<div class="m-4">
    <button type="button" class="btn btn-danger"
    @click="submitAnswer"
    :disabled="selectedIndex === null || answered"
    >
        Submit</button>
    <button @click="next" type="button" class="btn btn-success">Next</button>
</div>


</div>
</template>


<script>
import _ from 'lodash'
export default{
    props:{
        currentQuestion: Object,
        next: Function,
        increment: Function
    },
    data(){
        return{
            selectedIndex: null,
            shuffledAnswers: [],
            correctIndex: null,
            answered: false
        }
    },
    computed:{
        answers() {
       let answers =[...this.currentQuestion.incorrect_answers]
         answers.push(this.currentQuestion.correct_answer);
         return answers
    }},
    watch: {
        currentQuestion: {
            immediate: true,
            handler(){
                this.selectedIndex = null
                this.shuffleAnswers()
                this.answered = false
            }
        }
    },
    methods : {
        selectedAnswer (index) {
       this.selectedIndex = index
        },
        shuffleAnswers(){
            let answers = [...this.currentQuestion.incorrect_answers,this.currentQuestion.correct_answer]
           this.shuffledAnswers = _.shuffle(answers)
        },
        submitAnswer(){
            let isCorrect = false
            if(this.selectedIndex === this.correctIndex){
                isCorrect = true
            }
            this.answered= true
            this.increment(isCorrect)
        }
    }
}
</script>

<style scoped >
.list-group-item:hover {
    background-color: rgba(190, 190, 190, 0.682);
    cursor:pointer;
}
button{ margin:0 5px;}
.selected{ background-color: rgb(80, 184, 207);}
.correct{background-color: green;}
.incorrect {background-color:red;}

</style>