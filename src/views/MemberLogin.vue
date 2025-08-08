<template>
  <v-container>
    <v-row justify="center">
      <v-col cols="6">
        <v-card>
          <v-card-title class="text-center text-h5">
            <h1>로그인</h1>
          </v-card-title>
            <v-card-text>
              <v-form>
                <v-text-field label="이메일" type="email" v-model="email" prepend-icon="mdi-email" required></v-text-field>
                <v-text-field label="패스워드" type="password" v-model="password" prepend-icon="mdi-lock" required></v-text-field>
                <v-row>
                  <v-col class="text-center">
                    <v-btn color="primary" block @click="memberLogin()">
                      로그인
                    </v-btn>
                  </v-col>
                </v-row>
              </v-form>
            </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      name: "",
      email: "",
      password: "",
    }
  },
  methods: {
    async memberLogin() {
      try {
        const data = {
          email: this.email,
          password: this.password
        };
        const response = await axios.post("http://localhost:8080/member/doLogin", data);
        const accessToken = response.data.result.accessToken;
        const refreshToken = response.data.result.refreshToken;
        localStorage.setItem("accessToken", accessToken);
        localStorage.setItem("refreshToken", refreshToken);
        window.location.href = "/";
      }
      catch (e) {
        console.log(e);
        alert (e.response.data.statusMessage)
      }
    }
  },
}
</script>
