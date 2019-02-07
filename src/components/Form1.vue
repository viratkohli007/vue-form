<template>
	<div>
    <form>
    <div v-if="first">

  <div class="form-group row">
    <label class="col-lg-2 col-form-label" ref="search" >First Name</label>
    <div class="col-lg-8">
      <input type="text" id="fname" class="form-control" placeholder="First Name" v-model.trim="fname" :class="{focus:hasEr.fname}">
    </div>
  </div>
  <div class="form-group row">
    <label class="col-lg-2 col-form-label">Last Name</label>
    <div class="col-lg-8">
      <input type="text" id="lname" class="form-control" placeholder="Last Name" v-model.trim="lname" :class="{focus: hasEr.lname}">
    </div>
  </div>
  <div class="form-group row">
    <label class="col-lg-2 col-form-label">Email</label>
    <div class="col-lg-8">
      <input type="email" id="email" v-model.trim="email" class="form-control" placeholder="Email" :class="{focus: hasEr.email}">
    </div>
  </div>
  <div class="form-group row">
    <label class="col-lg-2 col-form-label">Mobile</label>
    <div class="col-lg-8">
      <input type="number" id="mobile" class="form-control" placeholder="Mobile no" v-model.trim="mobile" :class="{focus: hasEr.mobile}">
    </div>
  </div>
  <div class="form-group row">
    <div class="col-lg-2">
      <input type="submit" class="btn btn-primary" value="Next" @click="nextPage">
    </div>
  </div>

	 </div>

<div v-if="second">

	<div class="form-group row">
    <label class="col-lg-2 col-form-label">Bank Name</label>
    <div class="col-lg-8">
      <input type="text" class="form-control" v-model.trim="bName" placeholder="Bank Name" :class="{focus: hasEr.bName}">
    </div>
  </div>
  <div class="form-group row">
    <label class="col-lg-2 col-form-label">Bank Brach</label>
    <div class="col-lg-8">
      <input type="text" class="form-control" placeholder="Bank Branch"
      v-model.trim="bBranch" :class="{focus: hasEr.bBranch}">
    </div>
  </div>
  <div class="form-group row">
    <label class="col-lg-2 col-form-label">Account no.</label>
    <div class="col-lg-8">
      <input type="number" class="form-control" placeholder="Account no."
      v-model.trim="acc" :class="{focus: hasEr.acc}">
    </div>
  </div>
  <div class="form-group row">
    <label class="col-lg-2 col-form-label">IFSC code</label>
    <div class="col-lg-8">
      <input type="text" class="form-control" placeholder="IFSC code" v-model.trim="ifsc" :class="{focus: hasEr.ifsc}">
    </div>
  </div>
  <div class="form-group row">
    <div class="col-lg-2">
      <input type="submit" class="btn btn-primary" value="Previous" @click="previousPage">
    </div>
    <div class="col-lg-2">
      <input type="submit" class="btn btn-primary" value="Submit"  @click="store">
    </div>
  </div>
  </div>
		</form>

</div>


</template>
<script>

  export default{
     data: function(){
     	return{
     		second: false,
     		first: true,
        fname: "",
        lname: "",
        email: "",
        mobile: "",
        bName: "",
        bBranch:"",
        ifsc:"",
        acc: "",
        abc:0,
        hasEr: {
          fname: false,
          lname: false,
          email: false,
          mobile: false,
          bName:false,
          bBranch:false,
          ifsc: false,
          acc: false
        }

     	}
     },
    methods: {
    	nextPage(){
    		this.second = true,
    		this.first = false
    	},
    	previousPage(){
    		this.first=true,
    		this.second=false
    	},
    	store(){
        if(this.fname !="" && this.validName(this.fname)){
        localStorage.setItem('firstName', this.fname)
      }else{
        this.abc =1;
        this.hasEr.fname = true
      }
      if (this.lname !="" && this.validName(this.lname)) {
        localStorage.setItem('lastName', this.lname)
      }else{
        this.abc = 1
        this.hasEr.lname = true
      }
      if(this.email != "" && this.validEmail(this.email)){
        localStorage.setItem('email', this.email)
      }else{
        this.abc = 1;
        this.hasEr.email = true
      }
      if(this.mobile !="" && this.phonenumber(this.mobile)){
        localStorage.setItem('mobile no', this.mobile)
      }else{
        this.abc = 1
        this.hasEr.mobile = true
      }
      if(this.bName !="" && this.validName(this.bName)){
        localStorage.setItem('Bank Name', this.bName)
      }else{
        this.abc = 2
        this.hasEr.bName = true
      }
      if(this.bBranch !="" && this.validName(this.bBranch)){
        localStorage.setItem('Branch', this.bBranch)
      }else{
        this.abc = 2
        this.hasEr.bBranch = true
      }
      if(this.ifsc != "" ){
        localStorage.setItem('IFSC', this.ifsc)
      }else{
        this.abc = 2
        this.hasEr.ifsc = true
      }
      if(this.acc !="" && this.acccVal(this.acc)){
        localStorage.setItem('Account No', this.acc)
      }else{
        this.abc = 2
        this.hasEr.acc = true
      }
      if(this.abc == 1){
         this.previousPage()
      }
      if(this.abc == 2){
        this.nextPage()
      }
    	},
      validEmail: function (email) {
      var re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
      return re.test(email);
    },
    phonenumber: function (inputtxt){
     // console.log(">>>>>>>>>>>>>>>>>>>>>>>>>>>");
     ///^[1-9]{1}[0-9]{11}$/
     var phoneno = /^[1-9]{1}[0-9]{9}$/;
     return phoneno.test(inputtxt);
     },
     validName(name){
      var v = /^[a-z ,.'-]+$/i
      return v.test(name)
     },
     acccVal: function (inputtxt){
     // console.log(">>>>>>>>>>>>>>>>>>>>>>>>>>>");
     ///^[1-9]{1}[0-9]{11}$/
     var phoneno = /^[1-9]{1}[0-9]{11}$/;
     return phoneno.test(inputtxt);
     }

    }
  }
</script>
<style type="text/css">
  .focus{
    border: 1px solid red;
  }
</style>
