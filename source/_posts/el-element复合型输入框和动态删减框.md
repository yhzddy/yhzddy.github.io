---
title: el-element复合型输入框和动态删减框
date: 2019-09-22 14:33:23
tags: el-element，控件
categories: 前端
thumbnail: /assets/dd.jpg
---
这里我碰到的一个需求是添加多个电话,所以我猜想用到了push数组，刚好el-element里面有用到动态增减表单项的组件
查看源码，添加则是push一个空数组
<!-- more -->
    data() {
      return {
        dynamicValidateForm: {
          domains: [{
            value: ''
          }],
          email: ''
        }
      };

    addDomain() {
        this.dynamicValidateForm.domains.push({
          value: '',
          key: Date.now()
        });
删除则splice(index, 1)并返回一个删除后的数组

     removeDomain(item) {
        var index = this.dynamicValidateForm.domains.indexOf(item)
        if (index !== -1) {
          this.dynamicValidateForm.domains.splice(index, 1)
        }
      },

      关于数组的方法push和splice使用差不多，
      push() 方法可向数组的末尾添加一个或多个元素，并返回新的数组。
      arr.push(newelement1,newelement2,....,newelementX)

      splice不仅可以删除，还可以进行添加，返回新的数组
      splice 是数组的一个方法，使用这个方法会改变原来的数组结构，
      arr.splice（index ，howmany ， itemX）；


复合型输入框的使用

        <div style="margin-top: 15px;">
           <el-input placeholder="请输入内容" v-model="input3" class="input-with-select">
             <el-select v-model="select" slot="prepend" placeholder="请选择">
                <el-option label="餐厅名" value="1"></el-option>
                <el-option label="订单号" value="2"></el-option>
                <el-option label="用户电话" value="3"></el-option>
             </el-select>
                 <el-button slot="append" icon="el-icon-search"></el-button>
          </el-input>
       </div>