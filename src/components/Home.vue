<template>
<div>
	<h1 v-if='user'> Hello , {{user.name}}</h1>
	<h1 v-if='!user'> Hello </h1>

</div>
</template>
<script>
//import axios from  'axios'
export default{
	name:'Home',
	props:['user'],
}
</script>