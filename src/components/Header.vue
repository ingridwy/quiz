<template>
    <div>
    <b-nav>
        <b-nav-item disabled>Your Result</b-nav-item>
    
        <b-nav-item disabled>Count: {{numCorrect}}/{{numTotal}}</b-nav-item>
    </b-nav>
    </div>
</template>

<script>
export default {
    props: [
        'numCorrect',
        'numTotal'
    ]
}
</script>

<style scoped>
.nav-item {
    font-size: 25px;
}
</style>