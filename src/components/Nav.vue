<template>
 <nav class="navbar navbar-expand-lg navbar-dark bg-primary">
  <div class="container-fluid">
    <a class="navbar-brand" href="#"></a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <li class="nav-item" v-if='user'>
          <router-link to='/' class="nav-link active" aria-current="page" href="#">Home</router-link>
        </li>
      </ul>
      <form class="d-flex" v-if='!user'>
        <router-link to='/login' class="btn btn-dark bg-primary m-2" >login</router-link>
      </form>
      <form class="d-flex" v-if='!user'>
        <router-link to='/register' class="btn btn-dark bg-primary">Register</router-link>
      </form>
      <form class="d-flex" v-if='user'>
        <a href='javascript:void(0)' @click='handleClick' class="btn btn-dark bg-primary">Logout</a>
      </form>
    </div>
  </div>
</nav>
</template>
<script>
export default{
	name:'Nav',
	props:['user'],
	methods:{
    async handleClick(){
    // const response = await axios.post('signout');
    // console.log(response);
    localStorage.removeItem('token');
    this.$router.push('/login');
    }
  }
}
</script>