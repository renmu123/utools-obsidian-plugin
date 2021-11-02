<!--  -->
<template>
  <div class=""></div>
</template>

<script>
import router from "../router";

export default {
  components: {},
  setup() {},
  data() {
    return {};
  },
  created() {},
  mounted() {
    const utools = window.utools;

    utools.onPluginReady(() => {
      console.log("插件装配完成，已准备好");

      // 插件第一次访问，如果vault为空，自动跳转至设置页
      if (!utools.db.get("vault")) {
        router.push("Setting");
      }
    });

    utools.onPluginEnter(({ code, type, payload }) => {
      console.log("用户进入插件", code, type, payload);
      if (code === "ob-setting") {
        router.push("Setting");
      } else {
        utools.setExpendHeight(0);
        utools.setSubInput(({ text }) => {
          document.addEventListener("keydown", (event) => {
            if (event.code === "Enter") {
              const encodeSearchWord = encodeURI(text);
              const vault = utools.dbStorage.getItem("vault");
              utools.shellOpenExternal(
                `obsidian://search?vault=${vault}&query=${encodeSearchWord}`
              );
              utools.hideMainWindow();
            }
          });
        }, "请输入需要搜索的文本");
      }
    });
  },
  computed: {},
  watch: {},
  methods: {},
};
</script>
<style scoped></style>
