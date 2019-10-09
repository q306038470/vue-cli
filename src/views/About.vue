<template>
  <el-tabs v-model="activeName" @tab-click="handleClick">
    <el-tab-pane label="理科" name="first">
      <div>
        <div>
          <el-radio v-model="radio" label="1">优班</el-radio>
          <el-radio v-model="radio" label="2">普班</el-radio>
        </div>
        <div style="margin-top:20px">
          输入班级个数:
          <el-input-number style="margin-left:20px;margin-right:20px;" v-model="num1" @change="handleChange" :min="1" :max="10" label="输入班级个数"></el-input-number>
        </div>

        <div style="margin-top:20px">
          <el-input style="margin-bottom:20px;" v-for="(item, index) in arr1" v-model="pradeObj['input' + index]" placeholder="请输入内容" :key="index" small></el-input>
        </div>
        <el-button  type="primary" @click="getPrade">提交</el-button>
        <div>平均成绩为：{{avg1}}</div>
        <div v-if="numArr1.length >= 1">
          <p>成绩排名：</p>
          <p v-for="(item,index) in numArr1" :key="index">{{index+1}}: {{item}}</p>
        </div>
      </div>
    </el-tab-pane>
    <el-tab-pane label="文科" name="second">文科</el-tab-pane>
  </el-tabs>
</template>

<script>
export default {
  data() {
    return  {
      activeName: 'first',
      radio: '1',
      num1: 1,
      // arr1: new Array(this.num1),
      pradeObj: {
        input1: '',
        input2: '',
        input3: '',
        input4: '',
        input5: '',
        input6: '',
        input7: '',
        input8: '',
        input9: '',
        input10: ''
      },
      avg1:'',
      numArr1: [],
    }
  },
  methods: {
    handleClick(tab, event) {
      console.log(tab, event);
    },
    handleChange(value) {
      console.log(value);
      this.num1 = value;
    },
    getPrade() {
      console.log("pradeObj:", this.pradeObj);
      let obj = this.pradeObj;
      let sum = 0;
      let count = 0;
      let arr = [];
      for (var prop in obj) {
        if (obj[prop] > 0) {
          count++;
          sum += Number(obj[prop]);
          arr.push(obj[prop])
        }
      }
      this.avg1 = sum / count;
      this.numArr1 = arr.sort(function (a,b) {
        return b - a
      });
    }
  },
  computed: {
    arr1: function () {
      let arr = [];
      for (let i = 0; i < this.num1; i++) {
        arr.push({})
      }
      return arr;
    }
  }
}
</script>

<style lang="css">

</style>