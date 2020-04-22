<template>
  <div class="SZZT">
    <div class="btop">
      <mark>|</mark>
      {{title}}
    </div>
    <div style="display:flex">
      <div class="SL" style="padding: 10px 30px 10px 50px;">
        <div id="PMChart" :style="{width: '146px', height: '146px'}">
          <el-progress type="circle" :percentage="70" width="146"></el-progress>
          <div class="JDTNR">
            <div class="NR">
              <span class="fontSizeTiele">可用载水量</span>
              <span class="bigFontSize">5000KG</span>
              <span class="fontSize">2000KG</span>
            </div>
          </div>
        </div>
        <div class="xx">
          <span class="fontSizeTiele">
            消防泵实施压力：
            <br />
            <span class="fontSize">0.8mpa</span>
          </span>
          <span class="fontSizeTiele">
            消防泵实施压力：
            <br />
            <span class="fontSize">0.8mpa</span>
          </span>
          <span class="fontSizeTiele">
            消防泵实施压力：
            <br />
            <span class="fontSize">0.8mpa</span>
          </span>
        </div>
      </div>
      <div class="SL" style="padding: 10px 50px 10px 30px;">
        <div id="PMChart" :style="{width: '146px', height: '146px'}">
          <el-progress type="circle" :percentage="70" width="146"></el-progress>
          <div class="JDTNR">
            <div class="NR">
              <span class="fontSizeTiele">可用载水量</span>
              <span class="bigFontSize">5000KG</span>
              <span class="fontSize">2000KG</span>
            </div>
          </div>
        </div>
        <div class="xx">
          <span class="fontSizeTiele">
            消防泵实施压力：
            <br />
            <span class="fontSize">0.8mpa</span>
          </span>
          <span class="fontSizeTiele">
            消防泵实施压力：
            <br />
            <span class="fontSize">0.8mpa</span>
          </span>
          <span class="fontSizeTiele">
            消防泵实施压力：
            <br />
            <span class="fontSize">0.8mpa</span>
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
/**
 * 今日警情-派遣力量-上装状态
 *          ----张磊 2020.04.16
 */
export default {
  name: "SZZT",
  props: {
    title: String,
    list: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      form: {},
      option: {}
    };
  },
  created() {},
  mounted() {
    this.$nextTick(() => {
      // this.drawLine("SLChart");
      // this.drawLine("PMChart");
    });
  },
  methods: {
    drawLine(id) {
      let SLChart = this.$echarts.init(document.getElementById(id));
      let option = {
        backgroundColor: "#03141c",
        title: {
          text: "可用载水量\n",
          subtext: "2000KG\n5000KG",
          x: "center",
          y: "center",
          textStyle: {
            color: "#fff",
            fontSize: 20,
            fontWeight: "normal"
          },
          subtextStyle: {
            color: "rgba(255,255,255,.45)",
            fontSize: 24,
            fontWeight: "normal"
          }
        },
        legend: {
          x: "center",
          y: "bottom",
          data: ["rose3", "rose5", "rose6", "rose7", "rose8"]
        },
        calculable: true,
        series: [
          {
            name: "面积模式",
            type: "pie",
            radius: [100, 130],
            center: ["50%", "50%"],
            hoverAnimation: false,
            avoidLabelOverlap: false,
            label: {
              normal: {
                show: false
              },
              emphasis: {
                show: true
              }
            },
            lableLine: {
              normal: {
                show: false
              },
              emphasis: {
                show: true
              }
            },
            data: [
              {
                value: 300,
                itemStyle: {
                  color: new this.$echarts.graphic.LinearGradient(0, 1, 0, 0, [
                    {
                      offset: 0,
                      color: "#f6e3a1"
                    },
                    {
                      offset: 1,
                      color: "#ff4236"
                    }
                  ])
                }
              },
              {
                value: 52,
                name: "rose2",
                itemStyle: {
                  color: "transparent"
                }
              }
            ]
          },
          {
            name: "面积模式",
            type: "pie",
            radius: [110, 120],
            center: ["50%", "50%"],
            label: {
              normal: {
                show: false
              },
              emphasis: {
                show: true
              }
            },
            lableLine: {
              normal: {
                show: false
              },
              emphasis: {
                show: true
              }
            },
            data: [
              {
                value: 300,
                itemStyle: {
                  color: "transparent"
                }
              },
              {
                value: 52,
                name: "rose2",
                itemStyle: {
                  color: new this.$echarts.graphic.LinearGradient(0, 1, 0, 0, [
                    {
                      offset: 0,
                      color: "#348fe6"
                    },
                    {
                      offset: 1,
                      color: "#625bef"
                    }
                  ])
                }
              }
            ]
          }
        ]
      };
      SLChart.setOption(option);
    }
  }
};
</script>

<style lang="scss">
.SZZT {
  width: 100%;
  .JDTNR {
    width: 100%;
    height: 100%;
    position: relative;
    top: -151px;
    display: flex;
    // flex-wrap: wrap;
    align-items: center;
    span {
      display: inline-block;
      width: 100%;
      text-align: center;
    }
  }
  .fontSizeTiele {
    font-size: 13px;
  }
  .fontSize {
    font-size: 15px;
    font-weight: 700;
  }
  .bigFontSize {
    font-size: 19px;
    font-weight: 700;
    padding: 8px 0 1px 0;
  }
  .SL {
    display: flex;
    // justify-content: space-between;
    flex: 1;
    align-items: center;
    justify-content: center;
    .el-progress__text {
      color: transparent;
    }
    .xx {
      // display: flex;
      // justify-content: space-between;
      flex-wrap: wrap;
      padding: 0 15px;
      text-align: center;
      span {
        width: 100%;
        display: block;
        padding-bottom: 10px;
        line-height: 24px;
      }
    }
  }
}
</style>
