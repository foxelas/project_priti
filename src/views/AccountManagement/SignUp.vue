<template>
	<div
		style="max-width: 600px; margin: auto;"
    	class="grey lighten-3">

    	<v-toolbar dark color="indigo lighten-2" class="mt-4" >
    	  <h2>SIGN UP</h2>
    	</v-toolbar>

    	<v-card>
    	  <v-container
    	  	fluid
        	grid-list-lg>
	    	  <div>
	    	  	<v-form 
	    	  		v-model="valid">
	    	  		<v-text-field
				      v-model="name"
				      :rules="nameRules"
				      label="Name"
				      required
				    ></v-text-field>
				    <v-text-field
				      v-model="email"
				      :rules="emailRules"
				      label="E-mail"
				      required
				    ></v-text-field>
				    <v-text-field
				      v-model="password"
				      :rules="passwordRules"
				      :counter="10"
				      label="Password"
				      required
							input type="password" id="myInput"
				    ></v-text-field>
				    <v-text-field
				      v-model="confirmPassword"
				      :rules="passwordRules"
				      :counter="10"
				      label="Confirm Password"
				      required
							input type="password"  id="retypePassword"
				    ></v-text-field>
						<v-checkbox type="checkbox" onclick="showPassword()">Show Password</v-checkbox>					
				 </v-form>
				 <v-select
		          :items="items"
		          label="Use as">     	
		         </v-select>
		         <v-checkbox label="I agree with the condition terms"></v-checkbox>
				<v-btn  color="indigo"> Upload your ID card</v-btn>
				</div>
			<v-layout column wrap>
			  <v-flex xs12 sm6>
			    <v-btn color="success" v-on:click="SignUp">Sign Up</v-btn>
			  </v-flex>
			</v-layout>
    	  </v-container>
    	</v-card>
		
	</div>

</template>

<script>
import firebase from "firebase"
  export default {
    data: () => ({
      valid: false,
      name: '',
      nameRules: [
        v => !!v || 'Name is required',
      ],
      email: '',
      emailRules: [
        v => !!v || 'E-mail is required',
        v => /.+@.+/.test(v) || 'E-mail must be valid'
      ],
      password: '',
      passwordRules: [
        v => !!v || 'Password is required',
        v => v.length <= 10 || 'Password must be less than 10 characters'
      ],
      confirmPassword:'',
      items: ['','Student', 'Teacher'],
		 
		 name:"",
  data(){
    return{
      email:null,
      password: null
    }
  },

		}),
	  methods: {
			showPassword: function() {
					var x = document.getElementById("retypePassword");
					if (x.type === "password") {
					x.type = "text";
					} else {
					x.type = "password";
					}
				},
		SignUp: function(){
			console.log();
			firebase.auth().createUserWithEmailAndPassword(this.email, this.password)
			.then(user =>{
					alert('Create account: ',this.email);
					this.$router.push('/');
					console.log(user);
        })
        .catch(error =>{
            alert(error.message);
        });
        }
			}
	}
</script>