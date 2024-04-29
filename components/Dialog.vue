<template>
  <v-dialog v-model="show" :max-width="maxWidth" :persistent="false">
    <v-card class="pb-3 rounded-lg">
      <v-card-title class="font-weight-bold">
        <v-skeleton-loader v-if="loading" width="350" type="heading"></v-skeleton-loader>
        <span v-else>{{ title }}</span>
      </v-card-title>

      <v-divider />

      <v-card-text :class="{'mt-8': contentMarginTop}" style="font-size: 16px;">
        <slot name="content"></slot>
      </v-card-text>

      <v-divider class="mb-3" v-if="$slots.actions" />

      <v-card-actions>
        <slot name="actions">

        </slot>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>

export default {
  props: {
    value: {
      type:Boolean,
      required: true,
    },
    loading: {
      type: Boolean,
      required: false,
      default: false
    },
    title: {
      type: String,
      required: true,
    },
    icon: {
      type: String,
      required: false,
    },
    maxWidth: {
      type: Number,
      required: false,
      default: 560,
    },
    contentMarginTop: {
      type: Boolean,
      required: false,
      default: true
    },
  },

  data() {
    return {
      dialog: false,
    };
  },


  computed: {
    show: {
      get () {
        return this.value
      },
      set (value) {
         this.$emit('input', value)
      }
    }
  },

  methods: {

  },
};
</script>
<template>
  <v-dialog v-model="show" :max-width="maxWidth" :persistent="false">
    <v-card class="pb-3 rounded-lg">
      <v-card-title class="font-weight-bold">
        <v-skeleton-loader v-if="loading" width="350" type="heading"></v-skeleton-loader>
        <span v-else>{{ title }}</span>
        <!-- <v-spacer></v-spacer>
        <v-btn icon @click="show = false"><v-icon>mdi-close</v-icon></v-btn> -->
      </v-card-title>

      <v-divider />

      <v-card-text :class="{'mt-8': contentMarginTop}" style="font-size: 16px;">
        <slot name="content"></slot>
      </v-card-text>

      <v-divider class="mb-3" v-if="$slots.actions" />

      <v-card-actions>
        <slot name="actions">

        </slot>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>

export default {
  props: {
    value: {
      type:Boolean,
      required: true,
    },
    loading: {
      type: Boolean,
      required: false,
      default: false
    },
    title: {
      type: String,
      required: true,
    },
    icon: {
      type: String,
      required: false,
    },
    maxWidth: {
      type: Number,
      required: false,
      default: 560,
    },
    contentMarginTop: {
      type: Boolean,
      required: false,
      default: true
    },
  },

  data() {
    return {
      dialog: false,
    };
  },


  computed: {
    show: {
      get () {
        return this.value
      },
      set (value) {
         this.$emit('input', value)
      }
    }
  },

  methods: {

  },
};
</script>
