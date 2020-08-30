
<template>
  <div class="home">
    hello
    <div v-show="q1" >
    Q1. What's your name?
     
   <!--input type="text" v-model="name"  @keyup.enter="names , q3=true , q1=false" > <br>-->
    <!--<input type="text" v-model="name" @keyup.enter="names"  v-on:keyup.enter="q2=true, q1=false"   > <br>-->
    <input type="text" v-model="name" @keyup.enter="names" >
    

      <!--<button @click="q2=true , q1=false" >Add 1</button>-->
 <!-- <p>The button above has been clicked {{  }} times.</p>-->

    </div>
    <div v-show="q2"     >
    Q2. What's your favorite color?
    
    <select v-model="selected"  >
      <option disabled value=""></option>

  <option  value="red" style="color:red;">Red</option>
  <option value="blue" style="color:blue;" >Blue</option>
  <option value="green" style="color:green;" >Green</option>
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
            <button @click="q3=true,q2=false">to q3</button>
                  </div>


    <div v-show="q3" >
    Q3. Do you have a pet? 
    <input type="radio" id="yes" value="yes" v-model="ticked" @keyup.enter="q4=true , q3=false"><label for="yes"  >Yes</label>
    <input type="radio" id="no" value="no" v-model="ticked" @keyup.enter="q5=true , q3=false"><label for="no">No</label>
    
<br>
      <!--<button @click="q4=true,q3=false">Add 1</button>-->

    </div>
    <div v-show="q4" >
    Q4. What's your pet's name?
    <input type="text" v-model="pname" v-on:keyup.enter="pnames"   @keyup.enter="q7=true , q4=false "  > <br>{{pname}}
<br>
      <!--<button @click="q5=true,q4=false">Add 1</button>-->

    </div>
    <div v-show="q5" @keyup.enter="q6=true , q5=false">
    Q4. What are your Favorite Sports:
    <input type="checkbox" id="cricket" value="cricket" v-model="checkedNames">
    <label for="cricket">Cricket</label>
    <input type="checkbox" id="football" value="football" v-model="checkedNames">
    <label for="football">Football</label>
    <input type="checkbox" id="badminton" value="badminton" v-model="checkedNames">
    <label for="badminton">Badminton</label>
   <input type="checkbox" id="tennis" value="tennis" v-model="checkedNames">
    <label for="tennis">Tennis</label>
    <input type="checkbox" id="baseball" value="baseball" v-model="checkedNames">
    <label for="baseball">BaseBall</label>

          <!--<button @click="q6=true,q5=false">Add 1</button>-->

<br>
    </div>
    <div v-show="q6">
          <img alt="Vue logo" src="../assets/thankyou.png" /><br>

           <span>MY name is {{name}}</span><br>
          <span>My favorite color is {{selected}}</span><br>
          <span>No, I don't have a pet</span><br>
          <span>My  favorite sports are: {{ checkedNames }}</span><br>
          

     </div>
      <div v-show="q7">
          <img alt="Vue logo" src="../assets/thankyou.png" /><br>

           <span>MY name is {{name}}</span><br>
           <span>My favorite color is {{selected}}</span><br>
           <span>Yes, I have a pet</span><br>

          <!--<span>My  favorite sports are: {{ checkedNames }}</span><br>-->
          <span>My pet's name is : {{ pname }}</span><br>

     </div>
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "Home",
  /*components: {
    HelloWorld
  }*/
  data:function(){
    return{

    name:'',
    //fullname:'',
    q1:true,
    q2:false,
    q3:false,
    q4:false,
    q5:false,
    q6:false,
    ticked:'',
    pname:'',
    checkedNames:[],
    selected:'',
   // counter:0

  }
  
  
  },
   methods:{
    names: function(e) {
      if (e.keyCode === 13) {
        if (this.name==''){
          alert('enter your name');
          
        }
      
        else{
          //alert('name entered');
          //q2:true
         // v-hide.q1;
        // this.hide(q1);
         //this.show(q2);
          
          }
          
                   
          

        
      }      
    },
    pnames: function(e) {
      if (e.keyCode === 13) {
        if (this.pmsg==''){
          alert('enter your pet/s name');
        }
        else{
          alert('name entered');
        
      }      
    }
   
  },
 
  
  
}
};



</script>
  