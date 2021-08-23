<template>
  <div>
    <h1>Cola</h1>
    <div v-if="users.length">
      <h4>ประเภท Cola {{ users.length }}</h4>
      <p>
        <button v-on:click="navigateTo('/user/create')">
            เพิ่มประเภท Cola มี
          </button>
      </p>
      <div v-for="user in users" v-bind:key="user.id">
        <p>อันดับ: {{ user.id }}</p>
        <p>ชื่อ Cola: {{ user.name }} - {{ user.lastname }}</p>
        <p>บริษัท: {{ user.email }}</p>
        <p>สไตล์ Cola : {{ user.password }}</p>
        <p>
          <button v-on:click="navigateTo('/user/' + user.id)">
            ดูข้อมูล Cola
          </button>
          <button v-on:click="navigateTo('/user/edit/' + user.id)">
            แก้ไขข้อมูล Cola
          </button>
          <button v-on:click="deleteUser(user)">
            ลบข้อมูล Cola
          </button>
        </p>
        <hr />
      </div>
    </div>
  </div>
</template>
<script>
import UsersService from "@/services/UsersService";

export default {
  data() {
    return {
      users: [],
    };
  },
  async created() {
    try {
      this.users = (await UsersService.index()).data;
    } catch (error) {
      console.log(error);
    }
  },
  methods: {
    navigateTo(route) {
      this.$router.push(route);
    },
    async deleteUser(user){
      let result = confirm("Want to delete")
      if(result){
        try{
          await UsersService.delete(user)
          this.refreshData()
        }catch(error){
          console.log(error)
        }
      }
    },
    async refreshData(){
      this.users = (await UsersService.index()).data
    }
  },
};
</script>
<style scoped>
</style>