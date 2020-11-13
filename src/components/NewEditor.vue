<template>
  <div class="container">
    <div id="bar">
      <button @click="saveDesign">Save Design</button>
      <button @click="exportHtml">Export HTML</button>
    </div>
    <EmailEditor
      class="email-new-editor"
      locale="ru-RU"
      ref="editor"
      :tools="tools"
      @load="editorLoaded" />
  </div>
</template>

<script>
import EmailEditor from './editor/EmailEditor.vue';
import sample from './sample.json';
  
  export default {
    name: 'new-editor',
    components: {
      EmailEditor
    },
    props: [
      "template"
      ],
    data() {
      return {
        locTemplate: sample,
        tools: {
          html: {
            properties: {
                html: {
                value: '<strong>Hello, world! Test</strong>'
              }
            }
          }
        }
      }
    },
    mounted() {
    },
    methods: {
      editorLoaded() {
        this.locTemplate.body.rows[0].columns[0].contents[0].values.html = this.template;
        this.$refs.editor.loadDesign(this.locTemplate);
      },
      saveDesign() {
        this.$refs.editor.saveDesign(design => {
            console.log(this.locTemplate.body.rows[0].columns[0].contents[0].values.html);
            console.log('saveDesign', design);
            // console.log(JSON.stringify(design));
          }
        )
      },
      exportHtml() {
        this.$refs.editor.exportHtml(data => {
            // this.locTemplate = data;
            // this.locTemplate.html = this.template;
            console.log('exportHtml', data);
            console.log(data.html);
          }
        )
      }
      // TO DO - for email remove preview - it already exists in new library
      // make save title in email markup
    }
  }
</script>

<style lang="scss">
.email-new-editor {
  height: 900px;
}
</style>