<template>
  <div>
    <!-- 数据遍历 -->
     <table>
      <thead>
        <tr>
          <th>名称</th>
          <th>类型</th>
          <th>颜色</th>
        </tr>
      </thead>
      <tbody>
    <tr v-for="(item, index) of Object.entries(color)" :key="item[0]">
      <td>{{ item[1].text }}</td>
      <td>{{ item[1].type }}</td>
      <td>{{ item[1].value }}</td>
      <el-button type="success" @click="editBtn_C(index)"
        >修改</el-button
      >
    </tr>
</tbody>
</table>

    <!-- 修改信息的弹框 -->
    <el-dialog title="修改信息" :visible.sync="dialogVisible_C" width="50%">
      <el-form ref="form" :model="form_C" label-width="80px">
        <el-form-item label="名称">
          <el-input v-model="form_C.text"></el-input>
        </el-form-item>
        <el-form-item label="类型">
          <el-select
            v-model="form_C.type"
            placeholder="请选择活动区域"
            disabled
          >
            <el-option label="color" value="color"></el-option>
            <el-option label="image" value="image"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="颜色">
          <div class="block">
            <el-color-picker v-model="form_C.value"></el-color-picker>
          </div>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="cancal_C()">取 消</el-button>
        <el-button type="primary" @click="submit_C()">确 定</el-button>
      </span>
    </el-dialog>
  </div>
</template>
<script>

export default {
  data() {
    return {
      color: {
        themeHighlightPrimary: {
          type: "color",
          text: "主题⾊-⾼亮⾊",
          value: "#C1422F",
        },
        theme_bg_bottom: {
          type: "color",
          text: "背景底部⾊",
          value: "#FF752B",
        },
        theme_bg_color: {
          type: "color",
          text: "背景底部⾊",
          value: "#FF752B",
        },
      },
      dialogVisible_C: false,
      form_C: {
        text: "",
        type: "",
        value: "",
      },
      oldform_C: null,
      index_C: "",
      map_C:null
    };
  },
  mounted(){
    //  使用一个map集合,用于检测哪条数据被修改
      this.map_C = new Map();
      this.map_C.set(0,'themeHighlightPrimary');
      this.map_C.set(1,'theme_bg_bottom');
      this.map_C.set(2,'theme_bg_color');
  },
  methods: {
    editBtn_C(index) {
      // 深拷贝一份修改之前的数据
      this.oldform_C = JSON.parse(JSON.stringify(this.color[this.map_C.get(index)]));
      // 记录被修改的索引值
      this.index_C = index;
      // form表单回显数据
      this.form_C = this.color[this.map_C.get(index)];
      this.dialogVisible_C = true;
    },
    submit_C() {
      // 打印被修改过的数据
      console.log(this.form_C);
      this.dialogVisible_C = false;
    },
    cancal_C() {
      // 对象是引用数据类型，赋值使用的是同一个地址值，点击取消使用表格中的数据变回未修改之前的
      this.color[this.map_C.get(this.index_C)] = this.oldform_C
      this.dialogVisible_C = false;
    },
  },
};
</script>