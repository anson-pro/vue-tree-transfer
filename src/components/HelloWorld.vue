<template>
  <div class="hello">
    <el-input v-model="input" placeholder="请输入内容" @focus="showDialog"></el-input>
    <TreeTransferDialog
            :treeData="treeData"
            dialogTitle="选择人员"
            :transferTitle="['源', '目标']"
            :dialogVisible.sync="dialogVisible"
            :handleSubmit="handleSubmit">
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
      treeData,
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

<style lang="less">
</style>
