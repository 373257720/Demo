<template>
  <div class="top"></div>

  <main>
    <div
      class="activity"
      :class="{
        'sidebar-close': !sidebarSwitch,
        'sidebar-open': sidebarSwitch,
      }"
    >
      <div class="toolbar">
        <div :class="{ isactive: obj[0].isactive }" @click="toolbarFun(0)">
          Call
        </div>
        <div :class="{ isactive: obj[1].isactive }" @click="toolbarFun(1)">
          Activity
        </div>
        <div :class="{ isactive: obj[2].isactive }" @click="toolbarFun(2)">
          SMS
        </div>
        <div :class="{ isactive: obj[3].isactive }" @click="toolbarFun(3)">
          Update
        </div>
      </div>
      <el-table :data="tableData" border style="width: 100%">
        <el-table-column prop="name" label="操作">
          <template #default="scope">
            <el-button
              @click="
                () => {
                  scope.row.edit = true;
                }
              "
              >编辑</el-button
            >
            <el-button
              type="danger"
              @click="handleDelete(scope.$index, scope.row)"
              >删除</el-button
            >
          </template>
        </el-table-column>
        <el-table-column prop="date" label="Content">
          <template #default="scope">
            <el-popover effect="light" trigger="hover" placement="top">
              <template #default>
                <p>
                  <s>姓名: {{ scope.row.name }}</s>
                  <span>姓名: {{ scope.row.name }}</span>
                </p>
                <p>
                  <s>住址: {{ scope.row.address }}</s>
                  <span>住址: {{ scope.row.address }}</span>
                </p>
              </template>
              <template #reference>
                <div class="name-wrapper">
                  <span size="medium" v-if="!scope.row.edit">{{
                    scope.row.name
                  }}</span>
                  <el-input
                    v-else-if="scope.row.edit"
                    @blur="
                      () => {
                        scope.row.edit = false;
                      }
                    "
                    v-model="scope.row.name"
                  ></el-input>
                </div>
              </template>
            </el-popover>
          </template>
        </el-table-column>
        <el-table-column prop="date" label="姓名"> </el-table-column>
        <el-table-column prop="address" label="地址"> </el-table-column>
      </el-table>
    </div>
    <div
      class="mid-component"
      :class="{
        'sidebar-close': !sidebarSwitch,
        'sidebar-open': sidebarSwitch,
      }"
    >
      <div
        class="Formdata"
        :class="{
          'sidebar-close': !sidebarSwitch,
          'sidebar-open': sidebarSwitch,
        }"
      >
        <header>
          <div @click="sidebarOpen">CaLL</div>
          <div>SMS</div>
          <div>Email</div>
          <div @click="submitForm('ruleForm')">Save</div>
          <div>Task</div>
        </header>
        <div class="box">
          <el-form
            :model="ruleForm"
            :rules="rules"
            label-position="left"
            label-width="100px"
            ref="ruleForm"
            class="demo-ruleForm"
          >
            <el-form-item label="First name" prop="name">
              <el-input v-model="ruleForm.FirstName"></el-input>
            </el-form-item>
            <el-form-item label="Last name" prop="name">
              <el-input v-model="ruleForm.LastName"></el-input>
            </el-form-item>
            <el-form-item  prop="region">
              <!-- <el-form-item label="DOB" prop="region">
                <el-date-picker
                  type="date"
                  placeholder="选择日期"
                  v-model="ruleForm.date1"
                ></el-date-picker>
              </el-form-item>
              <el-form-item label="Title" prop="region">
                <el-select
                  v-model="ruleForm.region"
                  placeholder="请选择活动区域"
                >
                  <el-option label="区域一" value="shanghai"></el-option>
                  <el-option label="区域二" value="beijing"></el-option>
                </el-select>
              </el-form-item> -->
            </el-form-item>
            <el-form-item class="Email" label="Email">
              <el-form-item prop="Email">
                <el-input v-model="ruleForm.name"></el-input>
              </el-form-item>
              <el-form-item prop="Email">
                <el-input v-model="ruleForm.name"></el-input>
              </el-form-item>
            </el-form-item>
            <el-form-item class="Mobile" label="Mobile">
              <el-form-item prop="type">
                <el-input v-model="ruleForm.name"></el-input>
              </el-form-item>
              <el-form-item prop="type">
                <el-input v-model="ruleForm.name"></el-input>
              </el-form-item>
            </el-form-item>

            <el-form-item label="languange" prop="region">
              <!-- <slot name="label"><span></span></slot> -->
              <el-select
                v-model="ruleForm.languange"
                placeholder="请选择活动区域"
              >
                <el-option label="区域一" value="shanghai"></el-option>
                <el-option label="区域二" value="beijing"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item label="Country" prop="region">
              <!-- <slot name="label"><span>Country</span></slot> -->
              <el-select
                v-model="ruleForm.Country"
                placeholder="请选择活动区域"
              >
                <el-option label="区域一" value="shanghai"></el-option>
                <el-option label="区域二" value="beijing"></el-option>
              </el-select>
            </el-form-item>

            <el-form-item label="Address" prop="type">
              <el-input v-model="ruleForm.name"></el-input>
            </el-form-item>
            <el-form-item label="Local time" prop="type">
              <el-input v-model="ruleForm.name"></el-input>
            </el-form-item>

            <el-form-item label="Lead owner" prop="name">
              <el-select v-model="ruleForm.region" placeholder="请选择活动区域">
                <el-option label="区域一" value="shanghai"></el-option>
                <el-option label="区域二" value="beijing"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item label="Sale team" prop="region">
              <el-select v-model="ruleForm.region" placeholder="请选择活动区域">
                <el-option label="区域一" value="shanghai"></el-option>
                <el-option label="区域二" value="beijing"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item label="Regulation" prop="delivery">
              <el-input v-model="ruleForm.name"></el-input>
            </el-form-item>
            <el-form-item label="LeadSource" prop="resource">
              <el-select v-model="ruleForm.region" placeholder="请选择活动区域">
                <el-option label="区域一" value="shanghai"></el-option>
                <el-option label="区域二" value="beijing"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item label="Lead status" prop="type">
              <el-select v-model="ruleForm.region" placeholder="请选择活动区域">
                <el-option label="区域一" value="shanghai"></el-option>
                <el-option label="区域二" value="beijing"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item label="Timeassigned" prop="type">
              <div style="width: 200px">{{ ruleForm.name }}</div>
            </el-form-item>
            <el-form-item label="Timer" prop="type">
              <div style="width: 200px">sdfdsf</div>
              <!-- <el-input v-model="ruleForm.name"></el-input> -->
            </el-form-item>
            <el-form-item label="Inquiry" prop="type">
              <el-input v-model="ruleForm.name"></el-input>
            </el-form-item>
            <el-form-item label="Attachment" prop="type">
              <el-upload
                class="upload-demo"
                action="https://jsonplaceholder.typicode.com/posts/"
                :on-preview="handlePreview"
                :on-remove="handleRemove"
                :before-remove="beforeRemove"
                multiple
                :limit="3"
                :on-exceed="handleExceed"
                :file-list="fileList"
              >
                <el-button size="small" type="primary">点击上传</el-button>
                <template #tip>
                  <div class="el-upload__tip">
                    只能上传 jpg/png 文件，且不超过 500kb
                  </div>
                </template>
              </el-upload>
            </el-form-item>
          </el-form>
        </div>
      </div>
      <div class="saleNote">
        <header>Sale note</header>
        <div class="box">
          <el-form
            :model="ruleForm"
            :rules="rules"
            label-position="left"
            :inline="true"
            ref="ruleForm"
            label-width="100px"
            class="demo-ruleForm"
          >
            <el-form-item label="Interest" prop="name">
              <el-input v-model="ruleForm.FirstName"></el-input>
            </el-form-item>
            <el-form-item label="Call back" prop="name">
              <el-input v-model="ruleForm.LastName"></el-input>
            </el-form-item>
            <el-form-item label="Status" prop="Email">
              <el-input v-model="ruleForm.name"></el-input>
            </el-form-item>
            <el-form-item label="Note" prop="Email">
              <el-input v-model="ruleForm.name"></el-input>
            </el-form-item>
            <el-form-item label="Trading Level" prop="name">
              <el-select v-model="ruleForm.region" placeholder="请选择活动区域">
                <el-option label="区域一" value="shanghai"></el-option>
                <el-option label="区域二" value="beijing"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item label="Favo" prop="region">
              <el-select v-model="ruleForm.region" placeholder="请选择活动区域">
                <el-option label="区域一" value="shanghai"></el-option>
                <el-option label="区域二" value="beijing"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item label="Regulation" prop="delivery">
              <el-input v-model="ruleForm.name"></el-input>
            </el-form-item>
            <el-form-item label="LeadSource" prop="resource">
              <el-select v-model="ruleForm.region" placeholder="请选择活动区域">
                <el-option label="区域一" value="shanghai"></el-option>
                <el-option label="区域二" value="beijing"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item label="Lead status" prop="type">
              <el-select v-model="ruleForm.region" placeholder="请选择活动区域">
                <el-option label="区域一" value="shanghai"></el-option>
                <el-option label="区域二" value="beijing"></el-option>
              </el-select>
            </el-form-item>
            <el-form-item label="Timeassigned" prop="type">
              <div style="width: 200px">{{ ruleForm.name }}</div>
            </el-form-item>
            <el-form-item label="Timer" prop="type">
              <div style="width: 200px">sdfdsf</div>
            </el-form-item>
            <el-form-item label="Inquiry" prop="type">
              <el-input v-model="ruleForm.name"></el-input>
            </el-form-item>
          </el-form>
        </div>
      </div>
      <div class="demoAccount"></div>
    </div>
  </main>

  <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
  <!-- <GZinput></GZinput> -->
