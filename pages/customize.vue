<template>
  <v-row class="align-center justify-center">
    <v-col class="d-flex flex-column justify-center align-center" cols="12" sm="8" md="4">
      <StickerPicker :stickers="stickers" @stickerSelected="addSticker" />
      <div class="justify-center">
        <v-color-picker v-model="selectedColor" />
      </div>
      <v-btn class="mt-10" @click="addTextField">Add Text</v-btn>
    </v-col>
    <v-col class="d-flex justify-center" cols="12" sm="8" md="5">
      <div v-for="(field, index) in textFields" :key="index">
        <TextField :index="index">{{ field.text }}</TextField>
      </div>
      <div v-for="(sticker, index) in addedStickers" :key="index">
        <StickerSelected :index="index" :sticker="sticker" />
      </div>
      <ImageUpload v-model="image" :selectedColor="selectedColor" />
    </v-col>
  </v-row>
</template>

<script>
import ImageUpload from "~/components/ImageUpload.vue";
import TextField from "~/components/TextField.vue";
import StickerPicker from "~/components/StickerPicker.vue";
import StickerSelected from "~/components/StickerSelected.vue";
import coffeeSticker from '~/assets/images/coffee.png';
import fireSticker from '~/assets/images/fire.png';
import motivationSticker from '~/assets/images/motivation.png';
import omgSticker from '~/assets/images/omg.png';
import pvSticker from '~/assets/images/positive-vibes.png';
import saturnSticker from '~/assets/images/saturn.png';
import successSticker from '~/assets/images/success.png';
import workSticker from '~/assets/images/work.png';

export default {
  name: "CustomizePage",
  components: {
    TextField,
    ImageUpload,
    StickerPicker,
  },
  data() {
    return {
      image: undefined,
      selectedColor: "#FF0000",
      textFields: [{ text: "Write here...", color: "white" }],
      stickers: [
        { url: coffeeSticker, alt: 'coffee' },
        { url: fireSticker, alt: 'fire' },
        { url: motivationSticker, alt: 'motivation' },
        { url: omgSticker, alt: 'omg' },
        { url: pvSticker, alt: 'positive vibes' },
        { url: saturnSticker, alt: 'saturn' },
        { url: successSticker, alt: 'success' },
        { url: workSticker, alt: 'work' }
      ],
      addedStickers: []
    };
  },
  methods: {
    addTextField() {
      this.textFields.push({ text: "Write here...", color: "white" });
    },
    addSticker(sticker) {
      this.addedStickers.push(sticker);
    }
  },
};
</script>
