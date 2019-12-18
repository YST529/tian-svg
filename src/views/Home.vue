<template>
  <div class="home">
    <el-row>
      <el-col :span="24">
        <div id="svg">
          <svg xmlns="http://www.w3.org/2000/svg" version="1.1" width="240px" height="420px">
            <path v-for="(item, i) in pathList" :key="i" :d="item.d" style="fill:lime;stroke:purple;stroke-width:2" />
          </svg>
        </div>
      </el-col>
    </el-row>
    <el-form :inline="true" :model="formInline" class="demo-form-inline">
      <el-form-item label="绘画方式">
        <el-select v-model="formInline.region" placeholder="请选择" :style="{width:'100px'}">
          <el-option label="M" value="M"></el-option>
          <el-option label="m" value="m"></el-option>
          <el-option label="L" value="L"></el-option>
          <el-option label="l" value="l"></el-option>
          <el-option label="A" value="A"></el-option>
          <el-option label="a" value="a"></el-option>
        </el-select>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="addItem">添加</el-button>
      </el-form-item>
    </el-form>
    <el-form :inline="true" class="demo-form-inline" v-for="( data, i ) in svgData" :key="i">
      <el-form-item :label="data.region+':'" v-if="data.region == 'm' || data.region == 'M' ">
        <el-form-item>
          <el-input v-model="data.x" :style="inputWidth"></el-input>
        </el-form-item>
        <el-form-item>
          <el-input v-model="data.y" :style="inputWidth"></el-input>
        </el-form-item>
        <!-- <el-form-item label="style:">
          <el-form-item>
            <el-input v-model="data.fill" :style="inputWidth"></el-input>
          </el-form-item>
          <el-form-item>
            <el-input v-model="data.stroke" :style="inputWidth"></el-input>
          </el-form-item>
          <el-form-item>
            <el-input v-model="data[stroke-width]" :style="inputWidth"></el-input>
          </el-form-item>
        </el-form-item> -->
      </el-form-item>
      <el-form-item :label="data.region+':'" v-if="data.region == 'l' || data.region == 'L' ">
        <el-form-item>
          <el-input v-model="data.x" :style="inputWidth"></el-input>
        </el-form-item>
        <el-form-item>
          <el-input v-model="data.y" :style="inputWidth"></el-input>
        </el-form-item>
        <!-- <el-form-item label="style:">
          <el-form-item>
            <el-input v-model="data.fill" :style="inputWidth"></el-input>
          </el-form-item>
          <el-form-item>
            <el-input v-model="data.stroke" :style="inputWidth"></el-input>
          </el-form-item>
          <el-form-item>
            <el-input v-model="data[stroke-width]" :style="inputWidth"></el-input>
          </el-form-item>
        </el-form-item> -->
      </el-form-item>
      <el-form-item :label="data.region+':'" v-if="data.region == 'a' || data.region == 'A' ">
        <el-form-item>
          <el-input v-model="data.rx" :style="inputWidth"></el-input>
        </el-form-item>
        <el-form-item>
          <el-input v-model="data.ry" :style="inputWidth"></el-input>
        </el-form-item>
        <el-form-item>
          <el-input v-model="data.xar" :style="inputWidth"></el-input>
        </el-form-item>
        <el-form-item>
          <el-input v-model="data.laf" :style="inputWidth"></el-input>
        </el-form-item>
        <el-form-item>
          <el-input v-model="data.wf" :style="inputWidth"></el-input>
        </el-form-item>
        <el-form-item>
          <el-input v-model="data.x" :style="inputWidth"></el-input>
        </el-form-item>
        <el-form-item>
          <el-input v-model="data.y" :style="inputWidth"></el-input>
        </el-form-item>
        <!-- <el-form-item label="style:">
          <el-form-item>
            <el-input v-model="data.fill" :style="inputWidth"></el-input>
          </el-form-item>
          <el-form-item>
            <el-input v-model="data.stroke" :style="inputWidth"></el-input>
          </el-form-item>
          <el-form-item>
            <el-input v-model="data[stroke-width]" :style="inputWidth"></el-input>
          </el-form-item>
        </el-form-item> -->
      </el-form-item>
    </el-form>
    <el-button type="primary" @click="drawSvg">绘制</el-button>
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "home",
  data() {
    return {
      pathList: [],
      index: "",
      formInline: {
        region: ""
      },
      svgData: [],
      inputWidth: { width: "60px" }
    };
  },
  methods: {
    addItem() {
      let obj = { region: "", fill: "", stroke: "", 'stroke-width':"" };
      obj.region = this.formInline.region;
      if (obj.region != "") {
        this.svgData.push(obj);
      }
    },
    drawSvg() {
      let data = this.svgData;
      let newData = { d: "", style: "" };
      for (let obj of data) {
        // debugger
        let d = newData.d, style= newData.style;
        if (obj.region == "a" || obj.region == "A") {
          d +=
            obj.region + " " +
            obj.rx + " " +
            obj.ry + " " +
            obj.xar + " " +
            obj.laf + " " +
            obj.wf + " " +
            obj.x + " " +
            obj.y;
        } else {
          d +=
            obj.region + " " +
            obj.x + " " +
            obj.y;
        }
        style = "fill:"+ obj.fill + ";stroke:" + obj.stroke + ";stroke-width:" + obj['stroke-width']
        newData.d = d
        newData.style = style
      }
        this.pathList.push( newData )
        console.log( this.pathList, 'pathList' )
    }
  }
};
</script>
