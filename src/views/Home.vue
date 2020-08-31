<template>
<form id="jq-form" v-on:submit.prevent="submit" class="myform">
  <div  v-show="q1" class="myform">
  <label ><b>Enter your Name</b> <span class="text-danger">*</span></label>  <br>
  <input type="text" v-model.trim="$v.fullname.$model" :class="{'is-invalid':validationStatus($v.fullname)}"  class="form-control form-control-lg"  @keyup.enter="some()">
    <div v-if="!$v.fullname.required" class="invalid-feedback"> The name field is required</div><br>press enter for next question
  </div>
  <br>
  
<div v-show="q2" @keyup.enter="somec()" class="myform" >
  <b>  Q2. What's your favorite color?</b><br>
    
    <select v-model="selected"  >
      <option disabled value=""></option>
  <option  value="red" style="color:red;" >Red</option>
  <option value="blue" style="color:blue;" >Blue</option>
  <option value="gren" style="color:green;" >Green</option>
  <option value="yellow" style="color:yellow;" >Yellow</option>
   <option value="orange" style="color:orange;" >Orange</option>
  <option value="black"   style="color:black;" >Black</option>
  <option value="gold"    style="color:gold;" >Gold</option>
  <option value="purple"   style="color:purple;" >Purple</option>
   <option value="cyan"   style="color:cyan;" >Cyan</option>
  <option value="maroon"   style="color:maroon;" >Maroon</option>
  <option value="gray"   style="color:gray;" >Gray</option>
  <option value="brown"   style="color:brown;" >Brown</option>
   <option value="darkgreen"   style="color:darkgreen;" >Dark Green</option>
  <option value="olive"   style="color:olive;" >Olive</option>
  <option value="magenta"   style="color:magenta;">Magenta</option>
  <option value="indigo"   style="color:indigo" >Indigo</option>
      </select ><br>
<button @click="somec()">to question 3</button>
   </div>


  <br>
  

  <div v-show="q3" class="myform" >
    <b>Q3. Do you have a pet?</b> <br>
    <input type="radio" id="yes" value="yes" v-model="ticked"  @keyup.enter="somepy()" ><label for="yes"  >Yes</label>
    <input type="radio" id="no" value="no" v-model="ticked" @keyup.enter="somepn()"   ><label for="no">No</label><br>press enter for next question
  </div>
<br>
  <div  v-show="q4" @keyup.enter="somepnm()" class="myform">
  <label ><b>Enter your pet's Name</b> <span class="text-danger">*</span></label> <br> 
  <input type="text" v-model.trim="$v.petname.$model" :class="{'is-invalid':validationStatus($v.petname)}" class="form-control form-control-lg" @keyup.enter="somepn()">
    <div v-if="!$v.petname.required"  class="invalid-feedback"> The name field is required</div><br>press enter for next question
  </div>
  <br>
  <div v-show="q5"  @keyup.enter="somes()" class="myform" >
   <b> Q4. What are your Favorite Sports:</b><br>
    <input type="checkbox" id="cricket" value="cricket" v-model="checkedNames">
    <label for="cricket">Cricket</label>
    <input type="checkbox" id="football" value="football" v-model="checkedNames">
    <label for="football">Football</label>
    <input type="checkbox" id="badminton" value="badminton" v-model="checkedNames">
    <label for="badminton">Badminton</label>
   <input type="checkbox" id="tennis" value="tennis" v-model="checkedNames">
    <label for="tennis">Tennis</label>
    <input type="checkbox" id="baseball" value="baseball" v-model="checkedNames">
    <label for="baseball">BaseBall</label><br>press enter for next question


<br></div>
   <div v-show="q6" class="myform">
          <img alt="Vue logo" src="../assets/thankyou.png" /><br>

           <span>MY name is {{fullname}}</span><br>
          <span>My favorite color is {{selected}}</span><br>
          <span>No, I don't have a pet</span><br>
          <span>My  favorite sports are: {{ checkedNames }}</span><br>
          

     </div>
      <div v-show="q7" class="myform">
          <img alt="Vue logo" src="../assets/thankyou.png" /><br>

           <span>MY name is {{fullname}}</span><br>
           <span style="color:val">My favorite color is {{selected}}</span><br>
           <span>Yes, I have a pet</span><br>

          <!--<span>My  favorite sports are: {{ checkedNames }}</span><br>-->
          <span>My pet's name is : {{ petname }}</span><br>

     </div>



</form>
  
</template>
<script>
import { required } from 'vuelidate/lib/validators'
export default{
  name:'jqForm',
  data:function(){
    return{
      fullname:'',
      petname:'',
      ticked:'',
      checkedNames:[],
      color:'',
      colorList:[],
      selected:'',
      q1:true,
      q2:false,
      q3:false,
      q4:false,
      q5:false,
      q6:false,
      q7:false
      //#q2(hide)
    }
  },
  validations:{
      fullname:{required},
      petname:{required},
      color:{required}
    
  },
  mounted:function(){
      var v=this;
      v.$http.get('http://localhost:4700/colors')
      .then(function(resp){
          v.colorList=resp.data;
      })
      .catch(function(err){
          console.log(err)
      })

  },
  
  
  methods:{
      validationStatus:function(validation){
          return typeof validation !="undefined"?validation.$error:false;
      },
      submit:function(){
          this.$v.$touch();
          if(this.$v.$pendding || this.$v.$error) return;
          alert("done");
      },
          
        some(){
         this.q2=true,
         this.q1=false,
         this.q3=false

       },
       somec(){
             
         this.q3=true,
         this.q2=false
       },
       somepy(){
         this.q4=true,
         this.q3=false
  

       },
       somepn(){
         this.q5=true,
         this.q3=false
    
         

       },
       somepnm(){
         this.q7=true,
         this.q5=false,
         this.q4=false
       },
       somes(){
         this.q6=true,
         this.q5=false,
         this.q3=false
       }



     

  }
}
</script>
<style>
.myform{
margin-top:100px;
margin-left:-100px;
}
</style>
