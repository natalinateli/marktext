<template>
  <div class="editor-container">
    <title-bar
      :pathname="pathname"
      :filename="filename"
      :active="windowActive"
      :word-count="wordCount"
      :theme="theme"
      :platform="platform"
      :is-saved="isSaved"
    ></title-bar>
    <editor
      :typewriter="typewriter"
      :focus="focus"
      :source-code="sourceCode"
      :markdown="markdown"
      :cursor="cursor"
      :theme="theme"
      :dark-color="darkColor"
      :light-color="lightColor"
      :line-height="lineHeight"
      :font-size="fontSize"
      :editor-font-family="editorFontFamily"
    ></editor>
    <source-code
      v-if="sourceCode"
      :markdown="markdown"
      :cursor="cursor"
      :theme="theme"
    ></source-code>
    <bottom-bar
      :source-code="sourceCode"
      :theme="theme"
    ></bottom-bar>
    <aidou></aidou>
    <upload-image></upload-image>
    <about-dialog></about-dialog>
    <font></font>
    <rename></rename>
  </div>
</template>

<script>
  import Editor from '@/components/editor'
  import TitleBar from '@/components/titleBar'
  import BottomBar from '@/components/bottomBar'
  import SourceCode from '@/components/sourceCode'
  import Aidou from '@/components/aidou/aidou'
  import UploadImage from '@/components/uploadImage'
  import AboutDialog from '@/components/about'
  import Font from '@/components/font'
  import Rename from '@/components/rename'
  import { mapState } from 'vuex'

  export default {
    name: 'marktext',
    components: {
      Aidou,
      Editor,
      TitleBar,
      BottomBar,
      SourceCode,
      UploadImage,
      AboutDialog,
      Font,
      Rename
    },
    data () {
      return {}
    },
    computed: {
      ...mapState([
        'pathname', 'filename', 'isSaved', 'windowActive', 'wordCount',
        'typewriter', 'focus', 'sourceCode', 'markdown', 'preferLooseListItem',
        'cursor', 'theme', 'platform', 'lightColor', 'darkColor', 'fontSize', 'lineHeight', 'editorFontFamily'
      ])
    },
    created () {
      const { dispatch } = this.$store

      dispatch('ASK_FOR_USER_PREFERENCE')
      dispatch('ASK_FOR_MODE')
      dispatch('LISTEN_FOR_CLOSE')
      dispatch('LISTEN_FOR_SAVE_AS')
      dispatch('LISTEN_FOR_MOVE_TO')
      dispatch('LINTEN_WIN_STATUS')
      dispatch('LISTEN_FOR_SAVE')
      dispatch('GET_FILENAME')
      dispatch('LISTEN_FOR_FILE_LOAD')
      dispatch('LISTEN_FOR_FILE_CHANGE')
      dispatch('LISTEN_FOR_EDIT')
      dispatch('LISTEN_FOR_VIEW')
      dispatch('LISTEN_FOR_EXPORT')
      dispatch('LISTEN_FOR_PARAGRAPH_INLINE_STYLE')
      dispatch('LISTEN_FOR_UPDATE')
      dispatch('LISTEN_FOR_INSERT_IMAGE')
      dispatch('LISTEN_FOR_ABOUT_DIALOG')
      dispatch('LISTEN_FOR_RENAME')
      dispatch('LISTEN_FOR_IMAGE_PATH')
      dispatch('LISTEN_FOR_FILE_SAVED_SUCCESSFULLY')
      dispatch('LINTEN_FOR_SET_LINE_ENDING')
      dispatch('LISTEN_FOR_NOTIFICATION')
    }
  }
</script>

<style>
  .editor-container {
    padding-top: 22px;
  }
  .editor-container .hide {
    z-index: -1;
    opacity: 0;
    position: absolute;
    left: -10000px;
  }
</style>
