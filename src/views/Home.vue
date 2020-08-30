<template>
<form id="signup-form" v-on:submit.prevent="submit">
<div class="row">
  <div class="col-12 form-group" v-show="q1">
  <label class="col-form-label col-form-label-lg">Full Name <span class="text-danger">*</span></label>  
 
    <div v-if="!$v.fullname.required" class="invalid-feedback"> The name field is required</div>
  </div>
 <div v-show="q2">
   feeee
 </div>
  </div>
    <div class="col-12 form-group text-center">
     <button class="btn btn-vue btn-lg col-4">Sign up</button>
</div>
</form>
  
</template>
<script>
import { required } from 'vuelidate/lib/validators'

export default{
  name:'SignupForm',
  data:function(){
    return{
      fullname:'',
     /* email:'',
      country:'',
      password:'',
      countryList:[]*/
      q1:true,
      q2:false
    }
  },
  validations:{
      fullname:{required},
     /* email:{required,email},
      country:{required},
      password:{required , minLength:minLength(6), maxLength:maxLength(18)}*/

  },
/*  mounted:function(){
      var v=this;
      v.$http.get('http://localhost:4600/countries')
      .then(function(resp){
          v.countryList=resp.data;

      })
      .catch(function(err){
          console.log(err)

      })
  },*/
  methods:{
      validationStatus:function(validation){
          return typeof validation !="undefined"?validation.$error:false;
      },
      submit:function(){

          this.$v.$touch();
          if(this.$v.$pendding || this.$v.$error) return;
          //alert("done");

      }
  }
}
</script>
<style>
.btn-vue{
  background-color: #53b985;
  color:#31485D;
  font-weight: bold;
}
</style>