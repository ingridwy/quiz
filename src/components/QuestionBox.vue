<template>
    <div class="question-box">
    <b-jumbotron>
        <template v-slot:header>Question</template>

        <template v-slot:lead>
        {{ theQuestion.question }}
        </template>

        <hr class="my-4">
            <b-list-group >
                <b-list-group-item v-for="(answer,index) in answers" :key="index" @click="select(index)"
                :class="[selectIndex === index?  'selected' : '']">
                    {{ answer }} 
                </b-list-group-item>
            </b-list-group>
 
        <b-button variant="primary" @click="submitAnswer" :disabled="selectIndex === null || answered">Submit</b-button>
        <b-button @click="next" variant="success" >Next Q</b-button> 
    </b-jumbotron>
    </div>

</template>
<script>
    import _ from 'lodash'
    export default { 
        props: {
            theQuestion: Object,
            next: Function,
            increment: Function
        },
        data() {
            return{
                selectIndex: null,
                shuffledAnswer: [],
                answered: false
                } 
        },  
        computed:{
            answers(){
                let answers=[...this.theQuestion.incorrect_answers]
                answers.push(this.theQuestion.correct_answer) 
                return answers
            }
        },
        watch:{
            theQuestion:{
                immediate: true,
                handler() {
                    this.selectIndex = null
                    this.answered = false
                    this.shuffleAnswer()
                } 
            }
        },
        methods:{
            select(index) {
                this.selectIndex = index
                //console.log(index)
            },
            shuffleAnswer(){
                let answers = [...this.theQuestion.incorrect_answers , this.theQuestion.correct_answer]
                this.shuffledAnswer = _.shuffle(answers)
            },
            submitAnswer(){
                let isCorrect = false
                if (this.selectIndex === this.correctIndex){
                    isCorrect = true
                }
                this.answered = true
                this.increment(isCorrect)
            }

        }
      
    }
    
</script>
<style scoped>
.list-group{
    margin: 10px;
}
.list-group-item{
    margin: 10px;
}
.list-group-item:hover{
    background-color: #E5E5E5;
}
.btn{
    margin: 5px;
}
.selected{
    background-color: #FFB6C1;
}
.right{
    background-color: green;
}
.wrong{
    background-color:red;
}


</style>