<template>
<div>
    <h1>สร้างประเภท</h1>
    <form v-on:submit.prevent = "createUser">
        <p>ชื่อ Cola: <input type="text" v-model="user.name"></p>
        <p>รส: <input type="text" v-model="user.lastname"></p>
        <p>บริษัท: <input type="text" v-model="user.email"></p>
        <p>สไตล์ Cola: <input type="text" v-model="user.password"></p>
        <p><button type="submit">create user</button></p>
    </form>
    <hr>
    <div>
        <p>ชื่อ Cola: {{user.name}}</p>
        <p>รส: {{user.lastname}}</p>
        <p>บริษัท: {{user.email}}</p>
        <p>สไตล์ Cola: {{user.password}}</p>
    </div>
</div>
</template>
<script>
import UsersService from '@/services/UsersService'

export default {
    data(){
        return{
            user:{
                name: '',
                lastname: '',
                email: '',
                password: '',
                status: 'active'
            }
        }
    },
    methods:{
        async createUser(){
            try{
                await UsersService.post(this.user)
                this.$router.push({
                    name: 'users'
                })
            }catch(error){
                console.log(error)
            }
        }
    }    
}
</script>
<style scoped>


</style>