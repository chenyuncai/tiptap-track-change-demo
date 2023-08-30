<script setup lang="ts">
import { Editor, EditorContent } from '@tiptap/vue-3'
import TrackChangeExtension from 'track-change-extension'
// import TrackChangeExtension from './source'
import StarterKit from '@tiptap/starter-kit';

import * as Y from 'yjs'
// import { IndexeddbPersistence } from 'y-indexeddb'
import Collaboration from '@tiptap/extension-collaboration'
import {ref} from 'vue'

const ydoc = new Y.Doc()

// Store the Y document in the browser
// new IndexeddbPersistence('example-document', ydoc)

// Or another provider like a central hocuspocus(y-websocket powered) server or webRtc

// With P2P Provider, the init content need to be set with some provider like a central hocuspocus server.

const defaultContent = `
  <p>tiptap is a headless wrapper <insert data-op-user-id="123">around</insert> ProseMirror – a toolkit for building rich text WYSIWYG editors, which is already in use at many well-known companies such as New York Times, The Guardian or Atlassian.</p>
  <p>Create exactly the rich text editor you want out of <delete>customizable</delete> building blocks.</p>
`

const trackChangeEnabled = ref(true)

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
    <div style="display: flex; gap: 10px; flex-direction: flex-row; justify-content: flex-start; padding: 10px 0;">
      <button @click="editor.commands.toggleTrackChangeStatus()">Toggle Track:  {{ trackChangeEnabled }}</button>
    </div>
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

