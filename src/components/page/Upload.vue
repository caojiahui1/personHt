<template>
    <div class="table">
        <div class="crumbs">
            <el-breadcrumb separator="/">
                <el-breadcrumb-item><i class="el-icon-menu"></i> 交易中心</el-breadcrumb-item>
                <!-- <el-breadcrumb-item>基础表格</el-breadcrumb-item> -->
            </el-breadcrumb>
        </div>
        <div class="handle-box">
           
            <el-row :gutter="10">
             <el-col class="text-center lineHeight" :span="2">交易类型</el-col>
             <el-col :span="2">
<template>
  <el-select v-model="value" placeholder="请选择">
    <el-option
      v-for="item in options"
      :key="item.value"
      :label="item.label"
      :value="item.value">
    </el-option>
  </el-select>
</template>
</el-col>

             <el-col class="text-center lineHeight" :span="2">交易状态</el-col>
             <el-col :span="2">
<template>
  <el-select v-model="value" placeholder="请选择">
    <el-option
      v-for="item in options"
      :key="item.value"
      :label="item.label"
      :value="item.value">
    </el-option>
  </el-select>
</template>
</el-col>


             <el-col class="text-center lineHeight" :span="2">昵称</el-col>
             <el-col :span="3"><el-input v-model="select_word" placeholder="筛选关键词" ></el-input></el-col>
             <el-col class="text-center lineHeight" :span="2">空间号</el-col>
             <el-col :span="3"><el-input v-model="select_word" placeholder="筛选关键词" ></el-input></el-col>
             <el-col class="text-center lineHeight" :span="2">日期</el-col>
             <el-col :span="3"><el-input v-model="select_word" placeholder="筛选关键词" ></el-input></el-col>
            </el-row>
            
         <!--    <el-input v-model="select_word" placeholder="筛选关键词" class="handle-input mr10"></el-input>
            <el-input v-model="select_word" placeholder="筛选关键词" class="handle-input mr10"></el-input>
            <el-button type="primary" icon="search">搜索</el-button> -->
        </div>
        <el-row class='handle-box'>
        
        <el-col :span="6" :offset="18">
            <el-button>删除</el-button>
            <el-button>筛选</el-button>
            <el-button>导出</el-button>
        </el-col>
           
        </el-row>
       <el-table :data="tableData" border style="width: 100%" ref="multipleTable" @selection-change="handleSelectionChange">
            <el-table-column type="selection" width="55"></el-table-column>
            <el-table-column prop="id" label="序号"  width="80">
            </el-table-column>
            <el-table-column prop="name" label="昵称" width="120" >
            </el-table-column>
            <el-table-column prop="kjh" label="空间号" width="150" >
            </el-table-column>
            <el-table-column prop="sex" label="性别" width="120">
            </el-table-column>
            <el-table-column prop="phone" label="手机号" width="150">
            </el-table-column>
            <el-table-column prop="moneyPage" label="我的钱包" width="120">
            </el-table-column>
            <el-table-column prop="zt" label="账号状态" width="120">
            </el-table-column>
            <el-table-column prop="registerTime" label="注册时间" width="180">
            </el-table-column>
            <el-table-column label="操作" width="200" fixed="right">
               <!--  <template scope="scope">
                    <el-button size="small"
                            @click="handleEdit(scope.$index, scope.row)">替身机器人管理</el-button>
                    <el-button size="small" 
                           @click="handleDelete(scope.$index, scope.row)"   @click="dialogTableVisible = true">详情</el-button>
                </template> -->
                 <template scope="scope">
                    <el-button size="small"  @click="dialogTableVisible = true">修改交易状态</el-button>
                    <el-button size="small"  @click="dialogContentVisible = true">详情</el-button>
                </template>
            </el-table-column>

        </el-table>
        <div class="pagination">
            <el-pagination
                    @current-change ="handleCurrentChange"
                    layout="prev, pager, next"
                    :total="1000">
            </el-pagination>
        </div>
    


<el-dialog title="修改交易状态" size="tiny" :visible.sync="dialogTableVisible">
<el-row class="mr10">
 <el-col class="text-center lineHeight" :span="6">交易状态</el-col>
  <el-col :span="14">
<template>
  <el-select v-model="value" placeholder="请选择">
    <el-option
      v-for="item in options"
      :key="item.value"
      :label="item.label"
      :value="item.value">
    </el-option>
  </el-select>
</template>
</el-col>
</el-row>




  <div slot="footer" class="dialog-footer" style="display: flex;justify-content: space-around;">
    <el-button @click="dialogTableVisible = false">确定</el-button>
    <el-button @click="dialogTableVisible = false">取消</el-button>
  </div>

</el-dialog>



<el-dialog title="修改交易状态"  :visible.sync="dialogContentVisible">
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



                 options: [{
          value: '选项1',
          label: '已付款'
        }, {
          value: '选项2',
          label: '未付款'
        }],
        value:'',

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