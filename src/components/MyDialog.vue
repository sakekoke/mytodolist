<template>
  <v-dialog
      v-model="dialog"
      max-width="500px"
  >
    <template v-slot:activator="{ on, attrs }">
      <v-btn
          color="primary"
          dark
          class="mb-2"
          v-bind="attrs"
          v-on="on"
      >
        New Item
      </v-btn>
    </template>
    <v-card>
      <v-card-title>
        <span class="text-h5">Creating an Item</span>
      </v-card-title>

      <v-card-text>
        <v-container>
          <v-row>
            <v-col>
              <v-text-field
                  v-model="item.name"
                  label="Item name"
              />
            </v-col>
          </v-row>
        </v-container>
      </v-card-text>

      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn
            color="blue darken-1"
            text
            @click="closeItem"
        >
          Cancel
        </v-btn>
        <v-btn
            color="blue darken-1"
            text
            @click="saveItem"
        >
          Save
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  name: 'MyDialog',
  data() {
    return {
      dialog: false,
      item: {
        name: '',
        done: false,
      },
    };
  },
  methods: {
    closeItem() {
      this.dialog = false;
      this.item.name = '';
    },
    saveItem() {
      this.$emit('newItem', JSON.parse(JSON.stringify(this.item)));
      this.closeItem();
    },
  },
};
</script>

<style scoped>

</style>
