<template>
    <questions-queue
    :questions="questions"
    :unit-id="unitID"
    :is-revision="false"
    @endOfTest="endOfTest"
        >
        </questions-queue>
        </template>

        <script>
    import QuestionsQueue from "../components/QuestionsQueue";
    import store from "../assets/store";
    import Test from "../models/Test";

    export default {
        name: "Test",
        data: () => ({
            store: store,
            questions: [],
            unitID: null,
            chapterID: null
        }),

        components: {
            QuestionsQueue
        },
        methods: {
            endOfTest(answers, score) {
                console.log(answers);
                let test = new Test({
                    chapterID: this.chapterID,
                    unitID: null,
                    score: score,
                    date: new Date().toISOString().slice(0, 19).replace('T', ' ')
                });
                this.store.addAnswers(answers, test)
            },
        },
        created() {
            this.unitID = this.$route.params.unitID;
            this.chapterID = this.$route.params.chapterID;
            this.questions = store.getChapterQuestions(this.chapterID);
        }
    }
</script>

<style scoped>

</style>