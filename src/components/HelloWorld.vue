<template>
  <v-container>
    <v-layout text-xs-center wrap>
      <v-container app>
        <v-layout>
          <v-flex style="margin-right: 8px;">
            <v-text-field label="Name" v-model="info.name"></v-text-field>
          </v-flex>

          <v-flex>
            <v-text-field label="Phone" v-model="info.phone"></v-text-field>
          </v-flex>
          <v-btn @click="addPersonInfo">{{ btnText }}</v-btn>
        </v-layout>
      </v-container>

      <v-container>
        <v-list two-line v-if="persons.length">
          <v-list-tile v-for="(person, i) in persons" :key="i">
            <v-list-tile-content>
              <v-list-tile-title>{{ person.name }}</v-list-tile-title>
              <v-list-tile-sub-title>{{ person.phone }}</v-list-tile-sub-title>
            </v-list-tile-content>

            <v-list-tile-action>
              <v-layout>
                <v-btn @click="changePersonInfo(i)">📝</v-btn>
                <v-btn @click="deletePersonInfo(i)">❌</v-btn>
              </v-layout>
            </v-list-tile-action>
          </v-list-tile>
          <v-divider></v-divider>
        </v-list>
      </v-container>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  data: () => ({
    change: false,
    btnText: "Add",
    persons: [],
    info: {
      name: "",
      phone: ""
    }
  }),

  methods: {
    addPersonInfo: function() {
      if (this.change) {
        this.info = {
          name: "",
          phone: ""
        };
        this.change = false;
        this.btnText = "Add";
      } else {
        if (this.info.name && this.info.phone) {
          let obj = {
            name: this.info.name,
            phone: this.info.phone
          };
          this.persons.push(obj);
        }

        this.info.name = "";
        this.info.phone = "";
      }
    },

    deletePersonInfo: function(id) {
      this.persons.splice(id, 1);
    },

    changePersonInfo: function(id) {
      this.info = this.persons[id];
      this.change = true;
      this.btnText = "Change";
    }
  }
};
</script>

<style>
</style>
