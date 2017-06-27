<template>
    <div class="table">
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-menu"></i> 管理员管理</el-breadcrumb-item>
                <!-- <el-breadcrumb-item>基础表格</el-breadcrumb-item> -->
            </el-breadcrumb>
        </div>
       
        <el-row class='handle-box'>
        <el-col :span="20"> 
            <el-button @click="dialogTableVisible = true">添加管理员</el-button>
            <el-button>修改管理员</el-button>
            <el-button>重置管理员密码</el-button>
            <el-button>删除管理员</el-button>
        </el-col>
      
           
        </el-row>
        <el-table :data="tableData" border style="width: 100%" ref="multipleTable" @selection-change="handleSelectionChange">
            <el-table-column type="selection" width="55"></el-table-column>
            <el-table-column prop="id" label="序号"  width="80">
            </el-table-column>
            <el-table-column prop="name" label="管理员名称" width="120" >
            </el-table-column>
            <el-table-column prop="kjh" label="管理员类型" width="150" >
            </el-table-column>
            <el-table-column prop="sex" label="创建时间" width="120">
            </el-table-column>
            <el-table-column prop="phone" label="备注" width="230">
            </el-table-column>
           

        </el-table>
        <div class="pagination">
            <el-pagination
                    @current-change ="handleCurrentChange"
                    layout="prev, pager, next"
                    :total="1000">
            </el-pagination>
        </div>
    
<el-dialog title="" size="tiny"  :visible.sync="dialogTableVisible">
<el-row class="mr10">
    <el-col :span="6" :offset="4">管理员名称</el-col>
    <el-col :span="10"><el-input v-model="select_word" placeholder="筛选关键词" ></el-input></el-col>
</el-row>
<el-row class="mr10">
    <el-col :span="6" :offset="4">初始密码</el-col>
    <el-col :span="10"><el-input v-model="select_word" placeholder="筛选关键词" ></el-input></el-col>
</el-row>
<el-row class="mr10">
    <el-col :span="6" :offset="4">确认密码</el-col>
    <el-col :span="10"><el-input v-model="select_word" placeholder="筛选关键词" ></el-input></el-col>
</el-row>
<el-row class="mr10">
    <el-col :span="6" :offset="4">管理员类型</el-col>
    <el-col :span="10"><el-input v-model="select_word" placeholder="筛选关键词" ></el-input></el-col>
</el-row>

  <div slot="footer" class="dialog-footer" style="display: flex;justify-content: space-around;">
    <el-button @click="dialogTableVisible = false">提交</el-button>
    <el-button @click="dialogTableVisible = false">取消</el-button>
  </div>
</el-dialog>


<el-dialog title="林丽的个人信息"  :visible.sync="dialogContentVisible">
<el-row class="mr10">
  <el-col :span="12">昵称：林立</el-col>
  <el-col :span="12">手机号：15090909090</el-col>
</el-row>
<el-row class="mr10">
  <el-col :span="12">空间号：21313121211</el-col>
  <el-col :span="12">钱包余额：100元</el-col>
</el-row>
<el-row class="mr10">
 性别：男
</el-row>
<el-row class="mr10">
  地区：中国北京市
</el-row>
<el-row class="mr10">
  个性签名：我就是我，颜色不一样验货
</el-row>

<el-row class="mr10">
  <el-col :span="4">头像：</el-col><el-col :span="6"><img src="../../../static/img/img.jpg" style="width: 100%"/></el-col>
  <el-col :span="4">朋友圈背景图</el-col><el-col :span="6"><img src="../../../static/img/img.jpg" style="width: 100%"/></el-col>
</el-row>

</el-dialog>



<el-dialog title="如何才能学会快乐的思维方式？"  :visible.sync="dialogTableContentVisible">
<el-row class="mr10">
 设定金额：9.9元
</el-row>
<el-row class="mr10">
 就是不告诉你
</el-row>
<el-row class="mr10">
 语音
</el-row>
<el-row class="mr10">
<el-col :span="6"><img src="../../../static/img/img.jpg" style="width: 100%"/></el-col>
 <el-col :span="6"><img src="../../../static/img/img.jpg" style="width: 100%"/></el-col>
</el-row>

  <div slot="footer" class="dialog-footer">
    <el-button @click="dialogTableContentVisible = false">关闭</el-button>
    
  </div>

</el-dialog>


    </div>



</template>

<script>
    export default {
        data() {
            return {
                url: '../../../static/vuetable.json',
                tableData: [],
                cur_page: 1,
                multipleSelection: [],
                select_cate: '',
                select_word: '',


                num:12,
                gridData: [{
          id: '1',
          question: '这是一个问题',
          num: '99',
          setMoney: '999.00'
         
        }, {
           id: '2',
          question: '这是一个问题',
          num: '99',
          setMoney: '999.00'
        }, {
           id: '3',
          question: '这是一个问题',
          num: '99',
          setMoney: '999.00'
        }, {
           id: '4',
          question: '这是一个问题',
          num: '99',
          setMoney: '999.00'
        }],
        dialogTableVisible: false,
        dialogContentVisible: false,
        dialogTableContentVisible:false,
       
            }
        },
        created(){
            this.getData();
        },
        methods: {
            handleCurrentChange(val){
                this.cur_page = val;
                this.getData();
            },
            getData(){
                let self = this;
                // if(process.env.NODE_ENV === 'development'){
                //     self.url = '/ms/table/list';

                // };
                // console.log(self.url)
                // self.url='../../../static/vuetable.json'
                // self.$axios.get(self.url, {page:self.cur_page}).then((res) => {
                //     console.log(res.list)
                //     self.tableData = res.data.list;
                //     console.log(self.tableData)
                // })
                self.url='../../../static/vuetable.json'
                self.$axios.get(self.url).then((res) => {
                    console.log(res.data.list)
                    self.tableData = res.data.list;
                    console.log(self.tableData)
                })
            },
            formatter(row, column) {
                return row.address;
            },
            filterTag(value, row) {
                return row.tag === value;
            },
            handleEdit(index, row) {
                this.$message('编辑第'+(index+1)+'行');
            },
            handleDelete(index, row) {
                this.$message.error('删除第'+(index+1)+'行');
            },
            handleSelectionChange: function(val) {
                this.multipleSelection = val;
            }
        }
    }
</script>

<style scoped>
.handle-box{
    margin-bottom: 20px;
}
.text-center{text-align: center;}
.lineHeight{height: 36px;line-height: 36px;}
/*.handle-del{
    border-color: #bfcbd9;
    color: #999;
}
.handle-select{
    width: 120px;
}*/
/*.handle-input{
    width: 300px;
    display: inline-block;
}*/
.el-dialog{width:60%!important;}
.mr10{margin-bottom: 20px}
</style>