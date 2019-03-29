<template>
  <div id="main">
    <v-combobox
      v-model="chips"
      :items="items"
      label="List of Categories"
      chips
      clearable
      prepend-icon="add"
      solo
      multiple
      @input="insertLabel(), updateComponent()"
    >
      <template slot="selection" slot-scope="data">
        <v-chip
          :selected="data.selected"
          close
          @input="remove(data.item), alertMe(data.item), updateComponent()"
        >
          <v-avatar class="grey darken-3 white--text" v-text="(data.index)+1"></v-avatar>
          <strong>{{ data.item }}</strong>&nbsp;
          <!-- <span>(interest)</span> -->
        </v-chip>
      </template>
    </v-combobox>

    <section
      v-if="show"
      class="dataspace"
      v-html="actualContent[index]"
      style="font-size: 2.5em;"
      @click="getIndex(actualContent[index], $event)"
    ></section>

    <div id="highlight_menu" style="display:none;">
      <ul class="side-by-side">
        <li v-for="(data, index) in chips" :key="data" @click="getString(data)">
          <a href="#" :title="data" style="text-decoration: none !important; color: white">
            <!-- <img :src="icons[index]"> -->
            <span id="index_num">{{(index)+1}}</span>
          </a>
        </li>
        <!-- 
        <li id="first-menu">
          <a href="#" title="Skill" class="menuItem" @click="getString">
            <img
              src="data:image/svg+xml;utf8;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iaXNvLTg4NTktMSI/Pgo8IS0tIEdlbmVyYXRvcjogQWRvYmUgSWxsdXN0cmF0b3IgMTYuMC4wLCBTVkcgRXhwb3J0IFBsdWctSW4gLiBTVkcgVmVyc2lvbjogNi4wMCBCdWlsZCAwKSAgLS0+CjwhRE9DVFlQRSBzdmcgUFVCTElDICItLy9XM0MvL0RURCBTVkcgMS4xLy9FTiIgImh0dHA6Ly93d3cudzMub3JnL0dyYXBoaWNzL1NWRy8xLjEvRFREL3N2ZzExLmR0ZCI+CjxzdmcgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayIgdmVyc2lvbj0iMS4xIiBpZD0iQ2FwYV8xIiB4PSIwcHgiIHk9IjBweCIgd2lkdGg9IjI0cHgiIGhlaWdodD0iMjRweCIgdmlld0JveD0iMCAwIDUxMiA1MTIiIHN0eWxlPSJlbmFibGUtYmFja2dyb3VuZDpuZXcgMCAwIDUxMiA1MTI7IiB4bWw6c3BhY2U9InByZXNlcnZlIj4KPGc+Cgk8cGF0aCBkPSJNMjU2LDBDMTE0LjYwOSwwLDAsMTE0LjYwOSwwLDI1NmMwLDE0MS4zOTEsMTE0LjYwOSwyNTYsMjU2LDI1NmMxNDEuMzkxLDAsMjU2LTExNC42MDksMjU2LTI1NiAgIEM1MTIsMTE0LjYwOSwzOTcuMzkxLDAsMjU2LDB6IE0yNTYsNDcyYy0xMTkuMjk3LDAtMjE2LTk2LjcwMy0yMTYtMjE2UzEzNi43MDMsNDAsMjU2LDQwczIxNiw5Ni43MDMsMjE2LDIxNlMzNzUuMjk3LDQ3MiwyNTYsNDcyeiAgICIgZmlsbD0iIzAwMDAwMCIvPgoJPGc+CgkJPHBhdGggZD0iTTI0OS43MDMsMjAxLjI1SDE4OHYtMjVoMTkuMzEyYzYuODU5LDAsMTMuNDIyLTEuMjE5LDE5LjUtMy41OTRjNi4xNzItMi4zNzUsMTEuNDM4LTUuNjQxLDE1Ljc5Ny05Ljc5NyAgICBjNC4zNTgtNC4yMDMsNy45MjItOS4yNSwxMC41NDctMTUuMjM0YzIuNzM0LTUuOTA2LDQuMDQ3LTEyLjUsNC4wNDctMTkuNjI1SDI4NHYyNTZoLTM0LjI5N1YyMDEuMjV6IiBmaWxsPSIjMDAwMDAwIi8+Cgk8L2c+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPGc+CjwvZz4KPC9zdmc+Cg=="
            >
          </a>
        </li>
        <li id="second-menu">
          <a href="#" title="Location">
            <img
              src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAACQUlEQVRIS52VSajIURTGfy8lylAWpqRQ5lKKkISQKFZIIQllKcVKxIqFpWRMJMOKooTIEElJGZMsCFlYIKRE3+u7r/tud3g5m///3vOd853h3nM7aMsCYBUwGxhh+HvgLnAOuF5z0VFRjgGOAnMbMdwENgFvcrgSgaK9CAxqJ9iJ+AIsd1bdTHIEivxh5PyvMzkOPLP1JGADsBEIPkQyPc0kR6CUQ1k+AGsA7eVkHnAaGG6lcPNjYEqghl4zQJELfKtRJpHciDJZGDc+JTjitOVT/5vtvDewF1jr9SlgJ/Db68NudGrXVb8Q5AtgvBczgQf+3wdsTzLZD+zw3gzgvv9fAhMCNs3gG9DPygGA1hL1YlhC8DGqfX/gq/WykW2npAQCCSzR9/t/EMjHwBLB8yi9scDrHpZI2FfGyoeOcTaDq8Ai61YDZ/3farKwZ4yVj8Ulgl3AbitP+DIlpc8uhV1vjXzsKREotadW/gRGA58aDEOBt0Af4+RDZcqWSJsaBxOtPwBsaxAIszVXf+3lRsU64KQNfgCjgM8FkiGOvq/1stUl7JIcQS9nMc6oC8DKAsF5YIV1umCTgT8tAumXAJcj4BbgUEKivYPR3lLgShpI7cGJT8YvYBbw2A6mAveixhZPXI1A113zJTRcfZhjgtvA4KixmlthVHRLokYg4EiThHmvt1gS3mbNKA26d6WT1iKQ3RTgTjSjgi9FrIye1I5xTwhkr0flUjRpNQSXVV666jEtBTQNOGal3uNHtciD7h/GiXIZGZ8PmgAAAABJRU5ErkJggg=="
            >
          </a>
        -->
      </ul>

      <div class="caret"></div>
    </div>
    <v-btn id="btn" class="success" @click="submitData(), updateComponent()">Next</v-btn>
  </div>
