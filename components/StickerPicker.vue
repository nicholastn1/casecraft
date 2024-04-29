<template>
  <v-card class="rounded-lg">
    <v-card-text>
      <div class="text-center mb-3">Choose one or more stickers.</div>
      <div class="sticker-picker">
        <div class="sticker-list">
          <img class="sticker" width="50" height="50" v-for="sticker in stickers" :src="sticker.url" :alt="sticker.alt"
            @click="$emit('stickerSelected', sticker)" />
        </div>
      </div>
    </v-card-text>
  </v-card>

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

.sticker {
  margin: 0 5px
}

.sticker:hover {
  transform: scale(1.2);
}

.selected-sticker {
  /* Estilos para o sticker selecionado */
}
</style>
