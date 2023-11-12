<template>
  <div>
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
            <v-btn large dark @click="$router.push('/login')">Sign in</v-btn>
          </div>
          <div>
            <h1 class="tw-text-xl tw-font-semibold">
              Step {{ !isStepOneCompleted ? "01" : "02" }}/02
            </h1>
            <h1 class="tw-text-5xl tw-my-4 tw-text-black tw-font-semibold">
              Create Your BlogBrew <br />
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
          <user-details
            v-if="!isStepOneCompleted"
            @userData="userData"
          ></user-details>
          <user-domain
            :userData="formData"
            v-if="isStepOneCompleted"
          ></user-domain>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import UserDetails from "../components/UserDetails.vue";
import UserDOmain from "../components/UserDomian.vue";
export default {
  computed: {
    whichStep() {
      return `Step ${this.step} of 2`;
    },
  },
  components: {
    "user-details": UserDetails,
    "user-domain": UserDOmain,
  },
  data() {
    return {
      progress: 50,
      step: 1,
      isStepOneCompleted: false,
      formData: null,
      domainName: null,
    };
  },
  methods: {
    userData(data) {
      //  console.log(123);
      this.formData = data;
      this.progress = 100;
      this.step = 2;
      this.isStepOneCompleted = true;
    },

    showPasswordFunctions() {
      this.showPassword = !this.showPassword;
    },
  },
};
</script>
<style scoped>
.opacity {
  opacity: 0;
}
</style>
