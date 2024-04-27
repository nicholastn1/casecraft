<template>
  <v-row class="align-center justify-center">
    <v-col class="d-flex flex-column justify-center align-center" cols="12" sm="8" md="4">
      <div class="justify-center">
        <v-color-picker v-model="selectedColor"/>
      </div>
      <v-btn class="mt-10">Add Text</v-btn>
    </v-col>
    <v-col class="d-flex justify-center" cols="12" sm="8" md="5">
      <TextField>Write here...</TextField>
      <ImageUpload v-model="image" :selectedColor="selectedColor"/>
    </v-col>
  </v-row>
</template>

<script>
import ImageUpload from '~/components/ImageUpload.vue'
import TextField from '~/components/TextField.vue'
export default {
  name: 'CustomizePage',
  components: {
    TextField,
    ImageUpload
  },
  data() {
    return {
      image: undefined,
      selectedColor: '#ffffff'
    }
  }
}
</script>
