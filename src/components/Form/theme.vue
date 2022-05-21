<template>
  <div>
    <table>
      <thead>
        <tr>
          <th>名称</th>
          <th>类型</th>
          <th>图片</th>
          <th>宽度</th>
          <th>高度</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item, index) of Object.entries(theme)" :key="item[0]">
          <td>{{ item[1].text }}</td>
          <td>{{ item[1].type }}</td>
          <td>
            <img
              :src="item[1].value.src"
              :width="item[1].value.width"
              :height="item[1].value.height"
            />
          </td>
          <td>{{ item[1].value.width }}</td>
          <td>{{ item[1].value.height }}</td>
          <el-button type="success" @click="editBtn_T(index)">修改</el-button>
        </tr>
      </tbody>
    </table>
    <el-dialog title="修改信息" :visible.sync="dialogVisible_T" width="30%">
      <el-form ref="form" :model="form_T" label-width="80px">
        <el-form-item label="名称">
          <el-input v-model="form_T.text"></el-input>
        </el-form-item>
        <el-form-item label="类型">
          <el-select
            v-model="form_T.type"
            placeholder="请选择活动区域"
            disabled
          >
            <el-option label="color" value="color"></el-option>
            <el-option label="image" value="image"></el-option>
          </el-select>
        </el-form-item>
        <el-form-item label="图片">
          <img
            :src="form_T.value.src"
            :width="form_T.value.width"
            :height="form_T.value.height"
          />
        </el-form-item>
        <el-form-item label="宽度">
          <el-input
            v-model="form_T.value.width"
            @blur="change(form_T.value.width)"
          ></el-input>
        </el-form-item>
        <el-form-item label="高度">
          <el-input
            v-model="form_T.value.height"
            @blur="change(form_T.value.height)"
          ></el-input>
        </el-form-item>
      </el-form>
      <span slot="footer" class="dialog-footer">
        <el-button @click="cancal_T()">取 消</el-button>
        <el-button type="primary" @click="submit_T()">确 定</el-button>
      </span>
    </el-dialog>
  </div>
</template>
<script>
export default {
  data() {
    return {
      theme: {
        bg_a_top: {
          type: "image",
          text: "通⽤背景a-顶部图⽚",
          value: {
            src: "https://lofter.lf127.net/1650274089811/bg_a_top.png",
            width: "100%",
            height: "12px",
          },
        },
        bg_a_mid: {
          type: "image",
          text: "通⽤背景a-中部图⽚",
          value: {
            src: "https://lofter.lf127.net/1650274113058/bg_a_mid.png",
            width: "100%",
            height: "100%",
          },
        },
        bg_a_bottom: {
          type: "image",
          text: "通⽤背景a-底部图⽚",
          value: {
            src: "https://lofter.lf127.net/1650274128356/bg_a_bottom.png",
            width: "100%",
            height: "51px",
          },
        },
      },
      dialogVisible_T: false,
      form_T: {
        text: "",
        type: "",
        value: {
          src: "",
          width: "",
          height: "",
        },
        oldform_T: null,
        index_T: null,
        map_T: null,
      },
      dialogVisible: false,
    };
  },
  mounted() {
    this.map_T = new Map();
    this.map_T.set(0, "bg_a_top");
    this.map_T.set(1, "bg_a_mid");
    this.map_T.set(2, "bg_a_bottom");
  },
  methods: {
    editBtn_T(index) {
      this.oldform_T = JSON.parse(
        JSON.stringify(this.theme[this.map_T.get(index)])
      );
      console.log(this.oldform_T);
      this.form_T = this.theme[this.map_T.get(index)];
      this.index_T = index;
      this.dialogVisible_T = true;
    },
    submit_T() {
      console.log(this.form_T);
      this.dialogVisible_T = false;
    },
    cancal_T() {
      console.log(this.oldform_T);
      this.theme[this.map_T.get(this.index_T)] = this.oldform_T;
      this.dialogVisible_T = false;
    },
    change(value) {
      var str = new RegExp("^(\\d|[1-9]\\d|100)%$");
      var str_s = new RegExp("^(?!00)(?:[0-9]{1,3}|1000)px$");
      if (!str.test(value) && !str_s.test(value)) {
        alert("请输入1%-100%或者1px-1000px");
      }
    },
  },
};
</script>