<template>
  <div id="main">
    <v-expansion-panel>
      <v-expansion-panel-content v-for="(item,i) in 1" :key="i">
        <div slot="header">
          <h2>
            <v-icon>build</v-icon>&nbsp; Settings
          </h2>
          <h3 style="margin-left: 35px; margin-top: 5px">Mode: {{radios || 'null'}}</h3>
        </div>
        <v-divider></v-divider>
        <v-card>
          <v-card-text>
            <v-radio-group v-model="radios" :mandatory="false" id="radioGroup">
              <v-radio label="Multi-class" value="Multi-class"></v-radio>
              <v-radio label="Multi-label" value="Multi-label"></v-radio>
            </v-radio-group>

            <v-combobox
              v-model="chips"
              :items="items"
              label="List of Categories"
              chips
              clearable
              prepend-icon="add"
              solo
              multiple
            >
              <template slot="selection" slot-scope="data">
                <v-chip :selected="data.selected" close @input="remove(data.item)">
                  <strong>{{ data.item }}</strong>&nbsp;
                  <!-- <span>(interest)</span> -->
                </v-chip>
              </template>
            </v-combobox>
          </v-card-text>
        </v-card>
      </v-expansion-panel-content>
    </v-expansion-panel>

    <v-container fluid>
      <h2>
        <v-icon>scatter_plot</v-icon>&nbsp; Categories
      </h2>
      <v-radio-group
        v-if="radios === 'Multi-class'"
        row
        v-model="selectedRadioCategory"
        :mandatory="false"
      >
        <template v-for="(category,index) in chips">
          <v-radio :value="category" :label="category" :key="index"></v-radio>
        </template>
      </v-radio-group>
      <div v-else-if="radios === 'Multi-label'" class="checkboxes">
        <template v-for="(category,index) in chips">
          <v-checkbox :value="category" :label="category" :key="index" v-model="checkboxItems"></v-checkbox>
        </template>
        <!-- <v-checkbox class="checkboxitem" v-model="selected" label="John" value="John"></v-checkbox>
        <v-checkbox class="checkboxitem" v-model="selected" label="Jacob" value="Jacob"></v-checkbox>-->
      </div>
    </v-container>

    <v-divider></v-divider>
    <!-- <p>{{selectedRadioCategory}}</p>
    <p>{{checkboxItems}}</p>-->
    <section style="font-size: 2.5em;">{{actualContent[index]}}</section>

    <!-- <template v-for="(content,index) in contents">
      <section :key="index">{{content}}</section>
    </template>-->
    <v-btn id="btn" class="success" @click="submitData()">Submit</v-btn>
  </div>
</template>

<script>
export default {
  props: {
    contents: Array
  },
  data() {
    return {
      radios: "Multi-class",
      index: 0,
      actualContent: [],
      selectedRadioCategory: "",
      checkboxItems: [],
      chips: [
        "Programming",
        "Playing video games",
        "Watching movies",
        "Sleeping"
      ],
      items: ["Streaming", "Eating"],
      selected: ["John"]
    };
  },
  watch: {
    contents: {
      immediate: true,
      handler: function() {
        this.index = 0;
        this.actualContent = [];
        this.parser(this.contents, "$");
      }
    }
  },
  methods: {
    remove(item) {
      this.chips.splice(this.chips.indexOf(item), 1);
      this.chips = [...this.chips];
    },
    submitData() {
      this.index += 1;
      if (this.index === this.actualContent.length - 1) {
        alert("Reached end of file");
        return;
      }
    },
    parser(data, delimiter) {
      // var output = [];
      // var temp = "";
      // temp = data.replace(/(\r\n)+/g, "\r\n").split("\r\n");
      // temp = temp.join("");
      // output = temp.split(delimiter);

      // return output;
      this.actualContent = data.split(delimiter);
    }
  }
};
</script>

<style scoped>
#main {
  height: 100vh;
}
#radioGroup {
  padding: 0 20px;
}
.checkboxes {
  display: flex;
  flex-direction: row;
}
.checkboxes > * {
  margin-right: 15px !important;
  flex-grow: 0 !important;
}

#btn {
  margin: 20px auto;
  display: block;
}
</style>

