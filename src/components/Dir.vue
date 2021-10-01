<template>
  <div id="container">
    <p class="fileItem" v-for="file in dir" :key="file.name" v-on:click="enterDirectoryOrDisplayContent(file, file.children)">{{ file.name }}</p>
  </div>
</template>

<script lang="ts">

import { Vue } from 'vue-class-component';
import { fs } from "@tauri-apps/api";
import { homeDir } from "@tauri-apps/api/path";

export default class Dir extends Vue {

  public homeDirectory: any = "";
  public dir: any = "";
  public fileContent: any = "";

  async mounted () {
    this.homeDirectory = await homeDir();
    this.dir = await fs.readDir(this.homeDirectory);
  }

  async enterDirectoryOrDisplayContent(file: any, hasChildren: boolean) {
    if (hasChildren) {
      this.dir = await fs.readDir(file.path);
    }
    else {
      this.fileContent = await fs.readTextFile(file.path);
      this.$emit("sendFileContent", this.fileContent);
    }
  }
}
</script>

<style>
.fileItem:hover {
  background-color: black;
  color: white;
  cursor: pointer;
}
</style>

function homeDir(): any {
  throw new Error('Function not implemented.');
}

function homeDir(): any {
  throw new Error('Function not implemented.');
}
