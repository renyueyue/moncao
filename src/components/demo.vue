<template>
  <div>
    语言：
    <el-select
      v-model="opts.language"
      clearable
      placeholder="请选择"
      size="mini"
      @change="changeLanguage"
    >
      <el-option
        v-for="item in sets.language"
        :key="item"
        :label="item"
        :value="item"
      >
      </el-option>
    </el-select>
    样式风格：
    <el-select
      v-model="opts.theme"
      clearable
      placeholder="请选择"
      size="mini"
      @change="changeTheme"
    >
      <el-option
        v-for="item in sets.theme"
        :key="item"
        :label="item"
        :value="item"
      >
      </el-option>
    </el-select>
    <el-button type="primary" size="mini" @click="getValue">获取内容</el-button>
    <!--调用子组件-->
    <monaco-editor ref="monacos" :opts="opts"></monaco-editor>
    <!--@change="changeValue"-->
  </div>
</template>

<script>
import monacoEditor from "./monacoEditor";

export default {
  components: {
    monacoEditor,
  },
  data() {
    return {
      sets: {
        language: {
          bat: "bat",
          html: "html",
          javascript: "javascript",
          json: "json",
          mysql: "mysql",
          perl: "perl",
          python: "python",
          powershell: "powershell",
          shell: "shell",
          sql: "sql",
        },
        theme: {
          vs: "vs",
          "vs-dark": "vs-dark",
          "hc-black": "hc-black",
        },
      },
      opts: {
        value: "<div>123</div>",
        readOnly: false, // 只读
        language: "html", // 语言
        height: 100,
        width: 100,
        theme: "vs-dark", // 编辑器主题
        autoIndent: true, //自动布局
        fontSize: 20, // 字体大小
      },
    };
  },

  methods: {
    changeLanguage(val) {
      this.opts.language = val;
      this.$refs.monacos.destroyEditor();
    },
    changeTheme(val) {
      this.opts.theme = val;
      this.$refs.monacos.destroyEditor();
    },
    // 手动获取值
    getValue() {
      console.log(this.$refs.monacos);
      this.$message.info(this.$refs.monacos.getVal());
    },
    // 内容改变自动获取值
    changeValue(val) {
      console.log(val, 94);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>