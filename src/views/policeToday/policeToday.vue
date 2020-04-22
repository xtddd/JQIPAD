<template>
  <div class="page policeToday">
    <h2 class="header">今日警情</h2>
    <div class="main">
      <div class="right flex" :style="rightBGC">
        <div class="SJZ">
          <ZHLB></ZHLB>
          <SJC></SJC>
        </div>
        <div class="nb">
          <div class="nav">
            <template v-for="(item,index) in keyList">
              <div
                class="item"
                :class="[item]"
                :style="flag === index ? activeBgc : bgc"
                :key="item+index"
                @click="SelectionItem(item,index)"
              >
                <span>{{item}}</span>
              </div>
            </template>
          </div>
          <div class="contents">
            <dispatch-power v-if="item === '力量派遣'" :list="PX"></dispatch-power>
            <police-details v-if="item === '详情总览'"></police-details>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
/**
 * 今日警情
 *        ----张磊 2020.04.14
 */
import dispatchPower from "./componts/dispatchPower";
import policeDetails from "./componts/policeDetails";
import SJC from "./componts/SJC";
import ZHLB from "./componts/ZHLB";
import "../../scss/iconfont";
import * as api from "../../api/api";
export default {
  name: "policeToday",
  components: {
    dispatchPower,
    SJC,
    policeDetails,
    ZHLB
  },
  data() {
    return {
      list: [],
      form: {},
      xqList: [], //辖区的数据
      keyList: [
        "详情总览",
        "力量派遣",
        "处置措施",
        "组织指挥",
        "联战联勤",
        "信息报送"
      ],
      flag: 1,
      active: 1,
      item: "力量派遣",
      activeBgc: {
        background: "url(" + require("../../assets/纵线tab选中背景.png") + ")"
      },
      leftBGC: {
        background: "url(" + require("../../assets/左框.png") + ")",
        backgroundSize: "100% 100%"
      },
      rightBGC: {
        background: "url(" + require("../../assets/右框.png") + ")",
        backgroundSize: "100% 100%"
      },
      bgc: {},
      PX: null //派遣力量
    };
  },
  computed: {},
  created() {
    this.init();
  },
  mounted() {
    window.handlerDouble = this.handlerDouble;
  },
  methods: {
    //初始化
    init() {
      // this.getList();
      console.log("policeToday.init...");
    },
    //获取列表数据
    getList() {
      return api
        .InitAlarmService({
          jgid: "10033a1bbb6045adb72f256d63b294b3",
          type: 1
        })
        .then(res => {
          this.list = res.data.data;
          console.log(this.list);
        });
    },
    SelectionItem(item, index) {
      this.flag = index;
      this.item = item;
    },
    //双击事件
    handlerDouble() {
      // alert(data);
      //派遣力量
      // this.PX = data.dispatchDataList;
      let form = {
        to: "map",
        data: {
          x: 118.797499,
          y: 32.087104
        }
      };
      window.bound.SendToC(JSON.stringify(form));
      console.log(this.PX, "10101");
    }
  }
};
</script>

<style lang="scss">
.policeToday {
  color: #ffffff;
  .icons {
    width: 52px;
    height: 52px;
    vertical-align: -0.15em;
    fill: currentColor;
    overflow: hidden;
  }
  .header {
    height: 54px;
    line-height: 54px;
    color: #6cb1ff;
    text-align: left;
    font-size: 20px;
    margin: 0;
    // padding: 28px 0 30px;
    border-bottom: 1px #4cbaff solid;
    box-sizing: border-box;
    padding-left: 10px;
  }
  .main {
    width: 100%;
    height: calc(100% - 54px);
    display: flex;
    text-align: left;
    padding-top: 10px;
    box-sizing: border-box;
    .btop {
      // width: 100%;
      height: 30px;
      line-height: 30px;
      font-size: 16px;
      padding: 0 0 0 10px;
      padding: 6px 20px;
      border-bottom: 1px #2b8fff solid;
      mark {
        background-color: #00ffff;
        color: #00ffff;
        border-radius: 3px;
      }
    }
    .flex {
      display: flex;
      flex-flow: column nowrap;
    }
    .left {
      width: 470px;
      margin-right: 10px;
      padding: 5px;
      border: 1px #072e4b solid;
      box-sizing: border-box;
      ::-webkit-scrollbar {
        width: 10px;
        background-color: #2c6dcf;
      }
      ::-webkit-scrollbar-thumb {
        border-radius: 10px;
        background-color: #2575ec;
      }
      ::-webkit-scrollbar-track {
        box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.3);
        background-color: #2c6dcf;
        border-radius: 10px;
      }
      .top {
        font-size: 25px;
        height: 50px;
        line-height: 50px;
        border-bottom: 2px #69dce0 solid;
        box-sizing: border-box;
      }
      mark {
        background-color: #00ffff;
        color: #00ffff;
        border-radius: 3px;
      }
      .el-form {
        margin-top: 10px;
        .el-form-item__label {
          font-size: 20px;
          color: #ffffff;
        }
        &:first-child .el-form-item__label {
          letter-spacing: 2px;
        }
        .line {
          text-align: center;
        }
      }
      .btop {
        height: 30px;
        line-height: 30px;
        border-bottom: 1px #2b8fff solid;
        padding: 0 0 0 10px;
      }
      .bottom {
        overflow: auto;
        border: 2px #2b8fff solid;
        flex-grow: 1;
        box-sizing: border-box;
        .jqlb {
          display: flex;
          .topIcon {
            margin-right: 10px;
          }
          .bh {
            border-bottom: 2px #69dce0 solid;
          }
        }
      }
      .el-button {
        background-color: #133a89;
        color: #ffffff;
      }
      .el-input {
        input {
          // border-color: #2b8fff;
          background-color: #072c52;
        }
        // input:focus {
        //   outline: none;
        //   border: 1px solid #58b195;
        // }
      }
    }
    .right {
      display: flex;
      flex: 1;
      // border: 2px #072e4b solid;
      padding: 5px;
      margin: 0 10px;
      box-sizing: border-box;
      flex-wrap: wrap;
      ::-webkit-scrollbar {
        width: 10px;
        background-color: #0a3455;
      }
      ::-webkit-scrollbar-thumb {
        border-radius: 10px;
        background-color: #2575ec;
      }
      ::-webkit-scrollbar-track {
        box-shadow: inset 0 0 6px rgba(0, 0, 0, 0.3);
        background-color: #0a3455;
        border-radius: 10px;
      }
      .SJZ {
        width: 100%;
        height: 60px;
        background-color: #072e4b;
        padding-right: 50px;
        box-sizing: border-box;
        display: flex;
      }
      .nb {
        display: flex;
        flex: 1;
        // flex-flow: column;
        overflow: hidden;
      }
      .nav {
        width: 40px;
        // padding-bottom: 50px;
        height: 100%;
        // background-color: #ccc;
        box-sizing: border-box;
        display: flex;
        flex-wrap: wrap;
        justify-content: space-between;
        cursor: pointer;
        .item {
          width: 100%;
          background: #1e83e1;
          display: flex;
          justify-content: center;
          align-items: center;
          text-align: center;
          counter-reset: #ffffff;
          font-size: 16px;
          padding: 2px 0;
          border-bottom: 1px #ffffff solid;
          line-height: 1.3;
          span {
            display: inline-block;
            width: 24px;
          }
        }
        :nth-last-child(1) {
          border: none;
        }
        // .active {
        //   background-color: #41a7eb;
        // }
      }
      .contents {
        flex: 1;
        padding: 0 10px 10px;
      }
    }
  }
}
</style>
