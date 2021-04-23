<template>
 <div class="container">   
    <div class="row">
      <div class="col-md-6 offset-md-3">
        <!-- Sign Up form -->
        <form action="" @submit.prevent="handleSubmit" class="Signup">
          <h3>Sign In  Now!!!</h3>
          <ul v-if='error' class="bg-danger">
            <li v-for='(er,errorind) in error' v-bind:key='errorind'>{{er[0]}}</li>
          </ul>
          <div class="form-group">
              <label for="email">Email</label>
            <input type="text" class="form-control" placeholder="Enter Email" v-model='email'>
          </div>      
          <div class="form-group">
              <label for="psw">Password</label>
            <input type="password" class="form-control" placeholder="Enter Password"  v-model='password'> 
          </div>   
          
          
          <button type="submit" class="btn btn-success">SignIn</button>
          <div class="form-group">
            <p class="not-yet">Register an account? <a href="/register">Register</a></p>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
import axios from  'axios'
export default{
	name:'Login',
	data(){
		return {
			password:'',
			email:'',
      error:null,
		}
	},
	methods:{
		async handleSubmit(){
		const response = await axios.post('signin',{email:this.email,password:this.password
		});
		console.log(response);

   if (response.data.error) {
    this.error=response.data.error;
   }else{
    localStorage.setItem('token',response.data.access_token);
    location.href='/';
    //this.$router.push('/');
   }
		
		}
	}
}
</script>


