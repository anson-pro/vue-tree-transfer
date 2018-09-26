<template>
  <div class="hello">
    <el-button type="primary" @click="showDialog">Show</el-button>
    <TreeTransferDialog
            title="选择人员"
            :dialogVisible.sync="dialogVisible"
            :handleSubmit="handleSubmit"
    />
  </div>
</template>

<script>
  import TreeTransferDialog from './TreeTransferDialog';

  export default {
    name: 'HelloWorld',
    components: {
      TreeTransferDialog,
    },
    data() {
      return {
        dialogVisible: false,
      };
    },
    methods: {
      showDialog() {
        this.dialogVisible = true;
      },
      handleSubmit() {
        this.dialogVisible = false;
      },
    },
  };
</script>

<style scoped>

</style>
