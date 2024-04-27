<template>
  <div class="text" :id="'text' + index" @mousedown.prevent="moveText" @dblclick="editText" @contextmenu.prevent="showColorPicker">
    <slot></slot>
    <v-menu v-model="showPicker" :close-on-content-click="false" offset-y>
      <v-color-picker v-model="currentColor" @input="changeColor"/>
      <template v-slot:activator="{ on }">
        <div v-on="on"></div>
      </template>
    </v-menu>
  </div>
</template>

<script>
export default {
  name: 'TextField',
  props: ['index'],
  data() {
    return {
      isEditingText: false,
      originalText: 'Write here...',
      rotation: 0,
      currentColor: 'red',
      showPicker: false
    }
  },
  methods: {
    moveText(event){
      let textElement = document.getElementById('text' + this.index)
      if (textElement) {
        event.stopPropagation();
        const moveListener = function(e){
          const x = e.clientX
          const y = e.clientY
          textElement.style.top = y - 80 + "px"
          textElement.style.left = x - 30 + "px"
        }
        textElement.addEventListener('mousedown', function(e){
          document.addEventListener('mousemove', moveListener)
        })
        document.addEventListener('mouseup', function(e){
          document.removeEventListener('mousemove', moveListener)
        })
        textElement.addEventListener('wheel', this.rotateText)
      }
    },
    editText(){
      this.isEditingText = true;
      const textElement = document.getElementById('text' + this.index);
      if (textElement) {
        textElement.contentEditable = "true";
        textElement.focus();
        textElement.addEventListener('blur', () => {
          this.isEditingText = false;
          this.originalText = textElement.textContent;
          textElement.contentEditable = "false";
        })
      }
    },
    rotateText(event) {
      this.rotation += event.deltaY > 0 ? 5 : -5
      event.target.style.transform = `rotate(${this.rotation}deg)`
    },
    showColorPicker(event){
      event.preventDefault()
      this.showPicker = true
    },
    changeColor(color){
      this.currentColor = color
      const textElement = document.getElementById('text' + this.index)
      if (textElement){
        textElement.style.color = color
      }
    }
  }
}
</script>

<style scoped>
.text {
  position: absolute;
  z-index: 1;
  color: red;
  cursor: pointer;
  user-select: none;
}
.text[contenteditable=true] {
  border: 1px solid #ccc;
  padding: 5px;
}
</style>
