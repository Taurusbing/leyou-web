<template>
  <div>
    <div>
      <v-layout align-center>
        <v-btn color="primary">新增</v-btn>
        <v-spacer></v-spacer>
        <v-flex xs12 sm6 md3>
          <v-text-field label="搜索" append-icon="search" hide-details v-model="search"></v-text-field>
        </v-flex>
      </v-layout>
      <v-data-table
        :headers="headers"
        :items="branks"
        :options.sync="options"
        :server-items-length="totalDesserts"
        :loading="loading"
        :pagination="pagination"
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
            pagination:{},
            headers: [
              { text: '品牌Id',align: 'center',sortable: true,value: 'id'},
              { text: '品牌名',align: 'center',sortable: false,value: 'name'},
              { text: 'LOGO',align: 'center',sortable: false,value: 'image'},
              { text: '首字母',align: 'center',sortable: true,value: 'letter'},
              { text: '操作',align: 'center',sortable: false,value: 'id'},
            ]
          }
        },
      mounted(){//渲染后执行
        // this.getdata();
      },
      //钩子函数，页面一加载就创建
      created(){
        //   this.branks = [
        //   {id:"1234",name:"小米",image:"//",letter:"X"},
        //   {id:"1235",name:"华为",image:"//",letter:"H"},
        //   {id:"1134",name:"三星",image:"//",letter:"S"},
        //   {id:"1034",name:"苹果",image:"//",letter:"P"}
        // ];
        //   this.totalDesserts = 15
        //vue的ajax框架axios，then是成功的回调，catch是失败的回调
/*        axios.get("/item/queryBrank")
          .then(function (response) {
            this.branks = response;
        }).catch(function (error) {

        })*/

          this.$http.get("item/brand/queryAll")
            .then(resp =>{
              this.branks = resp.data;
          })
              // this.$http.get("item/brand/queryAll")
              //   .then(function (response) {
              //       this.branks = response.data;
              //   }).catch(function (error) {
              //
              // })

        }
      // methods:{
      //     getdata(){
      //       this.$http.get("item/brand/queryAll")
      //         .then(function (response) {
      //           console.log(response.data),
      //             this.branks = response.data
      //         }).catch(function (error) {
      //
      //       })
      //     }
      // }
      }
</script>

<style scoped>

</style>
