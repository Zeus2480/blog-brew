<template>
  <div>
    <v-overlay :value="overlay" opacity=".5">
      <div class="text-center">
        <v-progress-circular
          indeterminate
          color="white"
          size="50"
        ></v-progress-circular>
      </div>
    </v-overlay>
    <v-snackbar v-model="snackbar" :timeout="7000" :color="errorColor" absolute>
      {{ text }}

      <template v-slot:action="{ attrs }">
        <v-btn color="white" text v-bind="attrs" @click="snackbar = false">
          Close
        </v-btn>
      </template>
    </v-snackbar>
    <div class="tw-min-h-screen tw-min-w-screen tw-flex">
      <div
        class="logo-screen tw-w-2/5 tw-hidden tw-bg-white md:tw-flex tw-justify-center tw-items-center"
      >
        <div class="">
          <img src="../assets/Images/loginPage.svg" alt="" />
        </div>
      </div>
      <div
        class="form tw-w-full tw-bg-[#ECEDF0] md:tw-w-3/5 tw-px-5 md:tw-px-24 tw-flex tw-justify-center md:tw-pt-[100px] tw-py-6"
      >
        <div class="tw-w-full md:tw-w-[80%]">
          <div class="tw-flex tw-flex-row-reverse">
            <v-btn
              color="black"
              large
              dark
              @click="$router.push('/signup')"
              >Sign up</v-btn
            >
          </div>
          <div>
            <h1 class="tw-text-5xl tw-my-4 tw-text-black tw-font-semibold">
              Login into your BlogBrew <br />
              Account <span class="tw-text-[#0D99FF] tw-text-6xl">.</span>
            </h1>
          </div>
          <!-- <div class="tw-flex tw-mb-4">
                <img
                  src="../assets/Logo/WebookLogo.svg"
                  class="tw-h-8 tw-my-auto"
                  alt=""
                />
                <div class="tw-my-auto tw-mx-6">
                  <h1 class="tw-font-medium tw-text-xl">
                    Create Your Webook Account
                  </h1>
                </div>
              </div> -->

          <!-- <div>
                <v-progress-linear
                  :value="progress"
                  color="black"
                  rounded
                ></v-progress-linear>
                <div class="tw-flex tw-flex-row-reverse tw-mt-1 tw-mb-4">
                  <p class="tw-opacity-75">{{ whichStep }}</p>
                </div>
              </div> -->

          <!-- //Form -->
          <v-row>
            <v-col cols="12">
              <v-text-field
                v-model="inputEmail"
                ref="inputEmail"
                label="Email"
                outlined
                :rules="[() => !!inputEmail || 'This field is required']"
              ></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-text-field
                v-model="inputPassword"
                ref="inputPassword"
                :append-icon="showPassword ? 'mdi-eye' : 'mdi-eye-off'"
                :type="showPassword ? 'text' : 'password'"
                name="input-10-1"
                label="Password"
                :rules="[
                  () => !!inputPassword || 'This field is required',
                  () =>
                    (!!inputPassword && inputPassword.length >= 8) ||
                    'At least 8 characters',
                ]"
                hint="At least 8 characters"
                outlined
                @click:append="showPassword = !showPassword"
              ></v-text-field>
            </v-col>
            <v-col cols="12">
              <v-btn
                large
                block
                :loading="showButtonLoading"
                color="black"
                dark
                @click="login"
                >Login</v-btn
              >
            </v-col>
          </v-row>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  computed: {},
  components: {},
  created() {
    // this.$router.go('/login')
  },
  data() {
    return {
      showPassword: false,
      overlay: false,
      inputEmail: "",
      inputPassword: "",
      showPasswordMessage: false,
      showEmailMessage: false,
      formIsValid: true,
      emailMessage: "ww",
      passwordMessage: "ww",
      showButtonLoading: false,
      text: "",
      errorColor: null,
      snackbar: null,
    };
  },
  methods: {
    showPasswordFunctions() {
      this.showPassword = !this.showPassword;
    },
    reload() {},
    validate() {
      this.$refs.inputEmail.validate(true);
      this.$refs.inputPassword.validate(true);
      this.showPasswordMessage = false;
      this.showEmailMessage = false;
      this.formIsValid = true;
      if (this.inputPassword == "") {
        this.passwordMessage = "Required";
        this.showPasswordMessage = true;
        this.formIsValid = false;
      }
      if (this.inputEmail == "") {
        this.emailMessage = "Required";
        this.showEmailMessage = true;
        this.formIsValid = false;
      }
    },
    login() {
      this.showButtonLoading = true;
      this.validate();
      if (this.formIsValid) {
        axios
          .post("/login", {
            email: this.inputEmail,
            password: this.inputPassword,
          })
          .then((res) => {
            if (res.status === 200) {
              localStorage.setItem("token", res.data.access_token);
              this.$router.push("/dashboard/post");
            } else {
              this.text = "Invalid Credentials";
              this.errorColor = "red darken-4";
              this.snackbar = true;
            }
          })
          .catch((err) => {
            console.log(err);
            this.text = "Invalid Credentials";
            this.errorColor = "red darken-4";
            this.snackbar = true;
            // this.passwordMessage = "Invalid Credentials";
            // this.showPasswordMessage = true;
          })
          .finally(() => {
            this.showButtonLoading = false;
          });
      } else {
        this.showButtonLoading = false;
      }
    },
  },
};
</script>
<style scoped>
.opacity {
  opacity: 0;
}
</style>
