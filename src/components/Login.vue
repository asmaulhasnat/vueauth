<template>
 <div class="container">   
    <div class="row">
      <div class="col-md-6 offset-md-3">
        <!-- Sign Up form -->
        <form action="" @submit.prevent="handleSubmit" class="Signup">
          <h3>Sign In  Now!!!</h3>
          
          <div class="form-group">
              <label for="email">Email</label>
            <input type="text" class="form-control" placeholder="Enter Email" v-model='email' required>
          </div>      
          <div class="form-group">
              <label for="psw">Password</label>
            <input type="password" class="form-control" placeholder="Enter Password"  v-model='password' required> 
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
		}
	},
	methods:{
		async handleSubmit(){
		const response = await axios.post('signin',{email:this.email,password:this.password
		});
		console.log(response);
		localStorage.setItem('token',response.data.access_token);
		this.$router.push('/');
		}
	}
}
</script>


