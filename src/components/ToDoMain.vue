<template>
  <v-container>
    <v-row>
      <v-col>
        <h1>
          ToDo App
        </h1>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-card>
          <v-card-title>
            To Do List
            <v-spacer></v-spacer>
            <my-dialog @newItem="newItem"/>
            <v-spacer></v-spacer>
            <v-text-field
                v-model="search"
                append-icon="mdi-magnify"
                label="Search"
                single-line
                hide-details
            ></v-text-field>
          </v-card-title>
          <v-card-text>
            <v-data-table
                :headers="headers"
                :items="list"
                :search="search"
            >
              <template v-slot:item.name="props">
                <v-edit-dialog
                    :return-value.sync="props.item.name"
                    large
                    persistent
                    @save="save"
                    @cancel="cancel"
                    @open="open"
                    @close="close"
                >
                  <div>{{ props.item.name }}</div>
                  <template v-slot:input>
                    <v-text-field
                        v-model="props.item.name"
                        label="eddddddddddd"
                        single-line
                        counter
                        autofocus
                    ></v-text-field>
                  </template>
                </v-edit-dialog>
              </template>
              <template v-slot:item.done="{ item }">
                <v-simple-checkbox
                    v-model="item.done"
                ></v-simple-checkbox>
              </template>
              <template v-slot:item.actions="{ item }">
                <v-icon
                    small
                    @click="deleteItem(item)"
                >
                  mdi-delete
                </v-icon>
              </template>
            </v-data-table>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <h2>* IN ORDER TO EDIT ITEM CLICK ON ITS NAME </h2>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import MyDialog from './MyDialog';

export default {
  name: 'ToDoMain',
  components: {MyDialog},
  data: () => ({
    search: '',
    pagination: {},
    headers: [
      {
        text: 'To Do',
        align: 'start',
        value: 'name',
      },
      {text: 'Done', value: 'done'},
      {text: 'Actions', value: 'actions', sortable: false},
    ],
    list: [],
  }),
  methods: {
    newItem(val) {
      this.list.push(val);
    },
    deleteItem(item) {
      const index = this.list.indexOf(item);
      this.list.splice(index, 1);
    },
    save() {},
    open() {},
    cancel() {},
    close() {},
  },
  created() {
    if (localStorage.getItem('list')) {
      this.list = JSON.parse(localStorage.getItem('list'));
    } else {
      localStorage.setItem('list', JSON.stringify(this.list));
    }
  },
  watch: {
    list: {
      handler: function(val) {
        localStorage.list = JSON.stringify(val);
      },
      deep: true,
    },
  },
};
</script>
