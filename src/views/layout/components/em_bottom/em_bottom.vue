<template>
  <div class="bottom">
    <win :id="win.id" :data="win">
      <div style="width: 100%;" class="em-bottom-container">
        <el-dialog title="密码修改" :visible.sync="dialogFormVisible" :append-to-body="true" v-dialogDrag="true">
          <el-form :model="form">
            <el-form-item label="旧密码" :label-width="formLabelWidth">
              <el-input v-model="form.oldPassword" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="新密码" :label-width="formLabelWidth">
              <el-input v-model="form.newPassword" autocomplete="off"></el-input>
            </el-form-item>
          </el-form>
          <div slot="footer" class="dialog-footer">
            <el-button @click="cancel" class="em-btn-shadow">取 消</el-button>
            <el-button type="primary" @click="confirm" class="em-btn-shadow">确 定</el-button>
          </div>
        </el-dialog>
        <el-input v-model="input" placeholder="请输入内容" style="width: 150px"></el-input>
        <el-button class="data_button em-btn-border-animation  svg-style" @click="dialogFormVisible = true"><svg>
          <rect x="0" y="0" fill="none" width="100%" height="100%"></rect>
        </svg>密码修改</el-button>
        <el-button class="data_button em-btn-border-animation  svg-style" @click="loginOut"><svg>
          <rect x="0" y="0" fill="none" width="100%" height="100%" ></rect>
        </svg>退&emsp;&emsp;出</el-button>
      </div>
    </win>
  </div>
</template>

<script>
  import win from "@/components/win/win"
  import {modify} from "@/api/table_operate"
    export default {
        name: "em_bottom",
        components: {
          win
        },
      data(){
           return {
             win: {
               id: "bottom",
               title: "",
               top: "94%",
               left: 20,
               show: true,
               resizable:false,
               width:"98%",
               class:"em-bottom-window"
             },
             input:'',
             dialogFormVisible: false,
             form: {
               oldPassword: '',
               newPassword:''
             },
             formLabelWidth: '60px'
           }
      },
      created() {
          var bodyheight=Number(document.body.clientHeight);
          var bodywidth=Number(document.body.clientWidth);
          console.log(bodyheight);
         /* this.win.top=bodyheight-53;*/

      },
      methods:{
           confirm(){
             this.dialogFormVisible = false;
             modify({
                url:"/user/userext/updatePwd",
                params:this.form
             }).then(res=>{
                 console.log(res)
             })
           },
           cancel(){
             this.dialogFormVisible = false
           },
          loginOut(){
               this.$router.push("/login");
          }
      }
    }
</script>

<style lang="scss" scoped>
  @import "_em_bottom.scss";
</style>

