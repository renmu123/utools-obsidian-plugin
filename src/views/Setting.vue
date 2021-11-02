<!--  -->
<template>
  <form>
    <div>
      <label>库名称：</label
      ><input v-model="form.vault" placeholder="请输入库名称" required />
    </div>
    <button @click="submit">提交</button>
  </form>
</template>

<script>
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
      utools.dbStorage.setItem("vault", this.form.vault);
      console.log(utools.dbStorage.getItem("vault"), this.form.vault);
    },
  },
};
</script>
<style scoped></style>
