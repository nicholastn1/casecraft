<template>
  <div
    class="text"
    :id="'text' + index"
    @mousedown.prevent="moveText"
    @dblclick="editText"
    @contextmenu.prevent="showColorPicker"
    :style="{ fontSize: fontSize + 'px' }"
  >
    <slot></slot>
    <v-menu v-model="showPicker" :close-on-content-click="false" offset-y>
      <v-color-picker v-model="currentColor" @input="changeColor" />
      <v-slider
        style="background-color: #1e1e1e"
        v-model="fontSize"
        min="10"
        max="30"
        step="1"
      ></v-slider>
      <template v-slot:activator="{ on }">
        <div v-on="on"></div>
      </template>
      <v-list>
        <v-list-item
          v-for="(font, i) in fonts"
          :key="i"
          @click="changeFontStyle(font)"
        >
          <v-list-item-title>{{ font }}</v-list-item-title>
        </v-list-item>
      </v-list>
    </v-menu>
  </div>
</template>

<script>
export default {
  name: "TextField",
  props: ["index"],
  data() {
    return {
      isEditingText: false,
      originalText: "Write here...",
      rotation: 0,
      currentColor: "red",
      showPicker: false,
      showFontPicker: false,
      fonts: [
        "Arial",
        "Bungee",
        "Bungee Spice",
        "Honk",
        "Shantell Sans",
        "Fira Code",
      ],
      currentFont: "Arial",
      fontSize: 14,
    };
  },
  methods: {
    moveText(event) {
      let textElement = document.getElementById("text" + this.index);
      if (textElement) {
        event.stopPropagation();
        const moveListener = function (e) {
          const x = e.clientX;
          const y = e.clientY;
          textElement.style.top = y - 80 + "px";
          textElement.style.left = x - 30 + "px";
        };
        textElement.addEventListener("mousedown", function (e) {
          document.addEventListener("mousemove", moveListener);
        });
        document.addEventListener("mouseup", function (e) {
          document.removeEventListener("mousemove", moveListener);
        });
        textElement.addEventListener("wheel", this.rotateText);
      }
    },
    editText() {
      this.isEditingText = true;
      const textElement = document.getElementById("text" + this.index);
      if (textElement) {
        textElement.contentEditable = "true";
        textElement.focus();
        textElement.addEventListener("blur", () => {
          this.isEditingText = false;
          this.originalText = textElement.textContent;
          textElement.contentEditable = "false";
        });
      }
    },
    rotateText(event) {
      this.rotation += event.deltaY > 0 ? 5 : -5;
      event.target.style.transform = `rotate(${this.rotation}deg)`;
    },
    showColorPicker(event) {
      event.preventDefault();
      this.showPicker = true;
    },
    changeColor(color) {
      this.currentColor = color;
      const textElement = document.getElementById("text" + this.index);
      if (textElement) {
        textElement.style.color = color;
      }
    },
    changeFontStyle(font) {
      this.currentFont = font;
      const textElement = document.getElementById("text" + this.index);
      if (textElement) {
        textElement.style.fontFamily = font;
      }
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Bungee&family=Bungee+Spice&family=Fira+Code:wght@300..700&family=Honk&family=Jersey+25&family=Shantell+Sans:ital,wght@0,300..800;1,300..800&display=swap");
.text {
  position: absolute;
  z-index: 1;
  color: red;
  cursor: pointer;
  user-select: none;
}
.text[contenteditable="true"] {
  border: 1px solid #ccc;
  padding: 5px;
}
</style>
