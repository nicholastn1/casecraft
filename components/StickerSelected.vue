<template>
  <div class="sticker" :id="'sticker' + index" @mousedown.prevent="moveSticker">
    <img :src="sticker.url" :alt="sticker.alt" />
  </div>
</template>

<script>
export default {
  name: "StickerSelected",
  props: ['index', 'sticker'],
  data() {
    return {
      rotation: 0
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
        stickerElement.addEventListener("mousedown", function (e) {
          document.addEventListener("mousemove", moveListener);
        });
        document.addEventListener("mouseup", function (e) {
          document.removeEventListener("mousemove", moveListener);
        });
        stickerElement.addEventListener("wheel", this.rotateSticker);
      }
    },
    rotateSticker(event) {
      this.rotation += event.deltaY > 0 ? 5 : -5;
      event.target.style.transform = `rotate(${this.rotation}deg)`;
    }
  }
};
</script>

<style scoped>
.sticker {
  position: absolute;
  z-index: 2;
}

.sticker img {
  width: 100px;
  height: 100px;
  cursor: move;
  user-select: none;
}
</style>
