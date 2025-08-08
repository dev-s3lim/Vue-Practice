<template>
  <v-app-bar>
    <v-container>
      <v-row>
        <v-col class="d-flex justify-start">
          <div v-if="userRole === 'ADMIN'">
            <v-btn>회원관리</v-btn>
            <v-btn>상품관리</v-btn>
            <v-btn>주문관리</v-btn>
          </div>
        </v-col>
        <v-col class="text-center">
          <v-btn :to="'/'">JAVA SHOP</v-btn>
        </v-col>
        <v-col class="d-flex justify-end">
            <v-btn>장바구니</v-btn>
            <v-btn>상품목록</v-btn>
            <v-btn v-if ="!isLoggedin" :to="'/member/create'">회원가입</v-btn>
            <v-btn v-if ="!isLoggedin" :to="'/member/login'">로그인</v-btn>
            <v-btn v-if ="isLoggedin" @click="doLogout()">로그아웃</v-btn>
        </v-col>
      </v-row>
    </v-container>
  </v-app-bar>
</template>

<script>
export default {
  data() {
    return {
      userRole: null,
      isLoggedin: false,
    };
  },
  created() {
    const accessToken = localStorage.getItem("accessToken");
    if (accessToken) {
      this.isLoggedin = true;
    }
  },
  name: 'AppHeader',
  methods: {
    doLogout() {
      localStorage.clear();
      window.location.reload();
    }
  },
}
</script>