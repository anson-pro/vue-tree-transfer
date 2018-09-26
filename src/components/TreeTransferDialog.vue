<template>
  <div class="tree-transfer-dialog">
    <el-dialog
            :title="title"
            :visible.sync="visible"
            width="30%">
      <button type="button" aria-label="Close" class="el-dialog__headerbtn" @click.stop="handleCancel">
        <i class="el-dialog__close el-icon el-icon-close"></i>
      </button>
      <span>需要注意的是内容是默认不居中的</span>
      <span slot="footer" class="dialog-footer">
        <el-button size="mini" type="primary" @click="handleSubmit">确 定</el-button>
        <el-button size="mini" @click="handleCancel">取 消</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
  export default {
    name: 'TreeTransferDialog',
    props: {
      title: {
        type: String,
        default: 'Title'
      },
      dialogVisible: {
        type: Boolean,
        default: false,
        required: true,
      },
      handleSubmit: {
        type: Function,
        required: true,
      },
    },
    computed: {
      visible: function() {
        return this.dialogVisible;
      },
    },
    data() {
      return {};
    },
    methods: {
      handleCancel() {
        this.$emit('update:dialogVisible', false);
      },
    },
  };
</script>

<style>
  .tree-transfer-dialog .el-dialog__footer {
    text-align: center;
  }
</style>