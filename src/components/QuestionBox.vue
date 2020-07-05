<template>
    <div class="question-box">
    <b-jumbotron>
        <template v-slot:header>Question</template>

        <template v-slot:lead>
        {{ theQuestion.question }}
        </template>

        <hr class="my-4">
            <b-list-group v-for="(answer,index) in answers" :key="index">
                <b-list-group-item>{{ answer }}</b-list-group-item>
            </b-list-group>

        <b-button variant="primary" href="#">Submit</b-button>
        <b-button @click="next" variant="success" href="#">Next Q</b-button>
    </b-jumbotron>
    </div>

</template>
<script>
    export default { 
        props: {
            theQuestion: Object,
            next: Function
        },
        computed:{
            answers(){
                let answers=[...this.theQuestion.incorrect_answers]
                answers.push(this.theQuestion.correct_answer)
                return answers
            }
        }, 
        mounted() {
        console.log(this.thisQuestion)
    }
    }
    
</script>