</template>

<script>
import { mainHighlighter } from "@/assets/js/highlight.js";
import axios from "axios";
import md5 from "md5";

export default {
  props: {
    contents: Array,
    file: String
  },
  mounted() {
    fetch("http://localhost:8081/label")
      .then(response => response.json())
      //.then(data => console.log(JSON.stringify(data)))
      .then(data => {
        for (let i = 0; i < data.length; i++) {
          if (data[i].type == "contextual") {
            this.chips.push(data[i].label);
          }
        }
      });
  },
  updated() {
    mainHighlighter();
  },
  data() {
    return {
      show: true,
      finalContents: this.contents,
      index: 0,
      indexer: 0,
      tempdata: null,
      tempstring: "",
      actualContent: [],
      chips: [],
      items: ["Streaming", "Eating"],
      selected: ["John"]
    };
  },
  // watch: {
  //   contents(val) {
  //     this.finalContents = val;
  //     this.updateComponent();
  //   }
  // },
  watch: {
    contents: {
      immediate: true,
      handler: function() {
        this.index = 0;
        this.actualContent = [];
        this.parser(this.contents, "$");
        this.updateComponent();
      }
    },
    actualContent: function() {
      for (let i = 0; i < this.actualContent.length; i++) {
        axios.post("http://localhost:8081/content", {
          _id: md5(this.actualContent[i]),
          content: this.actualContent[i],
          file_id: this.file
        });
      }
    }
  },
  methods: {
    updateComponent() {
      var self = this;
      self.show = false;
      this.$nextTick(function() {
        self.show = true;
      });
    },
    remove(item) {
      this.chips.splice(this.chips.indexOf(item), 1);
      this.chips = [...this.chips];
    },
    parser(data, delimiter) {
      this.actualContent = data.split(delimiter);
    },
    submitData() {
      this.index += 1;
      if (this.index === this.actualContent.length - 1) {
        alert("Reached end of file");
        return;
      }
    },
    insertLabel() {
      axios.post("http://localhost:8081/label", {
        label: this.chips[this.chips.length - 1],
        type: "contextual"
      });
    },
    getIndex(str, event) {
      //alert(str);
      this.tempdata = event.target.toString();
      //this.indexer = str.indexOf(event.target);
    },
    alertMe(item) {
      //alert("hi" + item + this.counter);
      fetch("http://localhost:8081/label")
        .then(response => response.json())
        //.then(data => console.log(JSON.stringify(data)))
        .then(data => {
          for (let i = 0; i < data.length; i++) {
            if (data[i].type == "contextual") {
              if (data[i].label === item) {
                //this.myVarString = data[i].label;
                axios.delete("http://localhost:8081/label/" + data[i]._id);
                //this.myVarId = data[i]._id;
              }
            }
          }
        });
      // .then(
      //   setTimeout(function() {
      //     axios.delete("http://localhost:8081/label" + this.myVarId);
      //     alert("succes");
      //   }, 500)
      // );
    },
    getString(currentLabel) {
      setTimeout(function() {
        fetch("http://localhost:8081/text")
          .then(response => response.json())
          //.then(data => console.log(JSON.stringify(data)))
          .then(data => (this.tempstring = data[data.length - 1].text));
      }, 100);
      setTimeout(function() {
        axios.post("http://localhost:8081/labeledcontent", {
          label: currentLabel,
          type: "contextual",
          file_id: this.file,
          content_id: this.tempstring
        });
      }, 200);
    }
  }
};
</script>

<style scoped>
#btn {
  margin: 20px auto;
  display: block;
}
::selection {
  background: aqua;
  color: black;
}
::-moz-selection {
  background: aqua;
  color: black;
}
label {
  font-family: "Open Sans", Sans;
  font-weight: 100;
  font-size: 36px;
  color: #a0a0a0;
}
.container {
  font-family: "Open Sans", Sans;
  font-weight: 100;
  font-size: 18px;
  color: #484850;
  background: #f7f7f7;
  width: 50%;
  padding: 50px;
  position: absolute;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  margin: auto;
}
.caret {
  border-style: solid;
  border-width: 10px 10px 0px 10px;
  border-bottom-color: transparent;
  border-left-color: transparent;
  border-top-color: rgba(117, 117, 117, 0.8);
  border-right-color: transparent;
  width: 0px;
  height: 0px;
  display: block;
  position: absolute;
  top: 53px;
  left: 45%;
}
#highlight_menu {
  font-family: "Open Sans", Sans;
  font-weight: 100;
  font-size: 18px;
  color: #fff;
  border-radius: 5px;
  background: rgba(117, 117, 117, 0.8);
  position: absolute;
  user-select: none;
  -moz-user-select: none;
  -webkit-user-select: none;
}
.highlight_menu_animate {
  transition: top 75ms ease-out, left 75ms ease-out;
}
.side-by-side {
  width: 100%;
  padding: 0;
  margin: 10px;
  margin-top: 14px;
}
.side-by-side li {
  display: inline;
  padding: 10px;
}
</style>