<template>
  <v-app>
    <v-toolbar id="toolbar" absolute app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Data</span>
        <span class="font-weight-light">&nbsp;Labeler</span>
      </v-toolbar-title>&nbsp; &nbsp;
      <!-- <Logo></Logo> -->
    </v-toolbar>

    <v-content>
      <!-- <textarea rows="10" v-model="text"></textarea>
      <FileUpload @load="text = $event"></FileUpload>-->
      <TabsContainer></TabsContainer>
    </v-content>
  </v-app>
</template>

<script>
import TabsContainer from "./components/TabsContainer.vue";

//import Logo from "./components/Logo.vue";

export default {
  name: "App",
  components: {
    TabsContainer
  },
  data() {
    return {
      text: ""
    };
  }
};
</script>

<style>
.addHighlight {
  background-color: rgb(229, 255, 0) !important;
}
#toolbar {
  display: flex;
  justify-content: center;
}
section {
  padding: 60px 250px;
  background-color: #eee;
  font-size: 1.6rem;
}
</style>

