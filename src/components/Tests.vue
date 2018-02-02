<template>
    <div>
        <div v-if="answers.length != questions.length">
            <app-answers v-if="active === index" v-for="(question, index) in questions"
                         :title="question.title"
                         :answers="question.answers"
                         :type="question.type"
                         :key="index"
                         @submittest="onSubmit(index, $event)"
            ></app-answers>
        </div>
        <div v-else>
            <h5>Ваши ответы</h5>
            <table style="width: 300px" class="table table-bordered">
                <tr v-for="(answer, index) in answers">
                    <td>{{ questions[index].title }}</td>
                    <td><span v-for="item in answer">{{ item.index }} {{ item.value }}</span></td>
                </tr>
            </table>
        </div>
    </div>

</template>

<script>
    import AppAnswers from './Answers'

    export default {
        data() {
            return {
                questions : getQuestions(),
                answers: [],
                active: 0
            }
        },
        methods: {
            onSubmit(index, data) {
                this.answers.push(data);
                this.active = index + 1;
            }
        },

        components: {
            AppAnswers
        }
    }

    function getQuestions() {
        return [
            {
                title: 'Что с css описывает цвет шрифта?',
                answers: [
                    'color',
                    'margin',
                    'padding',
                    'background'
                ],
                type: 'radio'
            },
            {
                title: 'Какой html елемент строчный?',
                answers: [
                    'span',
                    'p',
                    'div',
                    'img'
                ],
                type: 'checkbox'
            }
        ]
    }
</script>

<style scoped>

</style>