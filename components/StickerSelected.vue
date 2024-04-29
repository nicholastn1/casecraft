<template>
  <div>
    <div @contextmenu.prevent="showMenu = true" class="sticker" :id="'sticker' + index" @mousedown.prevent="moveSticker" style="cursor: pointer;">
      <img :src="sticker.url" :alt="sticker.alt" :width="stickerWidth"/>
    </div>

    <v-menu v-model="showMenu" :close-on-content-click="false" offset-y min-width="320">
      <div class="ml-2">Size</div>
      <v-slider v-model="stickerWidth" min="50" max="200"  step="1"></v-slider>

      <template v-slot:activator="{ on }">
        <div v-on="on"></div>
      </template>

      <v-btn block @click.prevent="removeSticker">Remove</v-btn>
    </v-menu>
  </div>
</template>

<script>
export default {
  name: "StickerSelected",
  props: ['index', 'sticker'],
  data() {
    return {
      rotation: 0,
      showMenu: false,
      stickerWidth: 100,
    };
  },
  methods: {
    moveSticker(event) {
      let stickerElement = document.getElementById("sticker" + this.index);
      if (stickerElement) {
        event.stopPropagation();
        const moveListener = function (e) {
          const x = e.clientX;
          const y = e.clientY;
          stickerElement.style.top = y - 110 + "px";
          stickerElement.style.left = x - 45 + "px";
        };
        document.addEventListener("mousemove", moveListener);

        document.addEventListener("mouseup", function (e) {
          document.removeEventListener("mousemove", moveListener);
        });
        stickerElement.addEventListener("wheel", this.rotateSticker);
      }
    },
    rotateSticker(event) {
      this.rotation += event.deltaY > 0 ? 5 : -5;
      event.target.style.transform = `rotate(${this.rotation}deg)`;
    },
    removeSticker() {
      this.$emit("onRemoveSticker", this.index);
    }
  }
};
</script>

<style scoped>
.sticker {
  position: absolute;
  z-index: 1;
}

.v-menu__content {
  background: #1e1e1e;
}
</style>
