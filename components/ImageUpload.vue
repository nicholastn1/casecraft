<template>
  <v-card style="width: 413.5px !important; background-color: transparent; height: inherit;" class="overflow-hidden"
    @click.stop="selectImage">
    <input class="d-none" id="fileInput" type="file" accept="images/*" @input="handleFileUpload" />
    <v-fade-transition mode="out-in">
      <v-img v-if="image" :src="image" width="600" height="859" class="phone-case">
        <v-row class="fill-height" align="end" justify="center">
          <v-btn class="md-3" fab x-small color="error" @click.stop="deleteImage">
            <v-icon>mdi-delete</v-icon>
          </v-btn>
        </v-row>
      </v-img>
      <v-row v-else class="d-flex align-center justify-center fill-height">
        <svg v-bind:style="{ fill: selectedColor }" class="phone-mask" width="inherit" height="inherit" viewBox="0 0 241 498"
          fill="none" xmlns="http://www.w3.org/2000/svg">
          <defs>
            <mask>
              <rect x="10" y="10" width="100" height="200" />
            </mask>
          </defs>
          <path
            d="M0.236145 30.8832C0.236145 13.997 13.9272 0.308105 30.8159 0.308105H209.613C226.502 0.308105 240.193 13.997 240.193 30.8832V466.84C240.193 483.726 226.502 497.415 209.613 497.415H30.8159C13.9272 497.415 0.236145 483.726 0.236145 466.84V30.8832ZM6.33857 93.3281C6.33857 110.214 20.0296 123.903 36.9184 123.903H95.7372C112.626 123.903 126.317 110.214 126.317 93.3281V36.3359C126.317 19.4498 112.626 5.76083 95.7372 5.76083H36.9184C20.0296 5.76083 6.33857 19.4498 6.33857 36.3359V93.3281Z" />
        </svg>
        <img :src="caseMockup" style="position: absolute; width: inherit; height: inherit;" alt="Mockup Case IPhone 13 Pro Max" />
      </v-row>
    </v-fade-transition>
  </v-card>
</template>

<script>
import IphoneMockupCase from "~/assets/images/IphoneMockupCase.png";
export default {
  name: "ImageUpload",
  props: {
    selectedColor: String,
  },
  data() {
    return {
      input: undefined,
      imageFile: undefined,
      image: undefined,
      mask: false,
      caseMockup: IphoneMockupCase,
    };
  },
  mounted() {
    this.input = document.getElementById("fileInput");
  },
  methods: {
    selectImage() {
      if (!this.imageFile) {
        this.input.click();
      }
    },
    handleFileUpload(event) {
      this.imageFile = event.target.files[0];
      this.image = this.imageFile
        ? URL.createObjectURL(this.imageFile)
        : undefined;
      this.$emit("file", this.imageFile);
    },
    deleteImage() {
      if (this.imageFile) {
        this.image = undefined;
        this.imageFile = undefined;
        this.$emit("file", undefined);
      }
    },
  },
};
</script>

<style scoped>
.phone-case {
  mask-image: url(../assets/images/PhoneCaseMask.svg);
  mask-repeat: no-repeat;
  width: 24rem;
  height: 44rem;
  fill: "#{selectedColor}";
  bottom: 2.58rem !important;
  position: absolute;
}

.phone-mask {
  z-index: 1;
  width: 21rem;
  position: absolute;
  height: 43rem;
  top: 2.39rem;
}

@media (max-height: 885px) {
  .phone-mask {
    height: 43rem !important;
    top: 2.32rem !important;
  }
}

@media (max-height: 959px) {
  .phone-mask {
    width: 25.844rem;
    height: 46.5rem;
    top: 2.6rem;
    left: 0.1rem;
  }
}

</style>
