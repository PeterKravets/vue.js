<template>
    <div class="wrapper">
        <form v-if="!formSubmitted" @submit.prevent="formSubmitted = true">
            <div class="progress">
                <div class="progress-bar" :style="progressBarWidth"></div>
            </div>
            <div>
                <app-input v-for="(field, index) in info"
                           :key="index"
                           :name="field.name"
                           :value="field.value"
                           :pattern="field.pattern"
                           @incrementbar="onProgressBar(index, true)"
                           @decrementbar="onProgressBar(index, false)"
                >
                </app-input>
            </div>
            <button class="btn btn-primary" :disabled="!done">
                Send Data
            </button>
        </form>
        <div v-else>
            <table class="table table-bordered">
                <tr v-for="field in info">
                    <td>{{ field.name }}</td>
                    <td>{{ field.value }}</td>
                </tr>
            </table>
        </div>
    </div>
</template>

<script>
    import AppInput from './components/Input'

   export default {
       data() {
           return {
               info: [
                   {
                       name: 'Name',
                       value: '',
                       pattern: /^[a-zA-Z ]{2,30}$/
                   },
                   {
                       name: 'Phone',
                       value: '',
                       pattern: /^[0-9]{7,14}$/
                   },
                   {
                       name: 'Email',
                       value: '',
                       pattern: /.+/
                   },
                   {
                       name: 'Some Field 1',
                       value: '',
                       pattern: /.+/
                   },
                   {
                       name: 'Some Field 2',
                       value: '',
                       pattern: /.+/
                   }
               ],
               formSubmitted: false,
               progressBar: 0
           }
        },
       computed: {
           progressBarWidth() {
               return {
                   width: (this.progressBar.length * 100 / this.info.length) + '%'
               }
           },
           done() {
               return this.progressBar.length == this.info.length;
           }
       },
       methods: {
           onProgressBar(index, inc) {
               if (inc) {
                   if(!this.progressBar.includes(index)) {
                       this.progressBar.push(index);
                   }
               } else {
                   if(this.progressBar.includes(index)) {
                       this.progressBar.splice(index, 1);
                   }
               }
           }
       },
       components: {
           AppInput
       }
   }
</script>

<style>

</style>