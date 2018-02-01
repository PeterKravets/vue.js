<template>
    <div class="wrapper">
        <form v-if="!formSubmitted" @submit.prevent="formSubmitted = true">
            <div class="progress">
                <div class="progress-bar" :style="progressBarWidth"></div>
            </div>
            <div>
                <app-input
                       v-for="(field, index) in info"
                       :key="index"
                       :name="field.name"
                       :value="field.value"
                       :pattern="field.pattern"
                       @datachanged="onDataChange(index, $event)"
                >
                </app-input>
            </div>
            <button class="btn btn-primary" :disabled="done != info.length">
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
               progressBar: 0,
               controls: []
           }
        },
       computed: {
           done() {
               return this.controls.length;
           },
           progressBarWidth() {
               return {
                   width: (this.done * 100 / this.info.length) + '%'
               }
           },
       },
       methods: {
           onDataChange(index, data) {
               this.info[index].value = data.value;

               if(data.validate && !this.controls.includes(index)) {
                   this.controls.push(index);
               }

               if(!data.validate && this.controls.includes(index)) {
                   this.controls.splice(this.controls.indexOf(index), 1);
               }
           }
       },
       components: {
           AppInput
       }
   }

    /**
     * Or we can do it via created() hook and setup controlls array,
     * and then only update it error value "true, false"
     * But and also we will need cycle in done() computed property
     * which will go through controls[] array, and check if controls[index] == true, we do done++
     * and then return done;
     */
</script>

<style>

</style>