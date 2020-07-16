<template>
    <div class="question-box">
    <b-jumbotron>
        <template v-slot:header>Film Quiz</template>

        <template v-slot:lead>
        {{ theQuestion.question }}
        </template>

        <hr class="my-4">
            <b-list-group >
                <b-list-group-item v-for="(answer,index) in answers" :key="index" @click="select(index)"
                :class="answerClass(index)">
                    {{ answer }} 
                </b-list-group-item>
            </b-list-group>
 
        <b-button variant="primary" @click="submitAnswer" :disabled="selectIndex === null || answered">Submit</b-button>
        <b-button @click="next" :disabled="selectIndex === null || !answered" variant="success" >Next Question</b-button> 
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
                correctIndex: null,
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
                this.correctIndex = this.shuffledAnswer.indexOf(this.theQuestion.correct_answer)
            },
            submitAnswer(){
                let isCorrect = false
                if (this.selectIndex === this.correctIndex){
                    isCorrect = true
                }
                this.answered = true
                this.increment(isCorrect)
            },
            answerClass(index){
                let answerClass = ''
                if(!this.answered && this.selectIndex === index){
                    answerClass = 'selected'
                } else if(this.answered && this.correctIndex === index){
                    answerClass = 'right' 
                } else if(this.answered && this.selectIndex === index && this.correctIndex !== index){
                    answerClass = 'wrong'
                }
                return answerClass
            }

        }
      
    } 
    
</script>
<style scoped>
.jumbotron{
    background-color: #e7e5f3;
    border-radius: 20px;
}
.jumbotron h1{
    font-family: 'Grenze Gotisch', cursive;
}
 
.list-group{
    margin: 10px;
}
.list-group-item{
    margin: 10px;
    border-radius: 0 25px 0 25px;
}
.list-group-item:hover{
    background-color: #E5E5E5;
    border-radius: 0 25px 0 25px;
}
.btn{
    margin: 5px;
}
.selected{
    background-color: #FFB6C1;
}
.right, .right:hover{
    background-color:#b2dfbd;
}
.wrong, .wrong:hover{
    background-color:#ff6864;
}
.btn{
    color: #8FC1A9!important;
    text-transform: uppercase;
    background: #ffffff;
    padding: 10px;
    border: 4px solid #8FC1A9 !important;
    border-radius: 6px;
    display: inline-block;
    transition: all 0.3s ease 0s;
    margin: 20px;
}
.btn:hover{
    color:#8FC1A9 !important;
    border-radius: 50px;
    border-color: #8FC1A9!important;
    transition: all 0.3s ease 0s;
}

</style>