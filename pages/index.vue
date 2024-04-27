<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card>
        <v-card-text>
          <v-card-title>Welcome to the Case Craft </v-card-title>
          <v-card-subtitle>
            <p>
              This is a simple application that allows you to customize your own case.
            </p>
            <p>
              You can choose the color, the image and the font size of your case.
            </p>
          </v-card-subtitle>
          <v-card-text>
            <v-btn color="primary" to="/customize">Customize Your Case</v-btn>
          </v-card-text>
        </v-card-text>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'IndexPage'
}
</script>
