<template>
  <v-container class="px-10 mt-md-10">
    <div class="max-w-landing m-auto">
      <v-row justify="center">
        <v-col cols="12" md="8">
          <v-row align="center" justify="center">
            <v-col cols="12" sm="6" class="mb-5">
              <v-alert
                dense
                prominent
                :value="alertAttribute.show"
                :type="alertAttribute.type"
                border="left"
                elevation="2"
                class="top-right"
                transition="slide-x-reverse-transition">
                <b>{{alertAttribute.title}}</b><br/>
                {{alertAttribute.body}}
              </v-alert>
              <v-card  elevation="1" class="mx-auto" outlined>
                  <v-row class="mt-5">
                  <v-col cols="12" class="px-8">
                    <v-text-field
                      v-model="email"
                      :rules="rules.email"
                      outlined
                      filled
                      required
                      placeholder="Email"
                      hide-details="auto"
                      color="primary"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" class="px-8">
                    <v-text-field
                      v-model="fullname"
                      :rules="rules.fullname"
                      outlined
                      filled
                      required
                      placeholder="Nama Lengkap"
                      hide-details="auto"
                      color="primary"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" class="px-8">
                    <v-text-field
                      v-model="username"
                      :rules="rules.username"
                      outlined
                      filled
                      required
                      placeholder="Nama Pengguna"
                      hide-details="auto"
                      color="primary"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" class="px-8">
                    <v-text-field
                      v-model="password"
                      :rules="rules.password"
                      outlined
                      required
                      filled
                      type="password"
                      placeholder="Kata Sandi"
                      hide-details="auto"
                    ></v-text-field>
                  </v-col>
                </v-row>
                <v-row justify="center" class="mt-10">
                  <v-col cols="6" sm="6">
                    <v-btn @click="userRegister" depressed large block color="primary">Daftar</v-btn>
                  </v-col>
                </v-row>
                <v-row justify="center" class="mb-5">
                  <v-col class="px-8 text-center text-sm-body-2 .text-md-caption mt-5">
                    Sudah punya akun?
                    <nuxt-link to="/login" class="primary--text">Masuk disini</nuxt-link>
                  </v-col>
                </v-row>
              </v-card>
            </v-col>
            <v-col>
              <img
                class="m-auto float-sm-right md:w-11/12"
                src="~assets/images/register.webp"
                alt="register"
              />
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </div>
  </v-container>
</template>
<script>
export default {
  name: "Login",
  layout: "landing",
  data() {
    return {
      email:"",
      fullname:"",
      username:"",
      password:"",
      rules: {
        fullname: [
          val => val.length <= 20 || `Max 20 characters!`,
        ],
        username: [
          val => val.includes(" ") == false || `No spaces allowed`,
        ],
        email: [
          val => {
            if(val.length > 0) {
              const pattern = /^(([^<>()[\]\\.,;:\s@"]+(\.[^<>()[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
              return pattern.test(val) || 'Invalid e-mail.';
            } else {
              return true
            }
          }
        ],
        password: [
          val => val.length >= 6 || `Min 6 characters!`,
        ],
      },
      alertAttribute:{
        show:false,
        type:"success",
        title:"",
        body:"",
      }
    };
  },
  methods:{
    async userRegister(){
      const payload = {
        username: this.username,
        name: this.fullname,
        email: this.email,
        password: this.password,
        role:"operator"
      }
      this.$api.$post("auth/register", payload)
        .then(res => {
          if(res.code == 200){
            this.alertAttribute= {
              show:true,
              type:"success",
              title:"Success",
              body:res.message
            }
            setTimeout(() => this.alertAttribute.show = false, 6000)
            this.$router.push({ path: `/login`})
            this.resetForm()
          }
        })
        .catch(err => {
          this.alertAttribute= {
            show:true,
            type:"warning",
            title:"Failed",
            body:err.response.data.message
          }
          setTimeout(() => this.alertAttribute.show = false, 6000)
          return err
        })
    },
    resetForm(){
      this.email=""
      this.fullname=""
      this.username=""
      this.password=""
    },
  }
};
</script>

<style scoped>
.top-right{
  position: fixed;
  top: 20px;
  right: 20px;
  max-width:70%;
  z-index:100
}
</style>
