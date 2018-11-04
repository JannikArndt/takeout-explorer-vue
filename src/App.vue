<template>
  <div id="app">
    <FileReader @load="convert($event)"></FileReader>
    <br>
    <DataTable :file-headers="headers" :file-data="contents"></DataTable>
  </div>
</template>

<script>
import FileReader from "./components/FileReader";
import DataTable from "./components/DataTable.vue";

export default {
  name: "app",
  data: () => ({
    headers: [],
    contents: []
  }),
  components: {
    FileReader,
    DataTable
  },
  methods: {
    convert(rawString) {
      let self = this;
      let lines = rawString.split("\n").filter(item => item);
      self.headers = lines[0].split(",");
      self.contents = lines.slice(1).map(x => x.split(","));
    }
  }
};
</script>