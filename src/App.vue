<script setup lang="ts">
import MyEditor from './components/MyEditor.vue'
</script>

<template>
  <h3>
    Tiptap2 - Track Change Extension
    <a target="_blank" href="https://github.com/chenyuncai/tiptap-track-change-extension">
      <img style="vertical-align: middle; margin: 0 10px;border-radius: 6px;" src="./assets/githublog.svg">
      <span>Repository</span>
    </a>
  </h3>
  <h6>Mark the deleted content as red and new content as green. </h6>
  <div>
    <MyEditor style="width: 700px;" />
  </div>

  This is tiptap track change extension.
  <br>

  A ⭐️ to the repo if you 👍 / ❤️ what I'm doing would be much appreciated.
</template>
<style lang="less">
.ProseMirror {
  height: max-content;
  min-height: 400px;
  width: 100%;
  border: 1px solid gray;
  text-align: left;
  padding: 10px;
  box-sizing: border-box;
  overflow: auto;
  margin-bottom: 30px;

  &-focused {
    border: 1px solid gray;
    outline: none;
  }

  p {
    margin: 0;
  }

  insert {
    color: green;
    text-decoration: underline;
  }

  delete {
    color: red;
    text-decoration: line-through;
  }
}</style>

