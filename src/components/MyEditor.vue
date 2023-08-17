<script setup lang="ts">
import { Editor, EditorContent } from '@tiptap/vue-3'
import TrackChangeExtension from 'track-change-extension'
import StarterKit from '@tiptap/starter-kit';

import * as Y from 'yjs'
import { IndexeddbPersistence } from 'y-indexeddb'
import Collaboration from '@tiptap/extension-collaboration'
import {ref} from 'vue'

const ydoc = new Y.Doc()

// Store the Y document in the browser
new IndexeddbPersistence('example-document', ydoc)

// With P2P Provider, the init content need to be set with some provider like a central hocuspocus server.
const defaultContent = ``
const trackChangeEnabled = ref(false)

const editor = new Editor({
  content: defaultContent,
  extensions: [
    StarterKit.configure({
      history: {
        depth: 100,
        newGroupDelay: 1000
      }
    }),
    TrackChangeExtension.configure({
      enabled: trackChangeEnabled.value,
      onStatusChange (status: boolean) {
        trackChangeEnabled.value = status
      },
      dataOpUserId: Math.random().toString(36).substr(2, 5),
      dataOpUserNickname: 'Nickname1'
    }),
    Collaboration.configure({
      document: ydoc,
    }) as any
  ]
})
</script>

<template>
  <div>
    <EditorContent style="width: 100%;" :editor="editor" />
  </div>
</template>
<style lang="less">
.ProseMirror {
  height: 100px;
  width: 100%;
  border: 1px solid gray;
  text-align: left;
  padding: 10px;
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
}
</style>

