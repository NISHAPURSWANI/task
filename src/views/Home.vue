<template>
  <form id="jq-form" v-on:submit.prevent="submit" class="myform">
    <div v-show="question_1" class="myform">
      <label>
        <b>Enter your Name</b>
        <span class="text-danger">*</span>
      </label>
      <br />
      <input
        type="text" 
        v-model.trim="$v.fullname.$model"
        :class="{'is-invalid':validationStatus($v.fullname)}"
        class="input" placeholder="Enter your name here "
        
        @keyup.enter="some()"
      />
      <div v-if="!$v.fullname.required" class="invalid-feedback">The name field is required</div>
      <br >press enter for next question
    </div>
    <br />

    <div v-show="question_2" class="myform" >
        <div class="col-12 form-group">
  <label class="col-form-label col-form-label-lg"><b>Enter your favorite color?</b> <span class="text-danger">*</span></label>
<select v-model="$v.colors.$model" :class="{'is-invalid':validationStatus($v.colors)}" class="form-control form-control-lg">
<option value="">Select Color</option>
<option :value="c.iso" :key="c.iso" v-for="c in colorsList">{{c.colors}}</option>
</select>
      

      </div>
          <button @click="somec()">to question 3</button>
    </div>

    <br />

    <div v-show="question_3" class="myform">
      <b>Q3. Do you have a pet?</b>
      <br >
      <input type="radio" id="yes" value="yes" v-model="ticked" @keyup.enter="somepy()" />
      <label for="yes">Yes</label>
      <input type="radio" id="no" value="no" v-model="ticked" @keyup.enter="somepn()" />
      <label for="no">No</label>
      <br />press enter for next question
    </div>
    <br />
    <div v-show="question_4" @keyup.enter="somepnm()" class="myform">
      <label>
        <b>Enter your pet's Name</b>
        <span class="text-danger">*</span>
      </label>
      <br />
      <input
        type="text"
        v-model.trim="$v.petname.$model"
        :class="{'is-invalid':validationStatus($v.petname)}"
        class="input" placeholder="Enter your pet's here "
        @keyup.enter="somepn()"
      />
      <div v-if="!$v.petname.required" class="invalid-feedback">The name field is required</div>
      <br />press enter for next question
    </div>
    <br />
    <div v-show="question_5" @keyup.enter="somes()" class="myform">
      <b>Q4. What are your Favorite Sports:</b>
      <br >
      <input type="checkbox" id="cricket" value="cricket" v-model="checkedNames" />
      <label for="cricket">Cricket</label>
      <input type="checkbox" id="football" value="football" v-model="checkedNames" />
      <label for="football">Football</label>
      <input type="checkbox" id="badminton" value="badminton" v-model="checkedNames" />
      <label for="badminton">Badminton</label>
      <input type="checkbox" id="tennis" value="tennis" v-model="checkedNames" />
      <label for="tennis">Tennis</label>
      <input type="checkbox" id="baseball" value="baseball" v-model="checkedNames" />
      <label for="baseball">BaseBall</label>
      <br />
press enter for next question
      <br />
    </div>
    <div v-show="question_6" class="myans">
      <img alt="Vue logo" src="../assets/thankyou.png" style="width:300px;height:300px;" />
      <br />

      <span>MY name is {{fullname}}</span>
      <br />
      <span>My favorite color is {{colors}}</span>
      <br />
      <span>No, I don't have a pet</span>
      <br />
      <span>My favorite sports are: {{ checkedNames }}</span>
      <br />
    </div>
    <div v-show="question_7" class="myans">
      <img alt="Vue logo" src="../assets/thankyou.png" style="width:300px;height:300px;" />
      <br />

      <span>MY name is {{fullname}}</span>
      <br />
      <span style="color:val">My favorite color is {{colors}}</span>
      <br />
      <span>Yes, I have a pet</span>
      <br />

      <span>My pet's name is : {{ petname }}</span>
      <br />
    </div>
  </form>
</template>
<script>
import { required } from "vuelidate/lib/validators";
export default {
  name: "jqForm",
  data: function() {
    return {
      fullname: "",
      petname: "",
      ticked: "",
      checkedNames: [],
      colors: '',
      colorsList: [],
      selected: "",
      question_1: true,
      question_2: false,
      question_3: false,
      question_4: false,
      question_5: false,
      question_6: false,
      question_7: false
    };
  },
  mounted: function() {
    var v = this;
    v.$http
      .get("http://localhost:4707/colors")
      .then(function(resp) {
        v.colorsList = resp.data;
      })
      .catch(function(err) {
        console.log(err);
      });
  },
  validations: {
    fullname: { required },
    petname: { required },
    colors: { required }
  },
  
  

  methods: {
    validationStatus: function(validation) {
      return typeof validation != "undefined" ? validation.$error : false;
    },
    submit: function() {
      this.$v.$touch();
      if (this.$v.$pendding || this.$v.$error) return;
    },

    some() {
      (this.question_2 = true), (this.question_1 = false), (this.question_3 = false);
    },
    somec() {
      (this.question_3 = true), (this.question_2 = false);
    },
    somepy() {
      (this.question_4 = true), (this.question_3 = false);
    },
    somepn() {
      (this.question_5 = true), (this.question_3 = false);
    },
    somepnm() {
      (this.question_7 = true), (this.question_5 = false), (this.question_4 = false);
    },
    somes() {
      (this.question_6 = true), (this.question_5 = false), (this.question_3 = false);
    }
  }
};
</script>
<style>
.myform {
  margin-top: 100px;
  margin-left: -400px;
}
.input{
  background-color: transparent;
  border: none;
  border-bottom: 1px solid blue;
  color: rgb(0, 0, 0);
  box-sizing: border-box red;
  font-family: 'Arvo';
  font-size: 18px;
  height: 30px;
  padding: 10px 0px;

  width: 350px;
}
.myans {
  margin-top: 50px;
  margin-left: -400px;
}

</style>