</template>
<script>
// import GZinput from '../sass-submodules/components/Form/input'
export default {
  name: "App",
  data() {
    return {
      sidebarSwitch: true,
      obj: [
        { isactive: false },
        { isactive: false },
        { isactive: false },
        { isactive: false },
      ],
      // obj: {
      //   call: { isactive: false },
      //   activity: { isactive: false },
      //   sms: { isactive: false },
      //   Update: { isactive: false },
      // },
      modify: false,
      tableData: [
        {
          date: "2016-05-03",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
          edit: false,
        },
        {
          date: "2016-05-02",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
          edit: false,
        },
        {
          date: "2016-05-04",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
          edit: false,
        },
        {
          date: "2016-05-01",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄",
          edit: false,
        },
      ],
      ruleForm: {
        FirstName: "",
        region: "",
        date1: "",
        date2: "",
        delivery: false,
        type: [],
        resource: "",
        desc: "",
      },
      fileList: [
        {
          name: "food.jpeg",
          url:
            "https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100",
        },
        {
          name: "food2.jpeg",
          url:
            "https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100",
        },
      ],
      rules: {
        Email: [
          {
            type: "email",
            message: "请输入正确的邮箱地址",
            trigger: ["blur", "change"],
          },
        ],
        name: [
          { required: true, message: "请输入活动名称", trigger: "blur" },
          { min: 3, max: 5, message: "长度在 3 到 5 个字符", trigger: "blur" },
        ],
        region: [
          { required: true, message: "请选择活动区域", trigger: "change" },
        ],
        date1: [
          {
            type: "date",
            required: true,
            message: "请选择日期",
            trigger: "change",
          },
        ],
        date2: [
          {
            type: "date",
            required: true,
            message: "请选择时间",
            trigger: "change",
          },
        ],
        type: [
          {
            type: "array",
            // required: true,
            message: "请至少选择一个活动性质",
            trigger: "change",
          },
        ],
        resource: [
          { required: true, message: "请选择活动资源", trigger: "change" },
        ],
        desc: [{ required: true, message: "请填写活动形式", trigger: "blur" }],
      },
    };
  },
  methods: {
    sidebarOpen() {
      this.sidebarSwitch = !this.sidebarSwitch;
    },
    toolbarFun(num) {
      this.obj.forEach((item) => {
        item.isactive = false;
      });
      this.obj[num].isactive = !this.obj[num].isactive;
    },
    handleRemove(file, fileList) {
      console.log(file, fileList);
    },
    handlePreview(file) {
      console.log(file);
      window.open(file.url);
    },
    handleExceed(files, fileList) {
      this.$message.warning(
        `当前限制选择 3 个文件，本次选择了 ${files.length} 个文件，共选择了 ${
          files.length + fileList.length
        } 个文件`
      );
    },
    beforeRemove(file, fileList) {
      console.log(fileList);
      return this.$confirm(`确定移除 ${file.name}？`);
    },
    submitForm(formName) {
      this.$refs[formName].validate((valid) => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },
  },
  components: {
    // GZinput
    // HelloWorld
  },
};
</script>

<style lang='scss'>
*,
*::before,
*::after {
  box-sizing: border-box;
}
body,
div,
ul,
ol,
dl,
dt,
dd,
li,
dl,
h1,
h2,
h3,
h4 {
  margin: 0;
  padding: 0;
  font-style: normal;
  // font: 12px/22px "\5B8B\4F53", Arial, Helvetica, sans-serif;
}
ol,
ul,
li {
  list-style: none;
}
img {
  border: 0;
  vertical-align: middle;
}
body {
  height: 100vh;
  width: 100vw;
  color: #000000;
  background: #fff;
  // text-align: center;
}
.clear {
  clear: both;
  height: 1px;
  width: 100%;
  overflow: hidden;
  margin-top: -1px;
}
a {
  color: #000000;
  text-decoration: none;
}
a:hover {
  color: #ba2636;
  text-decoration: underline;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  position: relative;
  $height: 100px;
  height: 100%;
  $Topheight: 90px;
  $Sidebar-width: 450px;
  $main-width: 1000px;
  .top {
    width: 100%;
    height: $Topheight;
    background: $BackgroundColor;
  }
  main {
    position: relative;
    padding-top: 12px;
    width: 100%;
    height: calc(100% - #{$Topheight});
    overflow-y: auto;
    .activity {
      -webkit-transition: -webkit-transform 0.5s;
      transition: 0.5s;
      box-sizing: border-box;
      position: absolute;
      top: 12px;
      left: 20px;
      font-size: 12px;
      margin-bottom: 10px;
      width: $Sidebar-width;
      height: 850px;
      border: 1px solid #2c3e50;
      padding: 20px;
      .toolbar {
        display: flex;
        flex-wrap: wrap;
        margin-bottom: 10px;
        > div {
          padding: 5px;
          cursor: pointer;
          margin-right: 20px;
          @include border(
            $px: 1px,
            $color: #dcdfe6,
            $shape: solid,
            $radius: 5px
          );
        }
      }
      .isactive {
        background: #666;
      }
    }
    .activity.sidebar-close {
      left: -$Sidebar-width;
    }
    .activity.sidebar-open {
      left: 20px;
    }
    .mid-component {
      -webkit-transition: -webkit-transform 0.5s;
      transition: 0.5s;
      position: absolute;
      $default-top: 12px;
      $default-left: 500px;

      .Formdata {
        height: 300px;
        top: 12px;
        margin-bottom: 10px;
        left: $default-left;
        // width: $main-width;
        border: 1px solid #2c3e50;
        .el-form {
          // display: flex;
          // flex-wrap: wrap;
          justify-items: center;
          display: grid;
          grid-template-columns: repeat(2, auto);
          // grid-template-rows: repeat(3, 33.33%);
        }
        .left,
        .right {
          width: 50%;
        }
        header {
          display: flex;
          height: 40px;
          width: 100%;
          justify-content: flex-end;
          border-bottom: 1px solid #000000;
          > div {
            padding: 5px;
            cursor: pointer;
            margin-right: 20px;
            @include border(
              $px: 1px,
              $color: #dcdfe6,
              $shape: solid,
              $radius: 5px
            );
          }
        }
        .box {
          padding: 10px;
          height: 258px;
          overflow-y: auto;
          overflow-x: hidden;
        }
      }
      .Formdata.sidebar-close .el-form {
        grid-template-columns: repeat(3, auto);
      }
      .Formdata.sidebar-open .el-form {
        grid-template-columns: repeat(2, auto);
      }
      .saleNote {
        margin-bottom: 10px;
        height: 300px;
        left: 30%;
        border: 1px solid #2c3e50;
        header {
          border-bottom: 1px solid #000000;
          @include boxModel(
            $width: 100%,
            $height: 40px,
            $background-color: #fff,
            $padding: 0,
            $margin: 0,
            $box-sizing: "border-box"
          );
        }
        .box {
          padding: 10px;
          height: 258px;
          overflow-y: auto;
        }
      }
      .demoAccount {
        height: 230px;
        left: 30%;
        background: $BackgroundColor;
      }
    }
    .mid-component.sidebar-open {
      width: $main-width;
      left: 500px;
    }
    .mid-component.sidebar-close {
      width: $main-width + 500px - 20px;
      left: 20px;
    }
  }
  .el-button {
    padding: 0;
    font-size: 12px;
  }
  .el-form-item__error {
    width: 200px;
    padding-top: 0;
    position: relative;
  }
  .el-form-item__label {
    line-height: 30px;
    font-size: 12px;
  }
  .combine {
    .el-form-item {
      // flex:1
      // display: inline;
    }
  }
  .el-form-item__content {
    // margin-bottom: 5px;
    width: 250px;
    line-height: 30px;
    font-size: 12px;
  }
  .el-date-editor.el-input,
  .el-date-editor.el-input__inner {
    width: 250px;
  }
  .el-input__inner {
    width: 250px;
    height: 30px;
    line-height: 30px;
  }
  .el-input {
    height: 30px;
    font-size: 12px;
    line-height: 30px;
  }
  .el-form-item {
    margin-bottom: 5px;
  }
  .el-form-item.Email,
  .el-form-item.Mobile {
    margin-bottom: 0;
  }
  // .el-form-item.Email,
  // .el-form-item.mobile {
  //   .el-form-item{
  //     margin-bottom: 0;
  //   }
  // }
  .el-input__icon {
    line-height: 30px;
  }
}
</style>
