<template>
  <div class="hello">
    <el-input
            :value="value"
            placeholder="请输入内容"
            @focus="showDialog"
            readonly></el-input>
    <TreeTransferDialog
            :treeData="treeData"
            dialogTitle="选择人员"
            :transferTitle="['源', '目标']"
            :dialogVisible="dialogVisible"
            @close="handleClose"
            @submit="handleSubmit">
    </TreeTransferDialog>
  </div>
</template>

<script>
import treeData from '../static/data.json';
import TreeTransferDialog from './TreeTransferDialog.vue';

export default {
  name: 'HelloWorld',
  components: {
    TreeTransferDialog,
  },
  data() {
    return {
      dialogVisible: false,
      input: '',
      value: '',
      treeData,
    };
  },
  methods: {
    handleClose() {
      this.dialogVisible = false;
    },
    showDialog() {
      this.dialogVisible = true;
    },
    handleSubmit(newValue) {
      this.value = newValue;
    },
  },
};
</script>

<style lang="less">
</style>
