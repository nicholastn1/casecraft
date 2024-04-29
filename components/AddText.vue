<template>
  <Dialog title="Add Text" :maxWidth="480" v-model="showDialog">
    <template #content>
      <v-text-field
            v-model="text"
            placeholder="Type here..."
            ></v-text-field>
    </template>

    <template #actions>
      <v-row justify="end">
        <v-col cols="auto">
          <v-btn title="Cancelar" text @click="showDialog = false">
            Cancel
          </v-btn>
        </v-col>

        <v-col cols="auto">
          <v-btn
            title="Exportar"
            color="primary"
            @click.prevent="AddText"
            :disabled="!text"
          >
            Add
          </v-btn>
        </v-col>
      </v-row>
    </template>
  </Dialog>
</template>

<script>
import Dialog from "@/components/Dialog";

export default {
  name: "DataExport",

  components: {
    Dialog,
  },

  props: {
    value: {
      type: Boolean,
    },
  },

  data() {
    return {
      text: "",
    };
  },

  computed: {
    showDialog: {
      get() {
        return this.value;
      },
      set(value) {
        this.$emit("input", value);
      },
  },
},

  methods: {
    AddText() {
      this.$emit("onAddText", this.text);
      this.showDialog = false;
      this.text = "";
    }
  }

};
</script>
