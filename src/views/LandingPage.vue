<template>
  <div class="tw-bg-[#000]">
    <div
      class="header tw-fixed tw-top-0 tw-bg-[#111] tw-w-full tw-border-b-2 tw-h-[60px] tw-border-solid tw-border-[#333]"
    >
      <div class="tw-flex tw-justify-between tw-h-full">
        <div class="tw-flex tw-items-center tw-h-full">
          <div class="tw-mx-4">
            <h3 class="tw-text-white tw-text-xl tw-font-medium">BlogBrew</h3>
          </div>
        </div>
        <div class="tw-flex tw-items-center tw-h-full tw-mx-4">
          <div class="tw-flex">
            <!-- <div class="button border-gradient border-gradient-purple">
              Sign in
            </div> -->
            <div
              @click="logIn"
              class="tw-text-white tw-px-4 tw-py-2 tw-mr-4 tw-cursor-pointer tw-rounded"
            >
              <h4 class="tw-font-medium">Log in</h4>
            </div>
            <div
              @click="signUp"
              class="tw-bg-[#0070f3] hover:tw-bg-[#3291ff] tw-text-white tw-px-4 tw-py-2 tw-cursor-pointer tw-rounded"
            >
              <h4 class="tw-font-medium">Sign up</h4>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- section 1 -->
    <div class="tw-h-screen">
      <div class="tw-flex tw-justify-center tw-h-full tw-items-center">
        <div class="tw-px-4">
          <h1 class="boujee-text tw-text-center tw-font-medium">
            Craft. Publish. Inspire.
          </h1>
          <div class="tw-flex tw-justify-center tw-mt-6 md:tw-mt-12">
            <p
              class="tw-text-white tw-text-center tw-text-xl md:tw-text-3xl tw-max-w-[800px]"
            >
              Empower your voice. Effortless blogging, boundless stories. Start
              sharing your world now.
            </p>
          </div>
          <div class="tw-flex tw-justify-center tw-mt-12">
            <div
              @click="signUp"
              class="tw-cursor-pointer tw-text-white tw-bg-[#0070f3] hover:tw-bg-[#3291ff] tw-rounded-lg md:tw-px-6 tw-px-4 tw-py-2 md:tw-py-3"
            >
              <h3 class="md:tw-text-lg tw-font-medium">Get started</h3>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="tw-min-h-screen tw-pt-[60px] tw-mb-8">
      <div class="tw-w-full tw-text-center md:tw-mt-[100px]">
        <h2 class="tw-text-white tw-text-4xl md:tw-text-6xl tw-font-medium">
          What <span class="tw-text-[#0070f3]">you get?</span>
        </h2>
      </div>
      <div class="tw-mt-20 md:tw-px-[100px] tw-px-[20px]">
        <v-row>
          <v-col cols="12" lg="3" md="6">
            <div
              class="tw-bg-[#222] md:tw-min-h-[400px] tw-text-white tw-rounded-lg tw-p-8"
            >
              <div class="logo">
                <img src="../assets/Logo/edit.svg" alt="" />
              </div>
              <div>
                <h3 class="tw-text-3xl tw-my-6">Create and Manage Blogs</h3>
              </div>
              <div>
                <p class="tw-text-xl">
                  Effortlessly create, edit, and archive blogs through our
                  intuitive user interface, giving you complete control over
                  your content.
                </p>
              </div>
            </div>
          </v-col>
          <v-col cols="12" lg="3" md="6">
            <div
              class="tw-bg-[#222] md:tw-min-h-[400px] tw-text-white tw-rounded-lg tw-p-8"
            >
              <div class="logo">
                <img src="../assets/Logo/realTime.svg" alt="" />
              </div>
              <div>
                <h3 class="tw-text-3xl tw-my-6">Real-time Engagement</h3>
              </div>
              <div>
                <p class="tw-text-xl">
                  Keep your audience engaged with live tracking features,
                  allowing readers to follow updates and stay connected with
                  your content in real-time.
                </p>
              </div>
            </div>
          </v-col>
          <v-col cols="12" lg="3" md="6">
            <div
              class="tw-bg-[#222] md:tw-min-h-[400px] tw-text-white tw-rounded-lg tw-p-8"
            >
              <div class="logo">
                <img src="../assets/Logo/comment.svg" alt="" />
              </div>
              <div>
                <h3 class="tw-text-3xl tw-my-6">
                  Streamlined Comment Management
                </h3>
              </div>
              <div>
                <p class="tw-text-xl">
                  Administer comments efficiently through the Admin Panel,
                  ensuring a safe and engaging environment for your readers.
                </p>
              </div>
            </div>
          </v-col>
          <v-col cols="12" lg="3" md="6">
            <div
              class="tw-bg-[#222] md:tw-min-h-[400px] tw-text-white tw-rounded-lg tw-p-8"
            >
              <div class="logo">
                <img src="../assets/Logo/insight.svg" alt="" />
              </div>
              <div>
                <h3 class="tw-text-3xl tw-my-6">Insightful Statistics</h3>
              </div>
              <div>
                <p class="tw-text-xl">
                  Track the performance of your blogs with detailed stats on
                  likes, views, and more, helping you understand and enhance
                  your impact.
                </p>
              </div>
            </div>
          </v-col>
        </v-row>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  methods: {
    logIn() {
      this.$router.push("/login");
    },
    signUp() {
      this.$router.push("/signup");
    },
  },
};
</script>
<style scoped>
.button {
  /* background: none; */
  color: #fff;
  text-decoration: inherit;
  font-family: system-ui;
  font-size: 1rem;
  padding: 0.5rem 1rem;
  border-radius: 8px !important;
}
.border-gradient {
  border: 10px solid;
  border-image-slice: 1;
  border-width: 3px;
  border-radius: 8px;
}
.border-gradient-purple {
  border-image-source: linear-gradient(to left, #743ad5, #d53a9d);
}
.boujee-text {
  --bg-size: 400%;
  --color-one: hsl(15 90% 55%);
  --color-two: hsl(40 95% 55%);
  font-size: clamp(3rem, 25vmin, 8rem);
  background: linear-gradient(90deg, #c084f9, #fbcb8c, #f992ae, #c084f9) 0 0 /
    var(--bg-size) 100%;
  color: transparent;
  background-clip: text;
}

@media (prefers-reduced-motion: no-preference) {
  .boujee-text {
    animation: move-bg 10s linear infinite;
  }
  @keyframes move-bg {
    to {
      background-position: var(--bg-size) 0;
    }
  }
}
@media screen and (max-width: 600px) {
  .boujee-text {
    font-size: clamp(
      2.5rem,
      5vmin,
      3rem
    ); /* Further adjust font size for smaller screens */
  }
}
/* ===== Scrollbar CSS ===== */
/* Firefox */
* {
  scrollbar-width: auto;
  scrollbar-color: #111 #333333;
}

/* Chrome, Edge, and Safari */
*::-webkit-scrollbar {
  width: 16px;
}

*::-webkit-scrollbar-track {
  background: #333333;
}

*::-webkit-scrollbar-thumb {
  background-color: #111;
  border-radius: 10px;
  border: 0px solid #ffffff;
}
</style>