<template>
    <div>
        <h2>
            How much is this? <br/> <span>{{question}}</span>
        </h2>
        <div>
            <div class="answer" v-for="(answer, index) in answers" @click="answerChosen(answer.ifCorrect)" :key="index">
                {{answer.content}} 
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
                {ifCorrect: true, content: 0},
                {ifCorrect: true, content: 0},
                {ifCorrect: true, content: 0},
                {ifCorrect: true, content: 0}
            ]
        }
    },

    methods: {
        createNewQuestion() { 
            //numbers from 1 to 10
            const a = this.generateRandomNumber(5.5,3.5,false);
            const b = this.generateRandomNumber(5.5,3.5,false);
            const result = a*b;
            const times = "&times;";
            this.question = `${a} \xD7 ${b}`
            //position of correct answer
            const correctIndex = Math.floor(Math.random()*4);

            // using set characteristic to not repeat values
            const setAnswers = new Set();
            while (setAnswers.size < 4) {
                setAnswers.add(this.generateRandomNumber(result, 10));
            }
            const arrAnswers = [...setAnswers];
            this.answers[0].ifCorrect = false;
            this.answers[1].ifCorrect = false;
            this.answers[2].ifCorrect = false;
            this.answers[3].ifCorrect = false;

            this.answers[0].content = arrAnswers[0];       
            this.answers[1].content = arrAnswers[1];       
            this.answers[2].content = arrAnswers[2];       
            this.answers[3].content = arrAnswers[3];    
            
            this.answers[correctIndex].ifCorrect = true;
            this.answers[correctIndex].content = result;

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

    div {
        color: var(--primary-color);
    }
</style>

