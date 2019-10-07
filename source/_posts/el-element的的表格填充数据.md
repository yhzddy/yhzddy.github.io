---
title: el-element的的表格填充数据
date: 2019-09-22 14:04:59
tags: el-element，json，vue，solt
categories: 前端
thumbnail: /assets/ff.jpg
---


在我从后台拿到一个这样的数据
        
        data = {
                PersonInfo：{
                    id_card：
                }，
                Phone:[
                         {
                             personDataId:
                             phone_number:
                         },
                         {}
                      ],
                psAddress:[
                         {},
                         {}
                      ]
                }
<!-- more -->

由于el-table :data="tableData"中的：data需要的数据类型是数组
       
       这里我我将返回的数据push进tableData数组
        data(){
            return{
                 tableData: []
            }
        }

        methods:{
            this.tableData.push(res.data)
       }

       这样就是tableData[{
           [
               {},
               {}
           ],
           [
               {},
               {}
           ]
       }]
       
但是考虑里里面数据的复杂性，不能像之前直接使用，在el-table-column中用prop属性来对应对象中的键名即可填入数据。

     官方文档的数据形式
     tableData: [{
            date: '2016-05-02',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1518 弄'
          }, {
            date: '2016-05-04',
            name: '王小虎',
            address: '上海市普陀区金沙江路 1517 弄'
          }

    <el-table-column
        prop="date"
        label="日期"
        width="180">
    </el-table-column>

所以我们这里要用到solt插件和v-for循环

      <el-table-column label="ID号码">
        <template slot-scope="scope">
          <div>{{scope.row.PersonInfo.id_card}}</div>
        </template>
      </el-table-column>
      <el-table-column label="联系电话">
        <template slot-scope="scope">
          <div v-for=" (item,personDataId) in scope.row.Phone" :key="personDataId">
            <span>{{item.phone_number}}</span>
          </div>
        </template>
      </el-table-column>
