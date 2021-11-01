<template>
  <div id="app">
    <div class="office">
      <Map
        @tableClicked="showPersonInfo"
        @notTableClicked="hidePersonInfo"
        :legend="legend"
        :tables="tables"
      />
      <SideMenu :legend="legend" :person="person" :isUserOpenned.sync="isUserOpenned" />
    </div>
  </div>
</template>

<script>
import Map from "./components/Map.vue";
import SideMenu from "./components/SideMenu.vue";
import legend from "@/assets/data/legend.json";
import tables from "@/assets/data/tables.json";
import peoples from "@/assets/data/people.json";

export default {
  name: "App",
  data() {
    return {
      legend: legend,
      tables: tables,
      person: null,
      isUserOpenned: false,
    };
  },
  components: {
    Map,
    SideMenu,
  },
  created() {
    this.legend.forEach((legendItem) => {
      legendItem.counter = this.tables.filter(
        (tableItem) => tableItem.group_id === legendItem.group_id
      ).length;
    });
  },
  methods: {
    showPersonInfo(id) {
      this.person = peoples.find((people) => people.tableId === id) ?? null;

      this.isUserOpenned = true;
    },

    hidePersonInfo() {
      this.isUserOpenned = false;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
  background-color: #fafafa;
  padding: 24px;
  box-sizing: border-box;
}

html,
body,
#app {
  height: 100%;
}

* {
  box-sizing: border-box;
}

h3 {
  margin-top: 0px;
}

.office {
  display: grid;
  grid-template-columns: 1fr 320px;
  border-radius: 6px;
  border: 1px solid #ccd8e4;
  height: 100%;
  background: white;
  max-width: 1500px;
  margin: 0 auto;
}
</style>
