<template>
  <div id="add_report">
    <el-container class="detail">
      <header class="header">
        <el-form :inline="true" :model="addReport" class="demo-form-inline">
          <el-form-item label="姓名">
            <el-input v-model="addReport.name" placeholder="请输入"></el-input>
          </el-form-item>
          <el-form-item label="就诊科室">
            <el-input v-model="addReport.room" placeholder="请输入"></el-input>
          </el-form-item>
          <el-form-item label="检查时间">
            <el-input v-model="addReport.time" placeholder="请输入"></el-input>
          </el-form-item>
          <el-form-item label="预约状态">
            <el-select v-model="addReport.stat" placeholder="请选择">
              <el-option label="已预约" value="已预约"></el-option>
              <el-option label="未预约" value="未预约"></el-option>
            </el-select>
          </el-form-item>
        </el-form>
      </header>
      <el-main class="main">
        <div>
          <span> 诊断结果：</span>
          <el-input
            type="textarea"
            :rows="3"
            placeholder="请输入内容"
            v-model="addReport.result"
            class="revise_con"
            resize="none"
          >
          </el-input>
        </div>
        <div>
          <span> 详情：</span>
          <el-input
            type="textarea"
            :rows="15"
            placeholder="请输入内容"
            v-model="addReport.details"
            class="revise_con"
            resize="none"
          >
          </el-input>
        </div>
        <!-- <div>
          <span> 上传附件：</span>
          <p>最多上传三个附件，每个大小不超过2m</p>
        </div>
        <div class="dis">
          <span> 文件描述：</span>
          <el-input placeholder=""></el-input>
          <el-button size="mini">浏览</el-button>
          <el-button size="mini" type="primary">上传</el-button>
        </div> -->
      </el-main>
      <el-footer class="footer">
        <el-button type="primary" @click="clickSave" >保存</el-button>
        <el-button type="warning" @click="clickCancel">取消</el-button>
      </el-footer>
    </el-container>
  </div>
</template>
<script>
export default {
  data() {
    return {
      addReport : {
        name : '',
        time : '',
        room : '',
        result : '',
        details : '',
        stat : null,
      }
    };
  },

  methods: {
    clear_reload(){
      this.addReport.name=''
      this.addReport.time=''
      this.addReport.details=''
      this.addReport.room=''
      this.addReport.result=''
      this.addReport.stat=null
      this.$router.push('/person/report/add')
    },
    clickSave(){
      console.log("save!")
      var status
      this.$axios.post('/do/report/addreport', this.addReport)
      .then((response) => {
        // console.log(response)
        status=response.status;
        // console.log(status)
        if(response.status === 200) {
          console.log('success')
          this.$message({
            message: "保存成功",
            type: "success",
          })
          this.clear_reload()
        }else{
          console.log('failed')
          this.$message({
            message: "保存失败",
            type: "error",
          })
        }
      });
      
    },
    clickCancel(){
      console.log("cancel!")
      this.clear_reload()
    }
  },
};
</script>
<style lang="scss" scoped>
#add_report {
  position: relative;
  top: 20px;
  .detail {
    height: 100%;
  }
  .header {
    display: flex;
    justify-content: space-between;
    font-size: 12px;
    height: 30px;
    margin-left: 80px;
    .el-input__inner {
      height: 25px;
    }
    p {
      color: #797979;
      display: flex;
      justify-content: center;
      align-items: center;
      span {
        color: #333;
      }
    }
  }
  .main {
    color: #333;
    display: flex;
    flex-direction: column;
    > div {
      flex: 1;
      display: flex;
      margin-bottom: 13px;
      span {
        display: inline-block;
        width: 100px;
        text-align: right;
      }
      p {
        flex: 1;
      }
      .revise_con {
        flex: 1;
      }
      .bigtext {
        height: 100px;
      }
    }
  }
  .footer {
    height: 40px !important;
    display: flex;
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
#add_report {
  .el-message-box {
    width: auto !important;
  }
  //   注意 修改element-ui弹窗的样式不能在添加了scoped的style中修改，解决方法：另写一个style添加样式
  .header .el-input__inner {
    height: 30px;
  }
  .header .el-form-item__content {
    width: 105px;
  }
  .main .dis {
    height: 30px;
    .el-input {
      width: 160px;
      flex: 0 0 160px;
      margin-right: 15px;
    }
    .el-input__inner {
      height: 32px;
    }
  }
}
</style>
