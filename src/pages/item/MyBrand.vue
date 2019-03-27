<template>
  <div>
    <div>
      <v-layout align-center>
        <v-btn color="primary">新增</v-btn>
        <v-spacer></v-spacer>
        <v-flex xs12 sm6 md3>
          <!--搜索按钮，绑定参数-->
          <v-text-field label="搜索" append-icon="search" hide-details v-model="search"></v-text-field>
        </v-flex>
      </v-layout>
      <v-data-table
        :headers="headers"
        :items="branks"
        :options.sync="options"
        :server-items-length="totalDesserts"
        :loading="loading"
        :pagination.sync="pagination"
      >
        <!--class="elevation-1"    样式-->
        <!-- 数据渲染 -->
        <template slot="items" slot-scope="props">
          <td class="text-xs-center">{{ props.item.id }}</td>
          <td class="text-xs-center">{{ props.item.name }}</td>
          <td class="text-xs-center"><img :src="props.item.name"/></td>
          <td class="text-xs-center">{{ props.item.letter }}</td>
          <td class="text-xs-center">
            <v-icon small class="mr-2" @click="editItem(props.item)" >edit</v-icon>
            <v-icon small @click="deleteItem(props.item)">delete</v-icon>
          </td>
         </template>
      </v-data-table>
    </div>
  </div>
</template>

<script>
    export default {
        name: "MyBrand",
        data () {
          return {
            //定义上面用:的变量
            totalDesserts: 0,
            branks: [],
            loading: false,
            options: {},
            pagination:{},//分页对象
            search:"",
            headers: [
              { text: '品牌Id',align: 'center',sortable: true,value: 'id'},
              { text: '品牌名',align: 'center',sortable: false,value: 'name'},
              { text: 'LOGO',align: 'center',sortable: false,value: 'image'},
              { text: '首字母',align: 'center',sortable: true,value: 'letter'},
              { text: '操作',align: 'center',sortable: false,value: 'id'},
            ]
          }
        },
      //监听
      watch:{
        //监听只要搜索框修改就调用函数
        search(){
          this.loadData()
        },
        pagination:{
          //复杂参数，深度监听
          deep:true,
          handler(){
            this.loadData();
          }
        }
        // search:{ 另一种写法
        //   handler(){
        //     this.loadData()
        //   }
        // }
      },

      //钩子函数，页面一加载就创建
      created(){
          this.loadData()
        },
      methods:{
          //定义函数
          loadData(){
              this.$http.get("item/brand/queryAll",{
                params:{
                  search:this.search,
                  descending:this.pagination.descending,//排序方式，false是asc升序,true是desc降序
                  page:this.pagination.page,//当前页码
                  rows:this.pagination.rowsPerPage,//每页多少行
                  sortBy:this.pagination.sortBy,//排序字段
                  totalItems:this.pagination.totalItems//数据总数
                }
              }).then(resp =>{
                  this.branks = resp.data
              })
          }
      }
      }
</script>

<style scoped>

</style>

//搜索条件查询
  //绑定事件，定义变量
  //请求
  //监听
//分页查询
  //对象操作
  //请求参数
  //监听
