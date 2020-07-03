<template>
    <div class="question-box">
    <b-jumbotron>
        <template v-slot:header>Question</template>

        <template v-slot:lead>
        Q
        </template>

        <hr class="my-4">

        <p>
       ans
        </p>

        <b-button variant="primary" href="#">Submit</b-button>
        <b-button variant="success" href="#">Next Q</b-button>
    </b-jumbotron>
    </div>

</template>