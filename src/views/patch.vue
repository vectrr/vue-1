<template>
  <div data-v-320224c2="" data-v-40b8d964="" data-v-35ea163e="" style="" id="div1" >
      <router-link :to="'/'">
  <md-button class="md-raised md-primary" >back</md-button>
      </router-link>

    <md-field>
      <label>Name  </label>
      <md-input v-model="name" ></md-input>
    </md-field>

    <md-field>
      <label>Email</label>
      <md-input type="email" v-model="email"></md-input>
    </md-field>
    <md-field>
      <label>Occupation</label>
      <md-input v-model="occupation"></md-input>
    </md-field>

    <md-field>
      <label>Bio</label>
      <md-textarea v-model="bio" md-autogrow></md-textarea>
    </md-field>
    <md-button class="md-raised md-primary" v-on:click="submit">Submit</md-button>


  </div>
</template>



<script>
import axios from "axios"
export default {
    props: ['postId','postName','postEmail','postBio','postOccupation'],

    data() {
  return {
     name:this.postName,
     email:this.postEmail,
     occupation:this.postOccupation,
     bio:this.postBio,
  }
},

      methods: {
 validateEmail: function(email) {
  const re = /^(([^<>()[\]\\.,;:\s@\"]+(\.[^<>()[\]\\.,;:\s@\"]+)*)|(\".+\"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;  // eslint-disable-line
  return re.test(email);
},
    submit: function () {
      if( !this.name && !this.occupation && !this.bio && !this.email){
        alert("The form is empty")
         }else if(!this.validateEmail(this.email)){
      alert("invalid email")
         }else{

  
        axios.patch('https://ti-react-test.herokuapp.com/users/' + this.postId, { 
         name: this.name , 
         occupation: this.occupation, 
         bio: this.bio, 
         email: this.email,
         _method: 'patch'   
    })
    .then(function (response) {
        // this.first=alerttrue

         console.log(response.statusText);
         if(response.statusText=="OK"){
             alert("edited successfully")
         }
    })
    .catch(function (error) {
         console.log(error);   
          alert("Error please make sure you have filled the form correctly")         
    });
   
      }
    }
  },
  

}
</script>
<style>
#div1{
width: 90%; max-width: 700px; padding: 22px; margin-top:77px;margin-right: auto; margin-left: auto;  box-shadow: 0px 8px 22px #00000036;
}
</style>
