<template>
<div class="login">
<span>
<h1> {{msg}} </h1>
</span>
<form>
<label> <b> User Name </b> </label> 
<br>
<input type="text" v-model.lazy="login.userName" required >
 <br>
 <label> <b> Password </b> </label> 
<br>
<input type="text" v-model.lazy="login.password" required >
<br>
<button type="button"  v-on:click="LoginBloom()">Log-In</button>
      </form>
</div>
</template>
<script>
export default {
  name: 'Login',
  data: function(){
    return {
          msg:"Login Here for Bloom Gift Cards",
          id: this.$route.params.myid,
          login:{
             "userName":"",
             "password": ""
             
          },
          error:[]
      }
  },
  methods:{
      LoginBloom: function(){
         console.log(this.$route)
    console.log(this.$route.params.myid)
          let validLoginBloom = this.ValidateLogin()
      //     if(localStorage){
      //     localStorage.setItem("login"+this.login.id, JSON.stringify(this.login))
      // }
      if(validLoginBloom){
//if(this.login.userName != "" && this.login.password!=""){
              this.$http.get("http://localhost:3000/login"+'/'+ this.id)
              .then(res=>{
                  console.log(res.data)
              })
          }else {
              console.log("Incorrect Credientials")
          }
      
      },
       ValidateLogin: function(){
     console.log("Validating....");
     if(this.login.id == 0){
       this.error.push("Id must be non zero")
       return false
     }
     return true
       }
  }
}
</script>