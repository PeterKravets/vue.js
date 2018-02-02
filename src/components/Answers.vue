<template>
    <form @submit.prevent="onSubmit()">
        <h4>{{ title }}</h4>
            <div v-if="type == 'radio'">
                <ul>
                    <li v-for="(answer, index) in answers">
                        <input type="radio" name='answer' :value="answer" @change="onChange(index, $event.target.value)"> {{ answer }}
                    </li>
                </ul>
            </div>
            <div v-else>
                <ul>
                    <li v-for="(answer, index) in answers">
                        <input type="checkbox" name='answer' :value="answer" @change="onChange(index, $event.target.value)"> {{ answer }}
                    </li>
                </ul>
            </div>

        <button class="btn btn-primary" v-if="selected">Next</button>
    </form>
</template>

<script>
    export default {
        props: ['title', 'answers', 'type', 'index'],
        data() {
            return {
                selectedAnswer: [],
                selected: false,
            }
        },
        methods: {
            onChange(index, value) {
                this.selectedAnswer.push({
                    index: index,
                    value: value
                });
                this.selected = true;
            },
            onSubmit() {
                this.$emit('submittest', this.selectedAnswer);
            }
        }
    }
</script>

<style scoped>

</style>