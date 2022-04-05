<template>
    <div class="questions-ctr">
        <div class="progress">
            <div class="bar" :style="{ width: bar_Width }"></div>
            <div class="status">
                {{ this.index }} out of {{ questions.length }} questions
                answered
            </div>
        </div>
        <!-- <transition-group name="fade"> -->
            <div class="single-question">
                <div class="question">{{ questionText }}</div>
                <div class="answers">
                    <div
                        class="answer"
                        v-for="(answer, index) in answerText"
                        :key="index"
                        @click="pass_Answer(answer.is_Correct)"
                    >
                        {{ answer.aValue }}
                    </div>
                </div>
            </div>
        <!-- </transition-group> -->
    </div>
</template>

<script>
export default {
    name: "questions-component",
    props: ["questions", "questionText", "answerText", "index"],
    emits: ["pass_Answer"],

    methods: {
        pass_Answer(is_Correct) {
            this.$emit("pass_Answer", is_Correct);
        },
    },
    computed: {
        bar_Width() {
            return `${this.index * 33}%`;
        },
    },
};
</script>
