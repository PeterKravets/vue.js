<template>
    <div class="form-group">
        <label>{{ name }}</label>
        <i class="fa"
           v-if="activated"
           :class="getClass">
        </i>
        <input type="text"
               class="form-control"
               @input="onInput($event.target.value)"
        >
    </div>
</template>

<script>
    export default {
        props: {
            name: {
                validator(val) {
                    return val != '' && val.length < 20;
                }
            },
            value: {
                type: [String, Number],
                required: true,
            },
            pattern: {
                type:RegExp,
                required: true
            }
        },
        data() {
            return {
                activated: false,
            }
        },
        computed: {
            getClass() {
                return this.pattern.test(this.value) ?
                    'fa fa-check-circle success' :
                    'fa-exclamation-circle error';
            }
        },
        methods: {
            onInput(value) {
                this.$emit('datachanged', {
                    validate: this.pattern.test(value),
                    value: value
                });

                this.activated = true;
            }
        }
    }
</script>

<style scoped>
    .error {
        color: red;
    }
    .success {
        color: green;
    }
</style>