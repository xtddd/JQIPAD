<template>
  <div class="ZHLB">
    <div
      style="display:flex;height:60px;padding:0 23px;backgroundColor:#2C6DCF"
    >
      <div style="padding:5px 23px 15px 0">
        <svg class="icons" aria-hidden="true">
          <use xlink:href="#icon-Group32Copy2" />
        </svg>
      </div>
      <div style="flex:1">
        <div class="nr">
          <span>灾害对象名称</span>
          <i class="assIcon iconfont icon-location"></i>
        </div>
        <div class="ass">{{dataObj.afdz}}</div>
        <div class="nr">
          <div style="fontSize:12px">
            <span style="paddingRight:10px">高层建筑火灾</span>
            <span>{{dataObj.bjsj}}</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
/**
 * 今日警情-派遣力量-灾害列表
 *          ----张磊 2020.04.15
 */
export default {
  name: "ZHLB",
  props: {
    title: String,
    data: {
      type: Object,
      default: () => {
        return {
          afdz: "鼓楼区北京西路119号",
          bjsj: "14:32:32"
        };
      }
    },
    //双击事件
    func: Function
  },
  data() {
    return {
      form: {},
      dataObj: this.data
    };
  },
  created() {},
  methods: {
    //控制显示于隐藏
    handlerC() {
      this.flag = !this.flag;
    },
    ss() {
      console.log(this.func);
      // this.func();
    },
    //1-5的选中效果
    active(key) {
      let boo = this[key];
      this.one = false;
      this.two = false;
      this.three = false;
      this.four = false;
      this.five = false;
      this[key] = !boo;
    },
    //灾害类型
    ZHFChange(val) {
      console.log(val);
      let arr = [];
      if (val === "火灾") {
        arr = [
          "高层建筑",
          "砖木结构建筑",
          "地下建筑火灾",
          "石油化工火灾",
          "人员密集场所火灾",
          "交通工具火灾",
          "仓库火灾",
          "工厂火灾",
          "特殊情况下火灾",
          "其他火灾"
        ];
      }
      this.ZHDChange = arr;
    },
    ZHDChange(val) {
      console.log(val);
      let arr = [];
      if (val === "高层建筑") {
        arr = [
          "高层建筑",
          "砖木结构建筑",
          "地下建筑火灾",
          "石油化工火灾",
          "人员密集场所火灾",
          "交通工具火灾",
          "仓库火灾",
          "工厂火灾",
          "特殊情况下火灾",
          "其他火灾"
        ];
      }
      this.ZHTChange = arr;
    },
    //灾情特征
    checkedBox(item, index) {
      if (this.arr.includes(index)) {
        //includes()方法判断是否包含某一元素,返回true或false表示是否包含元素，对NaN一样有效
        //filter()方法用于把Array的某些元素过滤掉，filter()把传入的函数依次作用于每个元素，然后根据返回值是true还是false决定保留还是丢弃该元素：生成新的数组
        this.arr = this.arr.filter(function(ele) {
          return ele != index;
        });
        this.checkList = this.checkList.filter(function(ele) {
          return ele != item;
        });
      } else {
        this.arr.push(index);
        this.checkList.push(item);
      }
    }
  }
};
</script>

<style lang="scss" scope>
.ZHLB {
  width: 500px;
  color: #ffffff;
  // padding: 0 23px;
  // display: flex;
  .topIcon {
    margin-right: 10px;
  }
  .bh {
    border-bottom: 2px #69dce0 solid;
  }
  .nr {
    display: flex;
    font-size: 16px;
    justify-content: space-between;
    .assIcon {
      font-size: 16px;
      line-height: 24px
      // color: #ffffff;
    }
    .showIcon {
      font-size: 18px;
      // color: #ffffff;
    }
  }
  .ass {
    font-size: 12px;
  }
  .btn {
    height: 46px;
    display: flex;
    text-align: center;
    background-color: #0350d0;
    padding: 0 23px;
    .btnItem {
      flex: 1;
    }
    .btnIcon {
      font-size: 24px;
    }
  }
  .PZX {
    background-color: #2c6dcf;
    border-top: 1px #1a4e91 solid;
  }
  .duo {
    display: flex;
  }
  .Singular {
    display: flex;
    font-size: 16px;
    margin-top: 8px;
    line-height: 30px;
    // height: 30px;
    flex: 1;
    color: #ffffff;
    padding-right: 5px;
    .el-input__inner {
      height: 30px;
      line-height: 30px;
      border: 2px #a6d0ff solid;
      box-shadow: #0066ff 0px 0px 8px 0px inset;
    }
    .el-input__icon {
      line-height: 30px;
    }
    .title {
      text-align: center;
      width: 80px;
    }
    .value {
      display: flex;
      flex: 1;
      // .el-checkbox-button {
      //   // background-color: #2c6dcf;
      //   // border: 2px #a6d0ff solid;
      //   // color: #ffffff;
      //   margin-right: 10px;
      //   .el-checkbox-button__inner {
      //     background-color: #2c6dcf;
      //     color: #ffffff;
      //   }
      // }
      .el-textarea {
        .el-textarea__inner {
          // border-color: #2b8fff;
          background-color: #2c6dcf;
          border: 2px #a6d0ff solid;
          box-shadow: #0066ff 0px 0px 8px 0px inset;
        }
      }
      .el-select {
        flex: 1;
        select {
          background-color: #2c6dcf;
        }
      }
      .el-input {
        .el-input__inner {
          background-color: #2c6dcf;
          color: #fff;
        }
      }
      .el-button {
        flex: 1;
        margin-left: 5px;
      }
      .HX {
        text-align: center;
        display: inline-block;
        width: 15px;
      }
    }
    .DJ {
      width: 30px;
      height: 26px;
      line-height: 26px;
      text-align: center;
      position: relative;
      top: 8px;
      margin-left: 2px;
      border: 2px #a6d0ff solid;
      box-sizing: border-box;
      cursor: pointer;
    }
    .ZH {
      flex: 1;
    }
    .ZHActive {
      background-color: #a6d0ff;
    }
    .one {
      background-color: #2edb43;
      box-shadow: 0px 0px 10px #a6d0ff inset;
    }
    .two {
      background-color: #5eb1ff;
      box-shadow: 0px 0px 10px #a6d0ff inset;
    }
    .three {
      background-color: #ffe42e;
      box-shadow: 0px 0px 10px #a6d0ff inset;
    }
    .four {
      background-color: #ff8518;
      box-shadow: 0px 0px 10px #a6d0ff inset;
    }
    .five {
      background-color: #ff1818;
      box-shadow: 0px 0px 10px #a6d0ff inset;
    }
  }
}
.el-select-dropdown .el-scrollbar,
.el-select-dropdown__item {
  color: #ffffff;
  background-color: #2c6dcf;
}
.el-select-dropdown {
  color: #ffffff;
  background-color: #2c6dcf;
}
.el-select-dropdown__list,
.el-select-dropdown__empty {
  color: #ffffff;
  border: 1px #4cbaff solid;
}
.el-select-dropdown__item:hover {
  // color: #409eff;
  font-weight: 700;
}
.el-select-dropdown__item.hover,
.el-select-dropdown__item:hover {
  background-color: #6ca7ff;
}
</style>
