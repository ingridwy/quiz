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
 
        <b-button variant="primary" href="#">Submit</b-button>
        <b-button @click="next" variant="success" href="#">Next Q</b-button>
    </b-jumbotron>
    </div>

</template>
<script>
    import _ from 'lodash'
    export default { 
        props: {
            theQuestion: Object,
            next: Function
        },
        data() {
            return{
                selectIndex: null,
                shuffledAnswer: []
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
            theQuestion(){
                this.selectIndex = null
                this.shuffleAnswer()
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
            }

        }
      
    }
    
</script>
<style scoped>
.list-group{
    margin :10px;
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