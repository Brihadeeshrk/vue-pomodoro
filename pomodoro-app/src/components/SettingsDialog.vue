<template>
    <v-row justify="center">
    <v-dialog v-model="dialog" scrollable persistent max-width="300px" >
      <v-card>
        <v-card-title>
          <span class="headline">Settings</span>
        </v-card-title>

        <v-card-text>
            <v-text-field label="Pomodoro" />
            
        </v-card-text>

          <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text @click="closeDialog"> Close </v-btn>
          <v-btn color="blue darken-1" text @click="save"> Save </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    </v-row>
</template>

<script>
export default {
    props: {
        dialog: {
            type: Boolean,
            require: true
        },
        closeDialog: {
            type: Function,
            require: true
        },
        save: {
            type: Function,
            require: true
        }
    }
}
</script>