<template>
  <v-row align="center">
    <v-col cols="6" class="d-flex flex-column align-center">
      <v-row>
        <v-col cols="12">
          <StickerPicker :stickers="stickers" @stickerSelected="addSticker" />
        </v-col>
      </v-row>

      <v-row>
        <v-col cols="12">
          <v-card>
            <v-card-text>
              <div class="text-center mb-3">Choose a color.</div>
              <v-color-picker v-model="selectedColor" />
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>

      <v-row>
        <v-col>
          <v-btn @click="showAddText = true">Add Text</v-btn>
          <v-btn @click="addImage">Add Image</v-btn>
          <v-btn v-if="hasImage" color="error darken-1" @click="removeImage">Remove Image</v-btn>
        </v-col>
      </v-row>

      <v-row dense>
        <v-col>
          <v-btn @click="reset">Reset</v-btn>
          <v-btn color="success darken-2" @click="downloadElement">Download</v-btn>
        </v-col>
      </v-row>
    </v-col>

    <v-col col="6" class="d-flex flex-column align-center">
      <div ref="downloadableElement">
        <div v-if="textFields.length > 0">
          <div v-for="(field, index) in textFields" :key="index">
            <TextField :index="index">{{ field.text }}</TextField>
          </div>
        </div>

        <div v-for="(sticker, index) in addedStickers" :key="index">
          <StickerSelected :index="index" :sticker="sticker" @onRemoveSticker="removeSticker" />
        </div>

        <ImageUpload ref="imageUpload" :selectedColor="selectedColor" @onAddImage="showRemoveImage" />
      </div>
    </v-col>

    <AddText v-model="showAddText" @onAddText="addTextField" />
  </v-row>
</template>

<script>
import ImageUpload from "~/components/ImageUpload.vue";
import TextField from "~/components/TextField.vue";
import StickerPicker from "~/components/StickerPicker.vue";
import StickerSelected from "~/components/StickerSelected.vue";
import coffeeSticker from "~/assets/images/coffee.png";
import fireSticker from "~/assets/images/fire.png";
import motivationSticker from "~/assets/images/motivation.png";
import omgSticker from "~/assets/images/omg.png";
import pvSticker from "~/assets/images/positive-vibes.png";
import saturnSticker from "~/assets/images/saturn.png";
import successSticker from "~/assets/images/success.png";
import workSticker from "~/assets/images/work.png";
import html2canvas from "html2canvas";
import AddText from "~/components/AddText.vue";

export default {
  name: "CustomizePage",
  components: {
    TextField,
    ImageUpload,
    StickerPicker,
    AddText
  },
  data() {
    return {
      hasImage: false,
      selectedColor: "#FF0000",
      textFields: [],
      stickers: [
        { url: coffeeSticker, alt: "coffee" },
        { url: fireSticker, alt: "fire" },
        { url: motivationSticker, alt: "motivation" },
        { url: omgSticker, alt: "omg" },
        { url: pvSticker, alt: "positive vibes" },
        { url: saturnSticker, alt: "saturn" },
        { url: successSticker, alt: "success" },
        { url: workSticker, alt: "work" },
      ],
      addedStickers: [],
      showAddText: false,
    };
  },
  methods: {
    addImage() {
      this.$refs.imageUpload.selectImage();
    },
    showRemoveImage(payload) {
      this.hasImage = payload;
    },
    removeImage() {
      this.$refs.imageUpload.deleteImage();
    },
    addTextField(text) {
      console.log(text)
      this.textFields.push({ text: text, color: "white" });
    },
    addSticker(sticker) {
      this.addedStickers.push(sticker);
    },
    removeSticker(index) {
      if (index >= 0 && index < this.addedStickers.length) {
        this.addedStickers.splice(index, 1);
      } else {
        console.error("Índice inválido");
      }
    },
    downloadElement() {
      const element = this.$refs.downloadableElement;
      html2canvas(element).then((canvas) => {
        const link = document.createElement("a");
        link.download = "filename.png";
        link.href = canvas.toDataURL();
        link.click();
      });
      this.$toast.success('Arquivo baixado com sucesso!')
    },
    reset() {
      this.textFields = []
      this.addedStickers = []
      this.$refs.imageUpload.deleteImage();
    }
  },
};
</script>
