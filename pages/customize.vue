<template>
  <v-row class="align-center justify-center">
    <v-col
      class="d-flex flex-column justify-center align-center"
      cols="12"
      sm="8"
      md="4"
    >
      <div class="justify-center">
        <v-color-picker v-model="selectedColor" />
      </div>
      <v-btn class="mt-10" @click="addTextField">Add Text</v-btn>
    </v-col>
    <v-col class="d-flex justify-center" cols="12" sm="8" md="5">
      <div v-for="(field, index) in textFields" :key="index">
        <TextField :index="index">{{ field.text }}</TextField>
      </div>
      <ImageUpload v-model="image" :selectedColor="selectedColor" />
    </v-col>
  </v-row>
</template>

<script>
import ImageUpload from "~/components/ImageUpload.vue";
import TextField from "~/components/TextField.vue";
export default {
  name: "CustomizePage",
  components: {
    TextField,
    ImageUpload,
  },
  data() {
    return {
      image: undefined,
      selectedColor: "#ffffff",
      textFields: [{ text: "Write here...", color: "red" }],
    };
  },
  methods: {
    addTextField() {
      this.textFields.push({ text: "Write here...", color: "red" });
    },
  },
};
</script>
