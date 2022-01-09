<template>
  <div class="post-create">
      <form class="ui form">
          <div class="fields">
              <div class="four wide field">
                  <label for="">Title</label>
                  <input type="text" name="title" @change="handleChange" :value="form.title">
              </div>
              <div class="six wide field">
                  <label for="">Body</label>
                  <input type="text" name="body" @change="handleChange" :value="form.body">
              </div>
              <div class="two wide field">
                  <button class="ui primary button submit-button" @click="onFormSubmit">Save</button>
              </div>
          </div>
      </form>
  </div>
</template>

<script>
export default {
    name: "PostCreate",
    props:{
        form:{
            type:Object
        }
    },
    methods:{
        handleChange(event){
            const {name, value} = event.target;
            let frm = this.form;
            frm[name] = value;
        },
        onFormSubmit(e){
            e.preventDefault();
            if(this.formValidation()){
                // console.log('form submit');
                this.$emit('onFormSubmit', this.form);
            }
        },
        formValidation(){
            if(document.getElementsByName('title')[0].value === ''){
                alert('Please insert title');
                return false;
            }
            if(document.getElementsByName('body')[0].value === ''){
                alert('Please insert body');
                return false;
            }
            return true;
        }
    }
}
</script>

<style>

</style>