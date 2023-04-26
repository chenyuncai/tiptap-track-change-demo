<script setup lang="ts">
import { Editor, EditorContent } from '@tiptap/vue-3'
import TrackChangeExtension from 'track-change-extension'
import StarterKit from '@tiptap/starter-kit';
import {ref} from 'vue'
const defaultContent = `
<p>
  tiptap is a headless wrapper <insert>around</insert> ProseMirror – a toolkit for building rich text WYSIWYG editors, which is already in use at many well-known companies such as New York Times, The Guardian or Atlassian.</p>
Create exactly the rich text editor you want out of <delete>customizable</delete> building blocks. Tiptap comes with <insert>sensible</insert> defaults, a lot of extensions and a friendly API to customize every aspect. It’s backed by a welcoming community, open source, and free.
`
const trackChangeEnabled = ref(true)
const editor = new Editor({
  content: defaultContent,
  extensions: [
    StarterKit,
    TrackChangeExtension.configure({
      enabled: trackChangeEnabled.value,
      onStatusChange (status: boolean) {
        trackChangeEnabled.value = status
      }
    }),
  ]
})
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
    <EditorContent style="width: 600px;" :editor="editor" />
  </div>

  This is tiptap track change extension.
  <br>

  A ⭐️ to the repo if you 👍 / ❤️ what I'm doing would be much appreciated.
</template>
<style lang="less">
.ProseMirror {
  height: 400px;
  width: 100%;
  border: 1px solid gray;
  text-align: left;
  padding: 10px;
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
}
</style>

