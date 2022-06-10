<template>
  <v-container fill-height>
    <v-card height="100%" width="100%">
      <v-card-title>
        <v-toolbar color="transparent" elevation="0">
          <v-toolbar-title>KanBan Board</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-btn @click="showAddColumnDialog = true" color="primary" rounded>
            Add Column
            <v-icon right dark> mdi-plus </v-icon>
          </v-btn>
        </v-toolbar>
      </v-card-title>
      <v-card-text>
        <draggable class="row" v-model="columns">
          <v-col v-for="column in columns" :key="column.id" class="tester">
            <column
              :initalTitle="column.title"
              :initialItems="column.items"
            ></column>
          </v-col>
        </draggable>
      </v-card-text>
    </v-card>
    <v-dialog v-model="showAddColumnDialog" width="50%">
      <v-card>
        <v-card-title class="justify-center">
          <span>Add Column</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-divider></v-divider>
            </v-row>
            <v-row>
              <v-col>
                <v-text-field
                  v-model="columnTitle"
                  label="Column Title"
                ></v-text-field>
              </v-col>
            </v-row>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="primary" @click="addColumn()">Save</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
import Column from "@/components/Column";
import draggable from "vuedraggable";
export default {
  components: { Column, draggable },
  name: "BoardComponent",
  data() {
    return {
      columns: [
        {
          id: 1,
          title: "Not Started",
          items: [],
        },
        {
          id: 2,
          title: "In Progress",
          items: [],
        },
        {
          id: 3,
          title: "Completed",
          items: [],
        },
      ],
      showAddColumnDialog: false,
      columnTitle: "",
    };
  },
  methods: {
    addColumn() {
      this.columns.push({ title: this.columnTitle, items: [] });
      this.columnTitle = "";
      this.showAddColumnDialog = false;
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