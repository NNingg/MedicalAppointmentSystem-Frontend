<template>
  <div id="doctorInfo">
    <el-container>
      <el-header class="header">
        <h1>我的信息</h1>
        <!-- <p v-if="!revamp" style="color: red" @click="revamp = true">
          <i class="el-icon-edit"></i>
          修改信息
        </p> -->
      </el-header>
      <el-divider></el-divider>

      <el-main v-if="isdoctor">
        <el-row>
          <el-col :span="7">
            <el-form ref="ruleForm" label-width="100px" class="demo-ruleForm">
              <el-form-item label="姓名">
                <el-input v-model="info.name"></el-input>
              </el-form-item>
            </el-form>
            <el-form ref="ruleForm" label-width="100px" class="demo-ruleForm">
              <el-form-item label="职称">
                <el-input v-model="info.title"></el-input>
              </el-form-item>
            </el-form>
            <el-form ref="ruleForm" label-width="100px" class="demo-ruleForm">
              <el-form-item label="所属科室">
                <el-input v-model="info.department"></el-input>
              </el-form-item>
            </el-form>
            <el-form ref="ruleForm" label-width="100px" class="demo-ruleForm">
              <el-form-item label="所属单位">
                <el-input v-model="info.hospital"></el-input>
              </el-form-item>
            </el-form>
            <el-form ref="ruleForm" label-width="100px" class="demo-ruleForm">
              <el-form-item label="擅长科目">
                <el-input v-model="info.medicine"></el-input>
              </el-form-item>
            </el-form>
          </el-col>
          <el-col :span="1" class="divider">
            <el-divider direction="vertical"></el-divider>
          </el-col>
          <el-col :span="15">
            <el-form ref="ruleForm" label-width="100px" class="demo-ruleForm">
              <el-form-item label="个人简介">
                <el-input v-model="info.introduction"></el-input>
              </el-form-item>
            </el-form>
          </el-col>

          <!-- <el-col :span="7">
            <el-form
              :model="detailForm"
              ref="ruleForm"
              label-width="100px"
              class="demo-ruleForm"
            >
              <el-form-item label="就职医院" prop="name">
                <el-input v-model="detailForm.name"></el-input>
              </el-form-item>
              <el-row class="formInline">
                <el-col :span="11">
                  <el-form-item label="医院级别" prop="sex">
                    <el-select v-model="detailForm.sex" placeholder="医院级别">
                      <el-option label="三甲" value="三甲"></el-option>
                      <el-option label="二甲" value="二甲"></el-option>
                    </el-select>
                  </el-form-item>
                </el-col>
              </el-row>
              <el-form-item label="医院地址">
                <el-col :span="10">
                  <el-date-picker
                    type="year"
                    placeholder="选择年份"
                    style="width: 100%"
                  ></el-date-picker>
                </el-col>
                <el-col :span="2" style="text-align: center">省</el-col>
                <el-col :span="10">
                  <el-date-picker
                    placeholder="选择月份"
                    style="width: 100%"
                    type="month"
                  ></el-date-picker>
                </el-col>
                <el-col :span="2" style="text-align: center">市</el-col>
              </el-form-item>
              <el-form-item label="所属科室" prop="name">
                <el-input v-model="detailForm.name"></el-input>
              </el-form-item>
              <el-form-item label="医院地址" prop="name">
                <el-input v-model="detailForm.name"></el-input>
              </el-form-item>
            </el-form>
          </el-col>
          <el-col :span="1" class="divider">
            <el-divider direction="vertical"></el-divider>
          </el-col>
          <el-col :span="7">
            <el-form :model="detailForm" ref="ruleForm" class="demo-ruleForm">
              <el-form-item label="医生简介" prop="name">
                <el-input
                  v-model="detailForm.name"
                  type="textarea"
                  :rows="4"
                  resize="none"
                ></el-input>
              </el-form-item>
              <el-form-item label="工作经历" prop="name">
                <el-input
                  v-model="detailForm.name"
                  type="textarea"
                  :rows="4"
                  resize="none"
                ></el-input>
              </el-form-item>

              <el-form-item label="相关证明上传" prop="name">
                <el-input
                  v-model="detailForm.name"
                  type="textarea"
                  :rows="4"
                  resize="none"
                ></el-input>
              </el-form-item>
            </el-form>
          </el-col> -->
        </el-row>
      </el-main>

      <el-main v-if="!isdoctor">
        <el-row>
          <el-col :span="7">
            <el-form ref="ruleForm" label-width="100px" class="demo-ruleForm">
              <el-form-item label="照片" prop="graph">
                <img
                  style="width: 300px; height: 300px"
                  src="https://t12.baidu.com/it/u=433141544,21339958&fm=58"
                />
              </el-form-item>
            </el-form>
          </el-col>
          <el-col :span="1" class="divider">
            <el-divider direction="vertical"></el-divider>
          </el-col>
          <el-col :span=7>
            <el-form ref="ruleForm" label-width="100px" class="demo-ruleForm">
              <el-form-item label="姓名" prop="name">
                <el-input v-model="info.name"></el-input>
              </el-form-item>
            </el-form>
          </el-col>
        </el-row>
      </el-main>

      <!-- <div class="footer" v-if="revamp">
        <p class="bg16d" plain>保存</p>
        <p>取消</p>
      </div> -->
    </el-container>
  </div>
</template>
<script>
export default {
  data() {
    return {
      revamp: false,
      isdoctor: true,
      info: "",
    };
  },
  methods: {
    getPersonalInfo() {
      //   this.isdoctor = this.$store.state.isdoctor;
      console.log(this.isdoctor);
      if (!this.isdoctor)
        this.$axios
          // .get("/do/getinfo/usr?name=" + this.$store.state.username)
          .get("/do/getinfo/usr?name=123")
          .then((res) => {
            this.info = res[0];
            //   console.log("Current username: " + this.$store.state.username);
            console.log(this.info);
          })
          .catch(function (error) {
            console.log(error);
          });
      else {
        this.$axios
          // .get("/do/getinfo/doctor?id=" + this.$store.state.username)
          .get("/do/getinfo/doctor?id=008")
          .then((res) => {
            this.info = res[0];
            //   console.log("Current username: " + this.$store.state.username);
            console.log(this.info);
          })
          .catch(function (error) {
            console.log(error);
          });
      }
    },
  },
  created: function () {
    this.getPersonalInfo();
  },
};
</script>
<style lang="scss" scoped>
#doctorInfo {
  position: relative;
  top: 20px;
  .header {
    h1 {
      font-weight: normal;
    }
    display: flex;
    justify-content: space-between;
  }
  .el-main {
    padding-top: 0;
  }
  .el-divider--horizontal {
    margin: 0;
  }
  .el-col-8 {
    display: flex;
    flex-direction: column;
    // height: 70%;
  }
  .divider {
    height: 420px;
    padding-top: 40px;
    box-sizing: border-box;
    display: flex;
    justify-content: center;
    .el-divider {
      height: 100%;
    }
  }
  .footer {
    display: flex;
    height: 40px;
    justify-content: center;
    p {
      width: 100px;
      height: 35px;
      text-align: center;
      line-height: 35px;
      color: #fff;
    }
    p:nth-child(2) {
      background: #ccc;
      margin-left: 20px;
    }
  }
}
</style>
<style lang="scss">
#doctorInfo {
  .el-form-item__content {
    margin-left: 0px !important;
  }
  .el-form-item__label {
    width: 100% !important;
    text-align: left !important;
  }
  .el-form-item {
    margin-bottom: 10px;
  }
}
</style>
