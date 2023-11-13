<template>
  <div>
    <v-snackbar v-model="snackbar">
      {{ text }}

      <template v-slot:action="{ attrs }">
        <v-btn color="pink" text v-bind="attrs" @click="snackbar = false">
          Close
        </v-btn>
      </template>
    </v-snackbar>
    <the-navbar></the-navbar>

    <v-main class="tw-bg-secondary-background tw-min-h-screen">
      <v-container class="tw-h-full tw-px-0 xl:tw-px-20">
        <div class="view-profile">
          <v-card>
            <div class="tw-p-4">
              <div class="tw-flex tw-justify-between">
                <div class="back-btn tw-flex">
                  <v-btn @click="back" icon
                    ><img src="../assets/Logo/arrow_back_black_24dp.svg" alt=""
                  /></v-btn>
                  <h1 class="tw-my-auto tw-mx-2 tw-text-xl">Create Post</h1>
                </div>
                <div class="puplish-preview">
                  <!-- <v-btn outlined color="primary">Preview</v-btn> -->
                  <v-btn
                    color="primary"
                    :loading="loading"
                    @click="publish"
                    class="tw-ml-4"
                    >Publish</v-btn
                  >
                </div>
              </div>
              <div class="form tw-mt-8 tw-px-4">
                <v-form ref="form" v-model="valid" lazy-validation>
                  <v-text-field
                    :rules="[() => !!title || 'This field is required']"
                    ref="title"
                    v-model="title"
                    label="Title"
                    required
                  ></v-text-field>

                  <v-text-field
                    ref="summary"
                    :rules="[() => !!summary || 'This field is required']"
                    v-model="summary"
                    label="Summary"
                    required
                  ></v-text-field>
                </v-form>

                <div class="tw-my-2">
                  <v-file-input
                    label="Banner image"
                    ref="inputFile"
                    filled
                    required
                    show-size
                    prepend-icon="mdi-camera"
                    accept="image/png, image/gif, image/jpeg"
                    @change="onFileSelected"
                    :rules="rules"
                    hint="File size should not exceed 500kb"
                  ></v-file-input>
                </div>
                <div class="title">
                  <v-text-field
                    v-model="inputTag"
                    label="Tags"
                    @keyup.enter="onEnter"
                  ></v-text-field>

                  <v-chip-group v-model="selection" column>
                    <v-chip
                      v-for="(tag, index) in tagsArray"
                      :value="tag"
                      :key="index"
                      link
                    >
                      {{ tag }}
                    </v-chip>
                  </v-chip-group>
                </div>
                <div class="tw-my-4">
                  <VueEditor v-model="body" />
                </div>
              </div>
            </div>
          </v-card>
        </div>
      </v-container>
    </v-main>
  </div>
</template>
<script>
import TheNav from "../Common/TheNavbar.vue";
import { VueEditor } from "vue2-editor";
import axios from "axios";
export default {
  watch: {
    selection(newValue) {
      let temp = this.tagsArray.filter((val) => {
        return val !== newValue;
      });

      this.tagsArray = temp;
    },
  },

  data() {
    return {
      isLoadingCompleted: false,
      loading: false,
      prevRoute: null,
      rules: [
        (file) => {
          if (file) {
            return (
              !file ||
              file?.size < 500000 ||
              "File size should be less than 500 KB!"
            );
          }
          return false;
        },
      ],
      inputTag: "",
      tagsArray: [],
      selection: "",
      removeValue: "",
      snackbar: false,
      title: null,
      summary: null,
      body: null,
      selectedFile: null,
      text: `Hello, I'm a snackbar`,
      valid: true,
      titleRules: [
        (v) => !!v || "Title is required",
        // (v) =>
        //    (v && v.length <= 10) || "Name must be less than 10 characters",
      ],
      summaryRules: [(v) => !!v || "Summary is required"],
    };
  },
  beforeRouteEnter(to, from, next) {
    //   this.prevRoute=from.fullPath;
    next((vm) => {
      vm.prevRoute = from.fullPath;
    });
  },
  // beforeRouteLeave(to, from, next) {
  //    let formData = new FormData();
  //    if (this.title) {
  //       formData.append("name", this.title);
  //    }
  //    if (this.summary) {
  //       formData.append("summary", this.summary);
  //    }
  //    // formData.append("excerpt", this.summary);
  //    if (this.body) {
  //       formData.append("body", this.body);
  //    }
  //    if (this.tagsArray) {
  //       formData.append("tags", JSON.stringify(this.tagsArray));
  //    }
  //    if (this.selectedFile) {
  //       formData.append("image", this.selectedFile);
  //    }
  //    axios.post(``);
  //    // if (this.isLoadingCompleted) {
  //    //    next();
  //    // } else {
  //    //    this.snackbar = true;
  //    //    this.text = `Please wait while we are saving your post`;
  //    //    next(false);
  //    // }
  // },
  created() {
    setTimeout(() => {
      this.isLoadingCompleted = true;
    }, 2000);
  },
  components: {
    "the-navbar": TheNav,
    VueEditor,
  },
  beforeMount() {
    window.addEventListener("beforeunload", this.myfun);
  },
  watcher: {
    
  },
  methods: {
    myfun() {
      // Write your business logic here
    },
    onFileSelected(event) {
      // console.log(event);
      if (event) {
        this.selectedFile = event;
      } else {
        this.selectedFile = null;
      }
    },
    back() {
      this.$router.push(`${this.prevRoute}`);
    },
    onEnter() {
      this.tagsArray.push(this.inputTag);
      this.inputTag = "";
    },
    remove() {
      //   console.log(123);
      //   console.log(this.selection);
      //   console.log(this.s);
    },
    validate() {
      this.$refs.title.validate(true);
      this.$refs.summary.validate(true);
      this.$refs.inputFile.validate(true);
      this.valid = this.$refs.form.validate();
      this.valid = true;
      if (!this.title || !this.summary || !this.body || !this.selectedFile) {
        this.valid = false;
      }
    },
    publish() {
      this.validate();
      if (this.valid) {
        this.loading = true;
        let formData = new FormData();
        formData.append("name", this.title);
        formData.append("excerpt", this.summary);
        formData.append("body", this.body);
        this.tagsArray.forEach((tag) => {
          formData.append("tags[]", tag);
        });
        formData.append("image", this.selectedFile);
        // let obj = {
        //   name: this.title,
        //   excerpt: this.summary,
        //   body: this.body,
        //   tags: this.tagsArray,
        //   image: this.selectedFile,
        // };
        // console.log(obj);
        axios
          .post("/post/create", formData, {
            headers: {
              Authorization: "Bearer " + localStorage.getItem("token"),
            },
          })
          .then((res) => {
            if (res.status === 200) {
              this.snackbar = true;
              this.text = "Post Created Successfully";
              this.$router.push(`/dashboard/post`);
            }
          })
          .catch(() => {
            this.snackbar = true;
            this.text = `File size should not exceed 500kb`;
          })
          .finally(() => {
            this.loading = false;
          });
      }
      // this.$router.push(`/`);
    },
  },
};
</script>
