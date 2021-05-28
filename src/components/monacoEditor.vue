<template>
  <div>
    <div ref="monaco" class="monaco"></div>
  </div>
</template>

<script>
import * as monaco from "monaco-editor";

export default {
  props: {
    opts: {
      type: Object,
      default() {
        return {};
      },
    },
  },
  data() {
    return {
      monacoEditor: null,
      defaultOpts: {
        value: "", // 编辑器的值
        theme: "vs-dark", // 编辑器主题：vs, hc-black, or vs-dark，更多选择详见官网
        roundedSelection: false, // 右侧不显示编辑器预览框
        autoIndent: true, // 自动缩进
      },
      editorOptions: {},
    };
  },
  mounted() {
    this.initEditor();
  },
  watch: {
    opts: {
      handler() {
        this.initEditor();
      },
      deep: true,
    },
  },
  methods: {
    initEditor() {
      this.editorOptions = Object.assign(this.defaultOpts, this.opts);
      // 初始化编辑器，确保dom已经渲染
      this.monacoEditor = monaco.editor.create(
        this.$refs.monaco,
        this.editorOptions
      );
      // 编辑器内容发生改变时触发
      this.monacoEditor.onDidChangeModelContent(() => {
        this.$emit("change", this.monacoEditor.getValue());
      });
    },

    getVal() {
      return this.monacoEditor.getValue(); //获取编辑器中的文本
    },
    destroyEditor() {
      // 销毁编辑器
      this.monacoEditor.dispose();
    },
  },
  beforeDestroy() {
    this.destroyEditor();
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.monaco {
  width: 100%;
  height: 300px;
  text-align: left;
  border: 1px solid #ccc;
}
</style>
