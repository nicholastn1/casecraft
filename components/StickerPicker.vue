<template>
  <div class="sticker-picker">
    <div class="sticker-list">
      <img style="width: 50px; height: 50px;" v-for="sticker in stickers" :src="sticker.url" :alt="sticker.alt"
        @click="$emit('stickerSelected', sticker)" />
    </div>
  </div>
</template>

<script>
import coffeeSticker from '~/assets/images/coffee.png';
import fireSticker from '~/assets/images/fire.png';
import motivationSticker from '~/assets/images/motivation.png';
import omgSticker from '~/assets/images/omg.png';
import pvSticker from '~/assets/images/positive-vibes.png';
import saturnSticker from '~/assets/images/saturn.png';
import successSticker from '~/assets/images/success.png';
import workSticker from '~/assets/images/work.png';

export default {
  name: "StickerPicker",
  props: ['index'],
  data() {
    return {
      stickers: [
        { url: coffeeSticker, alt: 'coffee' },
        { url: fireSticker, alt: 'fire' },
        { url: motivationSticker, alt: 'motivation' },
        { url: omgSticker, alt: 'omg' },
        { url: pvSticker, alt: 'positive vibes' },
        { url: saturnSticker, alt: 'saturn' },
        { url: successSticker, alt: 'success' },
        { url: workSticker, alt: 'work' }
      ]
    };
  },
  methods: {}
};
</script>

<style scoped>
.sticker-picker {
  cursor: pointer;
  user-select: none;
}

.sticker-list {
  /* Estilos para a lista de stickers */
}

.selected-sticker {
  /* Estilos para o sticker selecionado */
}
</style>
