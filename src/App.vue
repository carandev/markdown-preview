<script setup>
import { ref } from 'vue'
import { marked } from 'marked'

const data = ref('')
const preview = ref('')
const md = ref('')

function markdownToHtml() {
  const element = preview.value

  element.scrollTo(0, element.scrollHeight)

  md.value = marked.parse(data.value)
}

</script>

<template>
  <header class="header">
    <h1>Mardown Previewer</h1>
  </header>
  <main class="main">
    <section class="section">
      <h2>Mardown</h2>
      <textarea 
        class="textarea"
        v-model="data"
        @input="markdownToHtml"
        placeholder="Write anything"
        spellcheck="false"
      />
    </section>
    <section class="section">
      <h2>Preview</h2>
      <div ref="preview" class="preview" v-html="md"></div>
    </section>
  </main>
</template>

<style scoped>
.header {
  background-color: #223;
  color: #eee;
  padding: 1rem 0;
}
.header h1 {
  margin: 0;
  text-align: center;
}
.main {
  display: flex;
  gap: 9rem;
  justify-content: center;
  flex-wrap: wrap;
  color: #eee;
  padding: 2rem;
}
.textarea {
  resize: none;
  width: 100%;
  height: 85%;
  border: none;
  background-color: #112;
  border: 1px solid #159;
  color: #eee;
  outline: none;
  padding: 1rem;
  font-family: sans-serif;
}
.section {
  width: 40vw;
  height: 75vh;
  overflow: hidden;
}
.preview {
  height: 85%;
  overflow-y: scroll;
}

@media screen and (max-width: 1040px) {
  .section {
    width: 80vw;
  }
}
</style>
