<template>
  <div id="main">
    <section v-if="show" class="dataspace" v-html="finalContents"></section>

    <div id="highlight_menu" style="display:none;">
      <ul class="side-by-side">
        <li id="first-menu">
          <a href="#" title="Skill">
            <img
              src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAABPUlEQVRIS83Vuy5FURAG4O80VNQujyBRuJQulQIVDT2lZ8AraOlpqFCoXDpEI14BNRUNmWTt5OQcZ9/YianWXnut+df/zz+ZloajVSF/nF1M58/xVeZuFYAlnKakyzj7a4AdbKeku4jvwijDYBCz2MJCyniFy7R+xyGef0IrAggp9jFU8NR7TFcFGMMD+gp1oBbAMVZS8qB/hJCjM96SRC9VGUTS4XQp6McrK0deDRoHaJco6IdTMok+8IhrhEQ9I49BmSK/YrOtAbuAimwa3XtQYNNPTOCpapGz89FoMxhHf9ocwBpG0vcJVusC9NI3nHXbZuPRfwcQ9NcRcnRG7MW/rE9qSXSHqRKdFZadrFPkMgBh04282ZBn06AfMoSLIuYxl9YX2MPNbxqtU53GBk4G1PjIbHzolzBU95Fv03g+GaYNGS0AAAAASUVORK5CYII="
            >
          </a>
        </li>
        <li id="second-menu">
          <a href="#" title="Location">
            <img
              src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAACQUlEQVRIS52VSajIURTGfy8lylAWpqRQ5lKKkISQKFZIIQllKcVKxIqFpWRMJMOKooTIEElJGZMsCFlYIKRE3+u7r/tud3g5m///3vOd853h3nM7aMsCYBUwGxhh+HvgLnAOuF5z0VFRjgGOAnMbMdwENgFvcrgSgaK9CAxqJ9iJ+AIsd1bdTHIEivxh5PyvMzkOPLP1JGADsBEIPkQyPc0kR6CUQ1k+AGsA7eVkHnAaGG6lcPNjYEqghl4zQJELfKtRJpHciDJZGDc+JTjitOVT/5vtvDewF1jr9SlgJ/Db68NudGrXVb8Q5AtgvBczgQf+3wdsTzLZD+zw3gzgvv9fAhMCNs3gG9DPygGA1hL1YlhC8DGqfX/gq/WykW2npAQCCSzR9/t/EMjHwBLB8yi9scDrHpZI2FfGyoeOcTaDq8Ai61YDZ/3farKwZ4yVj8Ulgl3AbitP+DIlpc8uhV1vjXzsKREotadW/gRGA58aDEOBt0Af4+RDZcqWSJsaBxOtPwBsaxAIszVXf+3lRsU64KQNfgCjgM8FkiGOvq/1stUl7JIcQS9nMc6oC8DKAsF5YIV1umCTgT8tAumXAJcj4BbgUEKivYPR3lLgShpI7cGJT8YvYBbw2A6mAveixhZPXI1A113zJTRcfZhjgtvA4KixmlthVHRLokYg4EiThHmvt1gS3mbNKA26d6WT1iKQ3RTgTjSjgi9FrIye1I5xTwhkr0flUjRpNQSXVV666jEtBTQNOGal3uNHtciD7h/GiXIZGZ8PmgAAAABJRU5ErkJggg=="
            >
          </a>
        </li>
        <li id="second-menu">
          <a href="#" title="Location">
            <img
              src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAACQUlEQVRIS52VSajIURTGfy8lylAWpqRQ5lKKkISQKFZIIQllKcVKxIqFpWRMJMOKooTIEElJGZMsCFlYIKRE3+u7r/tud3g5m///3vOd853h3nM7aMsCYBUwGxhh+HvgLnAOuF5z0VFRjgGOAnMbMdwENgFvcrgSgaK9CAxqJ9iJ+AIsd1bdTHIEivxh5PyvMzkOPLP1JGADsBEIPkQyPc0kR6CUQ1k+AGsA7eVkHnAaGG6lcPNjYEqghl4zQJELfKtRJpHciDJZGDc+JTjitOVT/5vtvDewF1jr9SlgJ/Db68NudGrXVb8Q5AtgvBczgQf+3wdsTzLZD+zw3gzgvv9fAhMCNs3gG9DPygGA1hL1YlhC8DGqfX/gq/WykW2npAQCCSzR9/t/EMjHwBLB8yi9scDrHpZI2FfGyoeOcTaDq8Ai61YDZ/3farKwZ4yVj8Ulgl3AbitP+DIlpc8uhV1vjXzsKREotadW/gRGA58aDEOBt0Af4+RDZcqWSJsaBxOtPwBsaxAIszVXf+3lRsU64KQNfgCjgM8FkiGOvq/1stUl7JIcQS9nMc6oC8DKAsF5YIV1umCTgT8tAumXAJcj4BbgUEKivYPR3lLgShpI7cGJT8YvYBbw2A6mAveixhZPXI1A113zJTRcfZhjgtvA4KixmlthVHRLokYg4EiThHmvt1gS3mbNKA26d6WT1iKQ3RTgTjSjgi9FrIye1I5xTwhkr0flUjRpNQSXVV666jEtBTQNOGal3uNHtciD7h/GiXIZGZ8PmgAAAABJRU5ErkJggg=="
            >
          </a>
        </li>
        <li id="second-menu">
          <a href="#" title="Location">
            <img
              src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAACQUlEQVRIS52VSajIURTGfy8lylAWpqRQ5lKKkISQKFZIIQllKcVKxIqFpWRMJMOKooTIEElJGZMsCFlYIKRE3+u7r/tud3g5m///3vOd853h3nM7aMsCYBUwGxhh+HvgLnAOuF5z0VFRjgGOAnMbMdwENgFvcrgSgaK9CAxqJ9iJ+AIsd1bdTHIEivxh5PyvMzkOPLP1JGADsBEIPkQyPc0kR6CUQ1k+AGsA7eVkHnAaGG6lcPNjYEqghl4zQJELfKtRJpHciDJZGDc+JTjitOVT/5vtvDewF1jr9SlgJ/Db68NudGrXVb8Q5AtgvBczgQf+3wdsTzLZD+zw3gzgvv9fAhMCNs3gG9DPygGA1hL1YlhC8DGqfX/gq/WykW2npAQCCSzR9/t/EMjHwBLB8yi9scDrHpZI2FfGyoeOcTaDq8Ai61YDZ/3farKwZ4yVj8Ulgl3AbitP+DIlpc8uhV1vjXzsKREotadW/gRGA58aDEOBt0Af4+RDZcqWSJsaBxOtPwBsaxAIszVXf+3lRsU64KQNfgCjgM8FkiGOvq/1stUl7JIcQS9nMc6oC8DKAsF5YIV1umCTgT8tAumXAJcj4BbgUEKivYPR3lLgShpI7cGJT8YvYBbw2A6mAveixhZPXI1A113zJTRcfZhjgtvA4KixmlthVHRLokYg4EiThHmvt1gS3mbNKA26d6WT1iKQ3RTgTjSjgi9FrIye1I5xTwhkr0flUjRpNQSXVV666jEtBTQNOGal3uNHtciD7h/GiXIZGZ8PmgAAAABJRU5ErkJggg=="
            >
          </a>
        </li>
        <li id="second-menu">
          <a href="#" title="Location">
            <img
              src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAACQUlEQVRIS52VSajIURTGfy8lylAWpqRQ5lKKkISQKFZIIQllKcVKxIqFpWRMJMOKooTIEElJGZMsCFlYIKRE3+u7r/tud3g5m///3vOd853h3nM7aMsCYBUwGxhh+HvgLnAOuF5z0VFRjgGOAnMbMdwENgFvcrgSgaK9CAxqJ9iJ+AIsd1bdTHIEivxh5PyvMzkOPLP1JGADsBEIPkQyPc0kR6CUQ1k+AGsA7eVkHnAaGG6lcPNjYEqghl4zQJELfKtRJpHciDJZGDc+JTjitOVT/5vtvDewF1jr9SlgJ/Db68NudGrXVb8Q5AtgvBczgQf+3wdsTzLZD+zw3gzgvv9fAhMCNs3gG9DPygGA1hL1YlhC8DGqfX/gq/WykW2npAQCCSzR9/t/EMjHwBLB8yi9scDrHpZI2FfGyoeOcTaDq8Ai61YDZ/3farKwZ4yVj8Ulgl3AbitP+DIlpc8uhV1vjXzsKREotadW/gRGA58aDEOBt0Af4+RDZcqWSJsaBxOtPwBsaxAIszVXf+3lRsU64KQNfgCjgM8FkiGOvq/1stUl7JIcQS9nMc6oC8DKAsF5YIV1umCTgT8tAumXAJcj4BbgUEKivYPR3lLgShpI7cGJT8YvYBbw2A6mAveixhZPXI1A113zJTRcfZhjgtvA4KixmlthVHRLokYg4EiThHmvt1gS3mbNKA26d6WT1iKQ3RTgTjSjgi9FrIye1I5xTwhkr0flUjRpNQSXVV666jEtBTQNOGal3uNHtciD7h/GiXIZGZ8PmgAAAABJRU5ErkJggg=="
            >
          </a>
        </li>
        <li id="second-menu">
          <a href="#" title="Location">
            <img
              src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAACQUlEQVRIS52VSajIURTGfy8lylAWpqRQ5lKKkISQKFZIIQllKcVKxIqFpWRMJMOKooTIEElJGZMsCFlYIKRE3+u7r/tud3g5m///3vOd853h3nM7aMsCYBUwGxhh+HvgLnAOuF5z0VFRjgGOAnMbMdwENgFvcrgSgaK9CAxqJ9iJ+AIsd1bdTHIEivxh5PyvMzkOPLP1JGADsBEIPkQyPc0kR6CUQ1k+AGsA7eVkHnAaGG6lcPNjYEqghl4zQJELfKtRJpHciDJZGDc+JTjitOVT/5vtvDewF1jr9SlgJ/Db68NudGrXVb8Q5AtgvBczgQf+3wdsTzLZD+zw3gzgvv9fAhMCNs3gG9DPygGA1hL1YlhC8DGqfX/gq/WykW2npAQCCSzR9/t/EMjHwBLB8yi9scDrHpZI2FfGyoeOcTaDq8Ai61YDZ/3farKwZ4yVj8Ulgl3AbitP+DIlpc8uhV1vjXzsKREotadW/gRGA58aDEOBt0Af4+RDZcqWSJsaBxOtPwBsaxAIszVXf+3lRsU64KQNfgCjgM8FkiGOvq/1stUl7JIcQS9nMc6oC8DKAsF5YIV1umCTgT8tAumXAJcj4BbgUEKivYPR3lLgShpI7cGJT8YvYBbw2A6mAveixhZPXI1A113zJTRcfZhjgtvA4KixmlthVHRLokYg4EiThHmvt1gS3mbNKA26d6WT1iKQ3RTgTjSjgi9FrIye1I5xTwhkr0flUjRpNQSXVV666jEtBTQNOGal3uNHtciD7h/GiXIZGZ8PmgAAAABJRU5ErkJggg=="
            >
          </a>
        </li>
        <li id="second-menu">
          <a href="#" title="Location">
            <img
              src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAACQUlEQVRIS52VSajIURTGfy8lylAWpqRQ5lKKkISQKFZIIQllKcVKxIqFpWRMJMOKooTIEElJGZMsCFlYIKRE3+u7r/tud3g5m///3vOd853h3nM7aMsCYBUwGxhh+HvgLnAOuF5z0VFRjgGOAnMbMdwENgFvcrgSgaK9CAxqJ9iJ+AIsd1bdTHIEivxh5PyvMzkOPLP1JGADsBEIPkQyPc0kR6CUQ1k+AGsA7eVkHnAaGG6lcPNjYEqghl4zQJELfKtRJpHciDJZGDc+JTjitOVT/5vtvDewF1jr9SlgJ/Db68NudGrXVb8Q5AtgvBczgQf+3wdsTzLZD+zw3gzgvv9fAhMCNs3gG9DPygGA1hL1YlhC8DGqfX/gq/WykW2npAQCCSzR9/t/EMjHwBLB8yi9scDrHpZI2FfGyoeOcTaDq8Ai61YDZ/3farKwZ4yVj8Ulgl3AbitP+DIlpc8uhV1vjXzsKREotadW/gRGA58aDEOBt0Af4+RDZcqWSJsaBxOtPwBsaxAIszVXf+3lRsU64KQNfgCjgM8FkiGOvq/1stUl7JIcQS9nMc6oC8DKAsF5YIV1umCTgT8tAumXAJcj4BbgUEKivYPR3lLgShpI7cGJT8YvYBbw2A6mAveixhZPXI1A113zJTRcfZhjgtvA4KixmlthVHRLokYg4EiThHmvt1gS3mbNKA26d6WT1iKQ3RTgTjSjgi9FrIye1I5xTwhkr0flUjRpNQSXVV666jEtBTQNOGal3uNHtciD7h/GiXIZGZ8PmgAAAABJRU5ErkJggg=="
            >
          </a>
        </li>
        <li id="third-menu">
          <a href="#" title="Job Title">
            <img
              src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAB6klEQVRIS7XVSaiOYRQH8N8lVoYkZaNMZVopmXZICmVc2VAyLSywIAvdSDcLLCykLFjIQhkKJbHkypANsjAspSvjShk6Om+9Xe/3ve/nu87q7T3/8/8/Z3jO06PepmA3VmBqwl/jFk7hTTuKnhr+/TiMkS1w33EIx1rxtBM4gT31Cf5BnMTeKmwrgXW4XAp4liftz38LM7M5Jcx6XBksUiUQ/15gRoKvYwOiHGWLssUhVuXPl5jZRGAeHibwSwq9a1GqiQjiMemP2MdlbFUGO3E6QTewuqYPgVmZmIg9UydwEEcTFI3eVyNwvNTgiO2rE/jvGczFk3/sQcQ+rcsg/M8xq8Mpismb3WSKArMGVzu8B2txralA4M5hc02DC/d5bKnCVo3peBzBdgxvKPAjxzP20od2PViGSxjXkHgw7CM24m7hKGcwH3cwqhR1My/dgzzZz/QNQ2S6ALtKFy3c37C02AaFwGQ8yqAAxY7fgdsNM1meJYq3IyzKFGvjbSFwFlvT+R6LEI9KJzYN9zEhg4JzWwhMwiuMwC8sRrGWOxEIbKzxewje2L7T4yN2x4FkiuZEo7ux4FiSBH0hEGmFctgmXOyGPTkuJEd/CAyUmtsl91/hAyHwCWOHmjn5PodAPNa9GD3EIl+D9zcQIGHQ6aGVVwAAAABJRU5ErkJggg=="
            >
          </a>
        </li>
        <li id="fourth-menu">
          <a href="#" title="Irrelevant">
            <img
              src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAABgAAAAYCAYAAADgdz34AAAA70lEQVRIS+2VsQ3CMBBFXyQEDdAzBBWipWAIBqGgJZQIwSDsQENNxw4ZgNCAhEA/OMiKEjtRKH2d5X//+75PdxHu6ABLYAGMga6BP4ErcAT2wKuKJnLwi/wEzDyPOAPzKhGXwArYesjza2F3ZViXwAWYmKQDEAOpOQ/MWfYphJ02FXhYng8t8pxHIjfrT3pNBd5WQlWlXowSVeYG6Nf0uy7sDqwlkACjulkNcUlegT5Qnv4z1BBx0Vuvp44XlOYGAduxYJG3g4NFwaKvA3YneD1xAH4jqDiLNAHb7gVxaANmURTQ8mkzurMRDWiHZ/EB2Co54vlRm6IAAAAASUVORK5CYII="
            >
          </a>
        </li>
      </ul>

      <div class="caret"></div>
    </div>
    <v-btn id="btn" class="success">Fail</v-btn>
  </div>
</template>

<script>
import mainHighlighter from "@/assets/js/highlight.js";
export default {
  props: ["contents"],
  updated() {
    mainHighlighter();
  },
  data() {
    return {
      show: true,
      finalContents: this.contents
    };
  },
  watch: {
    contents(val) {
      this.finalContents = val;
      this.updateComponent();
    }
  },
  methods: {
    updateComponent() {
      var self = this;
      self.show = false;

      this.$nextTick(function() {
        self.show = true;
      });
    }
  }
  // methods: {
  //   mainHighlighter() {
  //     mainHighlighter();
  //   }
  // }
  // mounted() {
  //   mainHighlighter();
  // }
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

