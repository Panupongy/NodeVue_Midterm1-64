<template>
  <div>
    <h1>Cola</h1>
    <p>อันดับ: {{ userId }}</p>
    <p>ชื่อ Cola {{ user.name }} - {{ user.lastname }}</p>
    <p>บริษัท: {{ user.email }}</p>
    <p>สไตล์ Cola: {{ user.password }}</p>
  </div>
</template>
<script>
import UserService from "@/services/UsersService";
export default {
  data() {
    return {
      user: null,
    };
  },
  async created() {
    try {
      let userId = this.$route.params.userId;
      this.user = (await UserService.show(userId)).data;
    } catch (error) {
      console.log(error);
    }
  },
};
</script>
<style scoped>
</style>