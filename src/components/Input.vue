<template>
    <div class="form-group">
        <label>{{ name }}</label>
        <i class="fa"
           v-if="activated"
           :class="getClass">
        </i>
        <input type="text"
               class="form-control"
               v-model="value"
               @input="setActivated"
        >
    </div>
</template>

<script>
    export default {
        name: "input",
        props: ['name', 'value', 'pattern'],
        data() {
            return {
                activated: false,
            }
        },
        computed: {
            validate() {
                let valid = this.pattern.test(this.value);

                if(valid) {
                    this.$emit('incrementbar');
                } else {
                    this.$emit('decrementbar');
                }

                return valid;
            },
            getClass() {
                return this.validate ?
                    'fa fa-check-circle success' :
                    'fa-exclamation-circle error';
            }
        },
        methods: {
            setActivated() {
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