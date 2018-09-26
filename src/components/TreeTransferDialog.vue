<template>
  <div class="tree-transfer" :style="{width,height}">
    <el-dialog
            :title="dialogTitle"
            :visible.sync="visible"
            :before-close="modalClose"
            class="tree-transfer__dialog">
      <section class="tree-transfer__content">
        <div class="tree-transfer__left">
          <h3 class="tree-transfer__title">
            {{ sourceTitle }}
          </h3>
          <div class="tree-transfer__list">
            <el-tree
                    ref="tree"
                    :data="treeData"
                    :node-key="nodeKey"
                    :props="defaultProps"
                    :highlight-current="true"
                    :expand-on-click-node="false">
            </el-tree>
          </div>
        </div>
        <div class="tree-transfer__middle">
          <el-button
                  type="primary"
                  icon="el-icon-arrow-right"
                  circle
                  @click="handleAdd">
          </el-button>
        </div>
        <div class="tree-transfer__right">
          <h3 class="tree-transfer__title">
            <span>{{ targetTitle }}</span>
            <span class="tree-transfer__right-close">清空</span>
          </h3>
          <div class="tree-transfer__list">
            <ul class="tree-transfer__list-ul">
              <li class="tree-transfer__list-li" v-for="item of targetNodes" :key="item[nodeKey]">
                <label>{{item[defaultProps.label]}}</label>
                <span class="tree-transfer__list-delete"
                   @click="handleDeleteItem(item[nodeKey])">删除</span>
              </li>
            </ul>
          </div>
        </div>
      </section>
      <span slot="footer" class="dialog-footer">
        <el-button size="mini" type="primary" @click="handleSubmit">确定</el-button>
        <el-button size="mini" @click="modalClose">取消</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
export default {
  name: 'TreeTransferDialog',
  props: {
    // 宽度
    width: {
      type: String,
      default: '500px',
    },
    // 高度
    height: {
      type: String,
      default: '1000px',
    },
    // 树形列表数据
    treeData: {
      type: Array,
      default: () => [],
    },
    // dialog 标题
    dialogTitle: {
      type: String,
      default: 'Title',
    },
    // transfer 标题
    transferTitle: {
      type: Array,
      default: () => ['源列表', '目标列表'],
    },
    nodeKey: {
      type: String,
      default: 'id',
    },
    defaultProps: {
      type: Object,
      default: () => ({ label: 'label', children: 'children' }),
    },
    // dialog 显示状态
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
  data() {
    return {
      visible: false,
      targetNodes: [
        {
          id: 2,
          label: '华北一区',
          disabled: true,
        },
        {
          id: 3,
          label: '华北二区',
          disabled: true,
        },
      ],
    };
  },
  computed: {
    sourceTitle() {
      return this.transferTitle[0];
    },
    targetTitle() {
      return this.transferTitle[1];
    },
  },
  watch: {
    dialogVisible(newValue) {
      this.visible = newValue;
    },
  },
  created() {
    this.visible = this.dialogVisible;
  },
  methods: {
    handleAdd() {
      console.log(this.$refs.tree.getCurrentKey());
    },
    handleDeleteItem() {

    },
    modalClose() {
      this.$emit('close');
      this.visible = false;
    },
  },
};
</script>

<style lang="less">
  .tree-transfer {
    h3, ul, li {
      margin: 0;
      padding: 0;
    }

    .tree-transfer__content {
      position: relative;
      overflow: hidden;
      height: 400px;

      .tree-transfer__title {
        border-bottom: 1px solid #ebeef5;
        padding: 0 15px;
        height: 40px;
        line-height: 40px;
        color: #333;
        font-size: 16px;
        background-color: #f5f7fa;
      }

      .tree-transfer__list {
        padding: 10px;
        height: calc(100% - 41px);
        box-sizing: border-box;
        overflow: auto;
      }

      .tree-transfer__left {
        position: absolute;
        top: 0;
        left: 0;
      }

      .tree-transfer__middle {
        position: absolute;
        top: 50%;
        left: 40%;
        width: 20%;
        transform: translateY(-50%);
        text-align: center;
      }

      .tree-transfer__right {
        position: absolute;
        top: 0;
        right: 0;

        .tree-transfer__right-close {
          float: right;
          color: #67c23a;
          font-size: 14px;
          cursor: pointer;
        }

        .tree-transfer__list-ul {
          padding-bottom: 20px;
        }

        .tree-transfer__list-li {
          position: relative;
          padding: 4px 24px 4px 10px;
          border-radius: 3px;
          overflow: hidden;
          white-space: nowrap;
          text-overflow: ellipsis;
        }

        .tree-transfer__list-li:hover {
          background-color: #f5f7fa;
        }

        .tree-transfer__list-li:hover .tree-transfer__list-delete {
          display: block;
        }

        .tree-transfer__list-delete {
          display: none;
          position: absolute;
          top: 50%;
          right: 10px;
          margin-top: -10px;
          color: #f56c6c;
          cursor: pointer;
          text-align: center;
        }
      }

      .tree-transfer__left,
      .tree-transfer__right {
        border: 1px solid #ebeef5;
        width: 40%;
        height: 100%;
        box-sizing: border-box;
        border-radius: 5px;
        vertical-align: middle;
      }
    }
    .el-dialog__footer {
      text-align: center;
    }

  }
</style>
