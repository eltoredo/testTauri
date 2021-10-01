<template>
  <div id="container" class="flex-container">
    <Dir
    height="300"
    width="300"
    v-on:sendFileContent="setValue"
    >
    </Dir>

    <MonacoEditor
      height="600"
      language="javascript"
      :code="code"
      :editorOptions="options"
      @mounted="onMounted"
      @codeChange="onCodeChange"
      @setValue="setValue"
    >
    </MonacoEditor>

  </div>
</template>

<script lang="ts">

import { Options, Vue } from 'vue-class-component';
import Dir from './components/Dir.vue';
import MonacoEditor from 'vue-monaco-editor'

@Options({
  components: {
    Dir,
    MonacoEditor
  },
})
export default class App extends Vue {

  public editor: any = "";
  public fileContent: any = "";

  onMounted(editor: any) {
    this.editor = editor;
  }

  setValue(fileContent: string) {
    this.editor.setValue(fileContent);
  }

}
</script>

<style>
.flex-container {
  display: flex;
  justify-content: space-between;
}
</style>
