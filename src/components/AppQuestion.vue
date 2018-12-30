<template>
    <div class="all-container">
        <h2 class="question">
            How much is <span class="question__numbers">{{question}} </span>
        </h2>
        <div class="answers-container">
            <div class="answer" v-for="(answer, index) in answers" @click="answerChosen(answer.correct)" :key="index">
                {{answer.answer}} 
            </div>
        </div>
    </div>
</template>

<script>
export default {

    data() {
        return {
            question: 'Something went wrong',
            answers: [
                {correct: true, answer: 0},
                {correct: true, answer: 0},
                {correct: true, answer: 0},
                {correct: true, answer: 0}
            ]
        }
    },

    methods: {
        createNewQuestion() { 
            const a = this.generateRandomNumber(5,5,false);
            const b = this.generateRandomNumber(5,5,false);
            const result = a*b;
            const times = "&times;";
            this.question = `${a} \xD7 ${b}`
            const correctIndex = Math.floor(Math.random()*4);

            const setAnswers = new Set();
            while (setAnswers.size < 4) {
                setAnswers.add(this.generateRandomNumber(result, 10));
            }
            const arrAnswers = [...setAnswers];
            this.answers[0].correct = false;
            this.answers[1].correct = false;
            this.answers[2].correct = false;
            this.answers[3].correct = false;

            this.answers[0].answer = arrAnswers[0];       
            this.answers[1].answer = arrAnswers[1];       
            this.answers[2].answer = arrAnswers[2];       
            this.answers[3].answer = arrAnswers[3];    
            
            this.answers[correctIndex].correct = true;
            this.answers[correctIndex].answer = result;

        },
        generateRandomNumber(center, radius, excludeCenter=true) {
            let rand;
            do {
                rand = Math.round(center + (Math.random() - 0.5) * 2 * radius);
            } while (rand === center && excludeCenter);
            return rand;
        },
        answerChosen(ifCorrect) {
            this.$emit('answerChosen',ifCorrect)
        }
    },

    created() {
        this.createNewQuestion();
    },
}
</script>

<style lang="scss" scoped>

* {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
}
.all-container {

    width: 100%;
}
.answers-container {
    width: 100%;
    display: flex;
    justify-content: space-between;
    flex-flow: row wrap;
}
.answer {
    cursor: pointer;
    text-align: center;
    width: 4rem;
    padding: 1.2rem 0;
    font-size: 1.6rem;
    background: rgb(34, 112, 24);
    box-shadow: 0 0 10px 3px rgb(8, 37, 4);
    border-radius: 1000px;
    color: white;
}
.answer:hover {
    background: rgb(16, 80, 8);
}
.answer:active {
    background: rgb(8, 39, 4);
}
.question {
    text-align: center;
    margin-bottom: 1rem;
    &__numbers {
        display: block;
        font-size: 2em;
        color: green;
    }
}
</style>

