<template>
  <v-container>
    <v-card color="grey lighten-3" height="100%">
      <v-card-title class="justify-center">
        <v-toolbar color="transparent" elevation="0">
          <v-toolbar-title>{{ title }}</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-text-field
            v-model="search"
            hide-details
            placeholder="Search"
            prepend-icon="mdi-magnify"
            single-line
          ></v-text-field>
          <v-spacer></v-spacer>
          <v-btn @click="showAddItemDialog = true"  class="mx-2" small color="primary" icon>
            <v-icon> mdi-plus </v-icon>
          </v-btn>
        </v-toolbar>
      </v-card-title>
      <v-card-text min-height="10%">
        <draggable :list="items" group="same">
          <v-row v-for="item in filteredItems" :key="item.title">
            <v-col cols="12">
              <Item :initialTitle="item.title" :initialNote="item.note" :initialColor="item.color"/>
            </v-col>
          </v-row>
        </draggable>
      </v-card-text>
    </v-card>
    <v-dialog v-model="showAddItemDialog" width="50%">
      <v-card>
        <v-card-title class="justify-center">
          <span>Add Item</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-divider></v-divider>
            </v-row>
            <v-row>
              <v-col>
                <v-text-field
                  v-model="itemTitle"
                  label="Item Title"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col>
                <v-text-field
                  v-model="itemNote"
                  label="Item Note"
                ></v-text-field>
              </v-col>
            </v-row>
            <v-row>
              <v-col>
                <v-autocomplete
                
                  v-model="itemColor"
                  :items="colors"
                  item-value="value"
                  item-text="name"
                  label="Color"
                ></v-autocomplete>
              </v-col>
            </v-row>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="primary" @click="addItem()">Save</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
import Item from "@/components/Item.vue";
import draggable from "vuedraggable";
export default {
  components: {
    Item,
    draggable,
  },
  name: "ColumnComponent",
  props: {
    initialItems: {
      type: Array,
    },
    initalTitle: {
      type: String,
      default: "Placeholder",
    },
  },
  watch: {
    search(newValue) {
      console.log(newValue);
      this.filteredItems = this.items.filter((item) => {
        return item.title.toLowerCase().includes(this.search.toLowerCase());
      });
    },
    items() {
      this.filteredItems = this.items.filter((item) => {
        return item.title.toLowerCase().includes(this.search.toLowerCase());
      });
    },
  },
  data() {
    return {
      title: this.initalTitle,
      items: this.initialItems,
      filteredItems: this.initialItems,
      search: "",
      itemTitle: "",
      itemNote: "",
      itemColor: "",
      showAddItemDialog: false,
      colors: [
          {value: "blue", name: "Blue"},
          {value: "red", name: "Red"},
          {value: "green", name: "Green"},
          {value: "yellow", name: "Yellow"},
      ]
    };
  },
  methods: {
    addItem() {
      this.items.push({ title: this.itemTitle, note: this.itemNote, color: this.itemColor });
      this.itemTitle = "";
      this.itemNote = "";
      this.itemColor = "";
      this.showAddItemDialog = false;
    },
  },
};
</script>

<style lang="scss" scoped>
.flip-list-move {
  transition: transform 0.5s;
}
.no-move {
  transition: transform 0s;
}
.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}
.list-group {
  min-height: 20px;
}
.list-group-item {
  cursor: move;
}
.list-group-item i {
  cursor: pointer;
}
</style>