<template>
  <v-layout row justify-center id="main">
    <v-dialog :disabled="state" v-model="dialog" persistent max-width="600px">
      <v-btn :disabled="state" slot="activator" color="primary">Initialize Project</v-btn>
      <v-card>
        <v-card-title>
          <span class="headline">Project Profile</span>
        </v-card-title>
        <v-card-text>
          <v-container grid-list-md>
            <v-layout wrap>
              <v-flex xs12>
                <v-text-field label="Project Name" required></v-text-field>
              </v-flex>
              <v-flex xs12>
                <v-flex
                  xs12
                  id="uploadField"
                  class="text-xs-center text-sm-center text-md-center text-lg-center"
                >
                  <v-text-field
                    label="Upload File"
                    @click="pickFile"
                    v-model="fileName"
                    prepend-icon="attach_file"
                  ></v-text-field>
                  <input
                    type="file"
                    style="display: none"
                    ref="image"
                    accept="text/*"
                    @change="loadTextFromFile"
                  >
                </v-flex>
              </v-flex>
              <v-flex xs12>
                <v-textarea solo name label="File Description"></v-textarea>
              </v-flex>
            </v-layout>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" flat @click="dialog = false">Close</v-btn>
          <v-btn class="success" flat @click="dialog = false">Save</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-layout>
</template>

<script>
// import FileUpload from "../components/FileUpload.vue";
export default {
  props: {
    state: Boolean
  },
  // components: {
  //   FileUpload
  // },
  data() {
    return {
      dialog: false,
      fileName: "",
      fileDescription: ""
    };
  },
  methods: {
    pickFile() {
      this.$refs.image.click();
    },
    loadTextFromFile(ev) {
      const file = ev.target.files[0];
      const temp = ev.target.files;
      const reader = new FileReader();

      this.fileName = temp[0].name;
      reader.onload = e => this.$emit("load", e.target.result);
      reader.readAsText(file);
      // reader.readAsText(file)
    }
  }
};
</script>

<style scoped>
@import "https://fonts.googleapis.com/css?family=Material+Icons";
#uploadField {
  /* width: 500px !important; */
  margin: 0 auto;
}
/* #main {
  background-color: #f3f3f3;
} */
</style>

