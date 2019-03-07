<template>
  <v-flex xs12 id="uploadField" class="text-xs-center text-sm-center text-md-center text-lg-center">
    <v-text-field
      label="Upload File"
      @click="pickFile"
      v-model="fileName"
      prepend-icon="attach_file"
    ></v-text-field>
    <input type="file" style="display: none" ref="image" accept="text/*" @change="loadTextFromFile">
  </v-flex>
</template>

<script>
export default {
  data() {
    return {
      fileName: ""
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

.container {
  background-color: #f3f3f3;
}
#uploadField {
  /* width: 500px !important; */
  margin: 0 auto;
}
</style>
