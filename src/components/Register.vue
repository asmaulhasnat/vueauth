<template>
 <div class="container">   
    <div class="row">
      <div class="col-md-6 offset-md-3">
        <!-- Sign Up form -->
        <form action="" @submit.prevent="handleSubmit" class="Signup">
          <h3>Sign Up Now!!!</h3>
          <div class="form-group">
              <label for="name">Name</label>
            <input type="text" class="form-control" placeholder="Name" v-model='name' required>
          </div>
          <div class="form-group">
              <label for="email">Email</label>
            <input type="text" class="form-control" placeholder="Enter Email" v-model='email' required>
          </div>      
          <div class="form-group">
              <label for="psw">Password</label>
            <input type="password" class="form-control" placeholder="Enter Password"  v-model='password' required> 
          </div>   
          <div class="form-group">
            <label for="psw-repeat">Confirm Password</label>
            <input type="password" class="form-control" placeholder="Repeat Password"  v-model='password_confirmation' required>
          </div>
          
          <button type="submit" class="btn btn-success">Signup</button>
          <div class="form-group">
            <p class="not-yet">Already have an account? <a href="/login">Login</a></p>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
import axios from  'axios'
export default{
	name:'Register',
	data(){
		return {
			name:'',
			email:'',
			password:'',
			password_confirmation:'',
		}
	},
	methods:{
		async handleSubmit(){
		const response = await axios.post('signup',{
			name:this.name,email:this.email,password:this.password,password_confirmation:this.password_confirmation
		});
		console.log(response);
		this.$router.push('/login');
		}
	}
}
</script>

