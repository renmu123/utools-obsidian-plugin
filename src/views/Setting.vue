<!--  -->
<template>
  <el-form ref="form" :model="form" label-width="120px">
    <el-form-item
      label="库名称"
      :rules="[{ required: true, message: '请填写库名称' }]"
    >
      <el-input
        v-model="form.vault"
        placeholder="请输入库名称"
        required
      ></el-input>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" @click="submit">保存</el-button>
    </el-form-item>
  </el-form>
</template>

<script>
import { ElMessage } from "element-plus";

const utools = window.utools;

export default {
  components: {},
  setup() {},
  data() {
    return {
      form: {
        vault: "",
      },
    };
  },
  created() {},
  mounted() {
    if (utools.dbStorage.getItem("vault")) {
      this.form.vault = utools.dbStorage.getItem("vault");
    }
  },
  computed: {},
  watch: {},
  methods: {
    submit() {
      if (this.form.vault === "") {
        ElMessage.error("请填写库名称");
      } else {
        ElMessage({
          message: "保存成功，你现在可以尝试搜索了，窗口将在3秒后关闭",
          type: "success",
        });
        utools.dbStorage.setItem("vault", this.form.vault);
        setTimeout(() => {
          utools.hideMainWindow();
        }, 3000);
      }

      console.log(utools.dbStorage.getItem("vault"), this.form.vault);
    },
  },
};
</script>
<style scoped></style>
