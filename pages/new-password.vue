<template>
  <v-container class="px-10 mt-md-10">
    <div class="max-w-landing m-auto">
      <v-row justify="center">
        <v-col cols="12" md="8">
          <v-row justify="center">
            <v-col cols="12" md="6">
              <v-card  elevation="1" class="mx-auto" outlined>
                <v-row class="pa-5">
                  <v-col cols="12">
                    <img
                      class="m-auto w-6/12 md:w-6/12"
                      src="~assets/images/forgot-password-1.webp"
                      alt="forgot-password-1"
                    />
                  </v-col>
                  <v-col cols="12" class="text-center">
                    <span class="font-weight-bold">Buat Kata Sandi Baru</span><br/>
                    <span class="body-2">Silakan buat kata sandi baru untuk akun berikut <span class="primary--text">bla***@gmail.com</span></span>
                  </v-col>
                  <v-col cols="12">
                    <v-text-field
                      v-model="email"
                      :rules="email"
                      outlined
                      filled
                      required
                      placeholder="Kata Sandi Baru"
                      hide-details="auto"
                      color="primary"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12">
                    <v-text-field
                      class="mt-5"
                      v-model="code"
                      outlined
                      filled
                      required
                      placeholder="Konfirmasi Sandi"
                      hide-details="auto"
                      color="primary"
                    ></v-text-field>
                  </v-col>
                </v-row>
                <v-row justify="center" class="mb-5">
                  <v-col cols="6" md="6">
                    <v-btn depressed large block color="primary" class="text-capitalize">Simpan</v-btn>
                  </v-col>
                </v-row>
              </v-card>
            </v-col>
          </v-row>
        </v-col>
      </v-row>
    </div>
  </v-container>
</template>

<script>
export default {
  name: "ForgotPassword",
  layout: "landing",
  data(){
    return{
      email: "",
      code : ""
    }
  }

}
</script>
