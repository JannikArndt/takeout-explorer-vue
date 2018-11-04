// https://alligator.io/vuejs/file-reader-component/
// https://scotch.io/tutorials/how-to-handle-file-uploads-in-vue-2

<template>
  <div class="col-md-12">
    <div class="container">
      <form enctype="multipart/form-data" novalidate v-if="isInitial || isSaving">
        <div class="dropbox">
          <input type="file" @change="loadTextFromFile" accept="application/json" class="input-file">
        </div>
      </form>
  </div>
</template>

<template>
  <label class="dropbox">
    <input type="file" @change="loadTextFromFile" class="input-file">
  </label>
</template>

<script>
export default {
  methods: {
    loadTextFromFile(ev) {
      const file = ev.target.files[0];
      const reader = new FileReader();

      reader.onload = e => this.$emit("load", e.target.result, e.target);
      reader.readAsText(file);
    }
  }
};
</script>

<style>
.dropbox {
  outline: 2px dashed grey; /* the dash box */
  outline-offset: -10px;
  background: lightcyan;
  color: dimgray;
  padding: 10px 10px;
  min-height: 200px; /* minimum height */
  position: relative;
  cursor: pointer;
  width: 100%;
}

.input-file {
  opacity: 0; /* invisible but it's there! */
  width: 100%;
  height: 200px;
  position: absolute;
  cursor: pointer;
}

.dropbox:hover {
  background: lightblue; /* when mouse over to the drop zone, change color */
}

.dropbox:-moz-drag-over {
  background: lightblue;
}

.dropbox:drop {
  background: lightblue;
}

.dropbox p {
  font-size: 1.2em;
  text-align: center;
  padding: 50px 0;
}
</style>