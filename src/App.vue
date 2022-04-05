<template>
    <div class="ctr">
        <transition name="fade" mode="out-in">
            <questions-component
                v-if="questionsAnswered < 3"
                :questions="questions"
                :questionText="questionText"
                :answerText="answerText"
                :index="index"
                :correct_Answers="correct_Answers"
                @pass_Answer="pass_Answer"
            />
            <result-component v-else :result="result" />
        </transition>
        <button
            v-if="questionsAnswered === 3"
            type="button"
            class="reset-btn"
            @click.prevent="reset"
        >
            Reset
        </button>
    </div>
</template>

<script>
import questionsComponent from "./components/Questions.vue";
import resultComponent from "./components/Result.vue";
export default {
    name: "App-component",
    components: { questionsComponent, resultComponent },
    data() {
        return {
            questionsAnswered: 0,
            index: 0,
            correct_Answers: 0,
            questions: [
                {
                    id: 1,
                    qValue: "What does HTML stand for?",
                    answers: [
                        { aValue: "Hello To My Land", is_Correct: false },
                        {
                            aValue: "HyperText Markup Language",
                            is_Correct: true,
                        },
                        {
                            aValue: "Hey Text Markup Language",
                            is_Correct: false,
                        },
                        {
                            aValue: "HyperText Makeup Language",
                            is_Correct: false,
                        },
                    ],
                },
                {
                    id: 2,
                    qValue: "What does JS stand for?",
                    answers: [
                        { aValue: "JavaShell", is_Correct: false },
                        { aValue: "JavaServer", is_Correct: false },
                        { aValue: "JavaScript", is_Correct: true },
                        { aValue: "JavaShop", is_Correct: false },
                    ],
                },
                {
                    id: 3,
                    qValue: "What does CSS stand for?",
                    answers: [
                        { aValue: "Cascading Style Sleep", is_Correct: false },
                        { aValue: "Cascading Style Sheets", is_Correct: false },
                        { aValue: "Cascading Show Sheet", is_Correct: false },
                        { aValue: "Cascading Style Sheet", is_Correct: true },
                    ],
                },
            ],
            results: {
                correct: {
                    title: "Wow, you're a genius!",
                    desc: "Studying has definitely paid off for you!",
                },
                false: {
                    title: "Try again!",
                    desc: "Do a little more studying and you may succeed!",
                },
            },
        };
    },
    methods: {
        pass_Answer(is_Correct) {
            this.index++;
            this.questionsAnswered++;
            if (is_Correct) {
                this.correct_Answers++;
            }
            console.log(this.correct_Answers);
        },

        reset() {
            this.index = 0;
            this.questionsAnswered = 0;
        },
    },
    computed: {
        questionText() {
            return this.questions[this.index].qValue;
        },
        answerText() {
            return this.questions[this.index].answers;
        },
        result() {
            return this.correct_Answers < 3
                ? this.results.false
                : this.results.correct;
        },
    },
};
</script>

<style lang="scss">
.ctr {
    margin: 0 auto;
    max-width: 600px;
    width: 100%;
    box-sizing: border-box;
    position: relative;
}
.questions-ctr {
    position: relative;
    width: 100%;
}
.question {
    width: 100%;
    padding: 20px;
    font-size: 32px;
    font-weight: bold;
    text-align: center;
    background-color: #00ca8c;
    color: #fff;
    box-sizing: border-box;
}
.single-question {
    position: relative;
    width: 100%;
}
.answer {
    border: 1px solid #8e959f;
    padding: 20px;
    font-size: 18px;
    width: 100%;
    background-color: #fff;
    transition: 0.2s linear all;
}
.answer span {
    display: inline-block;
    margin-left: 5px;
    font-size: 0.75em;
    font-style: italic;
}
.progress {
    height: 50px;
    margin-top: 10px;
    background-color: #ddd;
    position: relative;
}
.bar {
    height: 50px;
    background-color: #ff6372;
    transition: all 0.3s linear;
}
.status {
    position: absolute;
    top: 15px;
    left: 0;
    text-align: center;
    color: #fff;
    width: 100%;
}
.answer:not(.is-answered) {
    cursor: pointer;
}
.answer:not(.is-answered):hover {
    background-color: #8ce200;
    border-color: #8ce200;
    color: #fff;
}

.title {
    width: 100%;
    padding: 20px;
    font-size: 32px;
    font-weight: bold;
    text-align: center;
    background-color: #12cbc4;
    color: #fff;
    box-sizing: border-box;
}
.desc {
    border: 1px solid #8e959f;
    padding: 20px;
    font-size: 18px;
    width: 100%;
    background-color: #fff;
    transition: 0.4s linear all;
    text-align: center;
}
.fade-enter-from {
    opacity: 0;
}
.fade-enter-active {
    transition: all 0.3s linear;
}
.fade-leave-active {
    transition: all 0.3s linear;
    opacity: 0;
    position: absolute;
}

.reset-btn {
    background-color: #ff6372;
    border: 0;
    font-size: 22px;
    color: #fff;
    padding: 10px 25px;
    margin: 10px auto;
    display: block;
}

.result {
    width: 100%;
}

.reset-btn:active,
.reset-btn:focus,
.reset-btn:hover {
    border: 0;
    outline: 0;
}
</style>
