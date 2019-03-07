<template>
  <div>
    <!-- <file-upload @load="text = $event"></file-upload> -->
    <v-container>
      <v-layout wrap align-center justify-center>
        <v-flex xs2>
          <v-text-field label="Your Name" required id="textfield" v-model="labelerName"></v-text-field>
        </v-flex>
      </v-layout>
    </v-container>

    <file-modal :state="buttonState()" @load="(text = $event); outputText()"></file-modal>
    <file-list :state="buttonState()"></file-list>
    <v-tabs
      v-model="active_tab"
      id="tabs"
      color="white"
      light
      grow
      slider-color="black"
      style="margin-top: 20px;"
    >
      <!-- <p>Active Tabasx: {{checkActive}}</p> -->
      <!-- <p>active: {{tabs[active_tab].name}}</p> -->
      <v-tab
        id="tab"
        v-for="tab in tabs"
        :key="tab.index"
        active-class="black white--text"
      >{{tab.name}}</v-tab>
      <v-tab-item>
        <v-card flat>
          <v-card-text>
            <CategoricalTab :contents="catText"></CategoricalTab>
          </v-card-text>
        </v-card>
      </v-tab-item>
      <v-tab-item>
        <v-card flat>
          <v-card-text>
            <ContextualTab :contents="conText"></ContextualTab>
          </v-card-text>
        </v-card>
      </v-tab-item>
    </v-tabs>
  </div>
</template>

<script>
import CategoricalTab from "../components/CategoricalTab.vue";
import ContextualTab from "../components/ContextualTab.vue";
//import FileUpload from "../components/FileUpload.vue";
import FileModal from "../components/FileModal.vue";
import FileList from "../components/FileList.vue";
export default {
  components: {
    CategoricalTab,
    ContextualTab,
    // FileUpload,
    FileModal,
    FileList
  },
  data() {
    return {
      text: "",
      labelerName: "",
      catText: "",
      conText: "",
      active_tab: 0,
      tabs: [
        { index: 0, name: "Categorical" },
        { index: 1, name: "Contextual" }
      ]
    };
  },
  // computed: {
  //   checkActive() {
  //     return this.tabs[this.active_tab].name;
  //   }
  // },
  methods: {
    outputText() {
      if (this.tabs[this.active_tab].name === "Categorical") {
        this.catText = this.text;
      } else if (this.tabs[this.active_tab].name === "Contextual") {
        this.conText = this.text;
      }
    },
    buttonState() {
      if (this.labelerName === "") {
        return true;
      } else {
        return false;
      }
    }
  }
};
</script>

<style>
.v-tabs__container {
  height: 70px !important;
}
#tab {
  text-transform: none !important;
  font-size: 1.5rem;
}
.v-card__text {
  padding: 0 !important;
}
.container {
  max-width: 100%;
}
</style>

