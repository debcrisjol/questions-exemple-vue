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
      @click="selectAnswer(index)"> {{ answer}}
    </button>
    </div>

<div class="m-4">
    <button type="button" class="btn btn-danger">Submit</button>
    <button @click="next" type="button" class="btn btn-success">Next</button>
</div>


</div>
</template>


<script>
export default{
    props:{
        currentQuestion: Object,
        next: Function
    },
    data(){
        return{
            selectedIndex:null
        }
    },
    computed:{
        answers() {
       let answers =[...this.currentQuestion.incorrect_answers]
         answers.push(this.currentQuestion.correct_answer);
         return answers
    }},
    methods : {
        selectedAnswer(index){
       this.selectedIndex=index
        }
    }
}
</script>

<style scoped >
.list-group-item:hover {
    background-color: greenyellow;
    cursor:pointer;
}
button{ margin:0 5px;}

</style>