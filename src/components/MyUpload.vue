<template>
  <div>
    <el-upload
      action="https://jsonplaceholder.typicode.com/posts/"
      list-type="picture-card"
      :on-change="handleChange"
      :on-remove="handleRemove"
      :on-success="handleUpload">
      <i class="el-icon-plus"></i>
    </el-upload>
    <el-dialog :visible.sync="dialogVisible">
      <img width="100%" :src="dialogImageUrl" alt="">
    </el-dialog>
  </div>
</template>

<script>
import emitter from 'element-ui/src/mixins/emitter.js'
  export default {
    data() {
      return {
        dialogImageUrl: '',
        dialogVisible: false
      };
    },
    props: {
      value: {
        // 没有做初始化
        type: String || Array,
        default: '',
      }
    },
    methods: {

      handleChange(file, fileList) {
        this.handleImageList(fileList)
      },
      handleRemove(file, fileList) {
        this.handleImageList(fileList)
      },
      handleUpload(file, fileList) {
        this.handleImageList(fileList)
      },

      handleImageList(fileList) {
        let imageList = []
        fileList.length > 0 && fileList.forEach(item => {
          imageList.push(item.response && item.response.id || item.uid)
        })
        this.$emit('input', imageList.join(','))
        this.dispatch('ElFormItem', 'el.form.change', imageList)
      },

      // elementUI mixins - emitter 中拷贝的
      dispatch(componentName, eventName, params) {
        var parent = this.$parent || this.$root;
        var name = parent.$options.componentName;

        while (parent && (!name || name !== componentName)) {
          parent = parent.$parent;

          if (parent) {
            name = parent.$options.componentName;
          }
        }
        if (parent) {
          parent.$emit.apply(parent, [eventName].concat(params));
        }
      },
    }
  }
</script>
