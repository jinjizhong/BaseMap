<template>
 <div id="settings">
  <div class="setting-config config">
    <div class="config-item name">
      <img class="icon" src="./../assets/icon/3D.svg" alt="">
      <span class="baseMap">BaseMap</span>
    </div>
    <div class="config-item bg">
      <div class="bgs">
        <img class="bg-item" src="./../assets/icon/bg-gray.svg"  @click="changeBg('bg', 'gray')" alt="">
        <img class="bg-item" src="./../assets/icon/bg-grid.svg"   @click="changeBg('bg', 'grid')" alt="">
            <img class="bg-item" src="./../assets/icon/floor3.png"   @click="changeBg('bg', 'floor')" alt="">
        <input class="baseMapImgUrl" 
          id="filePicker"
          type="file" 
          placeholder="底图路径"
          @click="changeFile"
          @change="changeFile"> 
      </div>
    </div>
    <div class="config-item aligins">
        <div class="aligin">
          <div class="aligin-item">
          </div>
          <div class="aligin-item" @click="multipleActiveArr.length > 0 && setMultipleState('Isometric', 'colu')">
            <label for="">间距:</label>
            <input type="number" min="0" max="500" v-model="configs.Isometric_colu">
            <img class="img" 
              v-bind:src="img.dispersion_v" 
              @mouseenter="img.dispersion_v=img.dispersion_v_hover" 
              @mouseleave="img.dispersion_v=img.dispersion_v_def" 
              alt="垂直等距" 
              title="垂直等距">
          </div>
          <div class="aligin-item" @click="multipleActiveArr.length > 0 && setMultipleState('Isometric', 'row')">
            <label for="">间距:</label>
            <input type="number" min="0" max="500" v-model="configs.Isometric_row">
            <img class="img" 
              v-bind:src="img.dispersion_l" 
              @mouseenter="img.dispersion_l=img.dispersion_l_hover" 
              @mouseleave="img.dispersion_l=img.dispersion_l_def"
              alt="水平等距" 
              title="水平等距">
          </div>
          <div class="aligin-item" @click="multipleActiveArr.length > 0 && setMultipleState('align', 'l')">
            <img         
              v-bind:src="img.l" 
              @mouseenter="img.l=img.l_hover" 
              @mouseleave="img.l=img.l_def"  
              alt="左对齐" 
              title="左对齐"></div>
          <div class="aligin-item" @click="multipleActiveArr.length > 0 && setMultipleState('align', 't')">
            <img
              v-bind:src="img.t" 
              @mouseenter="img.t=img.t_hover" 
              @mouseleave="img.t=img.t_def"  
              alt="上对齐" title="上对齐"></div>
          <div class="aligin-item" @click="multipleActiveArr.length > 0 && setMultipleState('align', 'b')">
            <img 
              v-bind:src="img.b" 
              @mouseenter="img.b=img.b_hover" 
              @mouseleave="img.b=img.b_def"   alt="下对齐" title="下对齐"></div>
          <div class="aligin-item" @click="multipleActiveArr.length > 0 && setMultipleState('align', 'r')">
            <img
              v-bind:src="img.r" 
              @mouseenter="img.r=img.r_hover" 
              @mouseleave="img.r=img.r_def"  
              alt="右对齐" title="右对齐"></div>
        </div>
    </div>
    <div class="aligin-item contrls">
      <!-- <img  
        @click="downloadJSON()" 
        v-bind:src="img.output" 
        @mouseenter="img.output=img.output_hover" 
        @mouseleave="img.output=img.output_def" 
        alt="导出" 
        title="导出">
      <img  
        @click="saveData()" 
        v-bind:src="img.save" 
        @mouseenter="img.save=img.save_hover" 
        @mouseleave="img.save=img.save_def" 
        alt="导入" 
        title="导入"> -->
      <img  
        @click="saveData()" 
        v-bind:src="img.save" 
        @mouseenter="img.save=img.save_hover" 
        @mouseleave="img.save=img.save_def" 
        alt="保存" 
        title="保存">
      <img  
        @click="getHistory()" 
        v-bind:src="img.history" 
        @mouseenter="img.history=img.history_hover" 
        @mouseleave="img.history=img.history_def" 
        alt="历史记录" 
        title="历史记录"></div>
    <div 
      class="aligin-item screen">
      <img 
        @click="screen()"
        src="./../assets/icon/screen_full.svg" 
        alt="全屏预览" 
        title="全屏预览"></div>
      
    <!-- <div class="download">
      <span class="title" @click="download">下载</span>
    </div> -->
   
  </div>
  <div class="setting-element element" v-if="currentElement && multipleActiveArr.length === 0">
    <div class="item">
      <span class="name">{{currentElement.name}}</span>
    </div>
    <div class="item">
      <label for="" class="title">位置</label>
      <div class="subs grid grid-2">
        <div class="subs-item">
          <label for="" class="lab">上</label>
          <input type="number" class="val"  v-model="currentElement.style.top">
        </div>
         <div class="subs-item">
          <label for="" class="lab">左</label>
          <input type="number" class="val" v-model="currentElement.style.left"> 
        </div>
      </div>
      <div class="subs">
        <div class="subs-item">
          <input class="val-cb"
            type="checkbox"
            v-model="currentElement.style.isFixed"
            true-value=true
            false-value=false
          >
          <span class="val">固定</span>
        </div>
      </div>
    </div>
    <div class="item">
      <label for="" class="title">大小</label>
      <div class="subs grid grid-2">
        <div class="subs-item">
          <label class="lab" for="">长</label>
          <input 
            max="3200"
            min="0"
            class="val" type="number"  v-model="currentElement.style.width">
        </div>
         <div class="subs-item">
          <label class="lab" for="">宽</label>
          <input class="val" type="number" 
            max="1200"
            min="0"
            v-model="currentElement.style.height"> 
        </div>
      </div>
    </div>
    <div class="item"  v-if="currentElement.type === 'text'">
      <label for="" class="title">字体</label>
      <div class="subs grid grid-1">
        <div class="subs-item">
          <label class="lab" for="">大小</label>
          <input 
            max="50"
            min="12"
            class="val" type="number"  v-model="currentElement.style.fontSize">
        </div>
        <div class="subs-item full">
          <label class="lab" for="">颜色</label>
          <div class="cols">
            <span class="col-item" v-bind:class="{active: currentElement.style && currentElement.style.color === color}" v-for="(color, index) in colors" :key="index" v-bind:style="{
              background:color
            }"
            v-bind:title="color"
            @click="selColor(color)"></span>
          </div>
        </div>
      </div>
    </div>
    <div class="item" v-if="currentElement.type === 'aisle'">
      <label for="" class="title">透明度</label>
      <div class="subs grid grid-1 grid-1-1">
        <div class="subs-item">
          <label class="lab" for="">{{currentElement.style.opacity}}</label>
          <input type="range" min="0.2" max="1.0" step="0.1" v-model="currentElement.style.opacity">
        </div>
      </div>
    </div>
    <div class="item">
      <label for="" class="title">旋转</label>
      <div class="subs grid grid-1">
        <div class="subs-item">
          <label class="lab" for="">角度</label>
          <input class="val" type="number"  v-model="currentElement.style.rotate">
        </div>
      </div>
    </div>
    <div class="item">
      <label for="" class="title">阴影</label>
      <div class="subs">
        <div class="subs-item">
          <input class="val-cb"
            type="checkbox"
            v-model="currentElement.style.isApplyShadow"
            true-value=true
            false-value=false
          >
          <span class="val">应用阴影</span>
        </div>
      </div>
    </div>
    <div class="item" v-if="currentElement.type === 'room'">
      <label for="" class="title">材质</label>
      <div class="subs">
        <div class="subs-item">
          <input class="val-cb"
            type="checkbox" v-model="currentElement.style.bgiBool"
            true-value=true
            false-value=false
          >
          <span class="val">应用材质</span>
        </div>
      </div>
    </div>
    <div class="item">
      <label for="" class="title">圆角</label>
      <div class="subs">
        <div class="subs-item">
        <select class="val-s" v-model="currentElement.style.borderRadius">
          <option v-bind:value="0">无</option>
          <option v-bind:value="50">圆角</option>
        </select>
      </div>
    </div>
  </div>
  <div class="item del-item">
    <img class="del"  
      v-bind:class="{
        delDef:currentActiveIndex === -1
      }"
      @click="delComp()" src="./../assets/icon/delete.svg" alt="">
  </div>
  </div>

   <div class="setting-element element" v-if="currentActiveIndex === -1">
    <div class="item">
      <span class="name">{{'多选操作'}}</span>
    </div>
    <div class="item">
      <label for="" class="title">阴影</label>
      <div class="subs">
        <div class="subs-item">
          <input class="val-cb"
            type="checkbox"
            v-model="multipleApplyShadow"
            true-value=true
            false-value=false
            @change="setMultipleState('isApplyShadow', multipleApplyShadow)"
          >
          <span class="val">应用阴影</span>
        </div>
      </div>
    </div>
    <div class="item">
        <label for="" class="title">圆角</label>
        <div class="subs">
          <div class="subs-item">
          <select class="val-s" 
            v-model="multipleApplyBorderRadius"
             @change="setMultipleState('borderRadius', multipleApplyBorderRadius)">
            <option v-bind:value="0">无</option>
            <option v-bind:value="50">圆角</option>
          </select>
        </div>
      </div>
  </div>
  <div class="item del-item">
    <img class="del"  
      v-bind:class="{
        delDef:currentActiveIndex === -1
      }"
      @click="delComp('multipleDel')" src="./../assets/icon/delete.svg" alt="多选删除" title="多选删除">
  </div>
  <div class="item">
      <div class="muls-list">
        <label for="" class="title">多选列表</label>      
        <span class="nums">选中
          <span class="val">{{multipleActiveArr.length}}</span>个组件
        </span>
      </div>
      <div class="muls">
        <div class="muls-item" v-for="(ele, index) in multipleActiveArr" :key="index">
          <span class="ele-index">{{index+1}}</span>
          <img  class="ele-icon" v-bind:src="ele.icon" alt="">
          <span class="ele-name">{{ele.name}}</span>
          <img class="ele-del" @click="delMultipComp(ele, index)" src="./../assets/icon/del_sub.svg" alt="">
        </div>
      </div>
    </div>
  </div>
 </div>
</template>
       
<script>

export default {
  props: {
    currentElement:Object, //当前组件
    currentActiveIndex:Number, // 编辑状态管理
    configs:Object, //页面对象
    multipleActiveArr:Array
  },
  data() {
    return {
      multipleApplyShadow:'true',
      multipleApplyBorderRadius:'0',
      colors:[
        '#d81e06', 
        '#ff7f00',
        '#ffff00',
        '#00ca98', 
        '#0007ff',
        '#13227a',
        '#ffffff',
        '#dbdbdb',
        '#bfbfbf',
        '#4f4f4f',
        '#2c2c2c',
        '#000000'],
      img: {
        l:require('./../assets/icon/align/l.png'),
        l_def:require('./../assets/icon/align/l.png'),
        l_hover:require('./../assets/icon/align/l_h.png'),
        r:require('./../assets/icon/align/r.png'),
        r_def:require('./../assets/icon/align/r.png'),
        r_hover:require('./../assets/icon/align/r_h.png'),
        t:require('./../assets/icon/align/t.png'),
        t_def:require('./../assets/icon/align/t.png'),
        t_hover:require('./../assets/icon/align/t_h.png'),
        b:require('./../assets/icon/align/b.png'),
        b_def:require('./../assets/icon/align/b.png'),
        b_hover:require('./../assets/icon/align/b_h.png'),
        dispersion_l:require('./../assets/icon/align/dispersion_l.png'),
        dispersion_l_def:require('./../assets/icon/align/dispersion_l.png'),
        dispersion_l_hover:require('./../assets/icon/align/dispersion_l_h.png'),
        dispersion_v:require('./../assets/icon/align/dispersion_v.png'),
        dispersion_v_def:require('./../assets/icon/align/dispersion_v.png'),
        dispersion_v_hover:require('./../assets/icon/align/dispersion_v_h.png'),
        save:require('./../assets/icon/save.png'),
        save_def:require('./../assets/icon/save.png'),
        save_hover:require('./../assets/icon/save_h.png'),
        history:require('./../assets/icon/history.png'),
        history_def:require('./../assets/icon/history.png'),
        history_hover:require('./../assets/icon/history_h.png'),
        region:require('./../assets/icon/align/region.png'),
        region_def:require('./../assets/icon/align/region.png'),
        region_hover:require('./../assets/icon/align/region_h.png'),
        output:require('./../assets/icon/contr/output.png'),
        output_def:require('./../assets/icon/contr/output.png'),
        output_hover:require('./../assets/icon/contr/output_h.png'),
      }
    }
  },
  mounted:function() {

  },
  methods: {
    selColor:function(color) {
      this.$emit('selColor',this.currentElement, color);
    },
    delMultipComp:function(comp, index) {
      this.$emit('delMultipComp', comp, index);
    },
    delComp:function(state) {
      this.$emit('delComp', this.currentActiveIndex, state);
    },
    setMultipleState:function(state, val) {
      this.$emit('setMultipleState',state, val)
    },
    changeBg:function(state, val) {
      this.$emit('changeConfig', state, val);
    },
    screen:function() {
      this.$emit('screen');
    },
    getHistory:function() {
      this.$emit('getHistory')
    },
    saveData:function() {
      this.$emit('saveDateToStorage', null , 'custom');
    },
    downloadJSON:function() {
      this.$emit('downloadJSON')
    },
    changeFile:function() {
      let that = this;
      let fileInput = document.getElementById("filePicker").files[0];
      if(!fileInput) {
        return;
      }
      var reader = new FileReader();
      reader.readAsDataURL(fileInput);
      reader.onload = function() 
      {
        that.$emit('changeBgImg', this.result)
      }
    }
  }
}
</script>

<style scoped>
#settings {
  position: relative;
  background: #eee;
  min-height: 820px;
  padding: 0px;
  border: 1px solid #cccc;
  user-select:none;
}
.setting-config {
    position: fixed;
    top: 0px;
    left: 0px;
    width: 100%;
    margin-left: 10px;
    font-size: 16px;
    height: 60px;
    background: #fff;
    z-index: 1000;
    border-bottom: 1px solid #cccccc;
}
.baseMap {
  color: #999;
  font-size: 18px;
  display: inline-block;
  width: 100px;
  position: absolute;
  top: 18px;
}
.config-item{
  height: 60px;
  width: 300px;
  user-select: none;
}
.setting-element {
  position:fixed;
}

.icon {
  width: 26px;
  height: 26px;
  display: inline-block;
  padding: 10px 5px;
  margin-top: 9px;
}
.config-item.bg {
  position: absolute;
  top: 0px;
  font-size: 14px;
  width: 130px;
  left: 200px;
}
.bg .name {
  position: absolute;
  right: 120px;
  top: 19px;
  color:#2c3e50;
  width: 50px;
}
.bg .bgs {
  width: 215px;
  display: inline-block;
  height: 60px;
}
.bg .bg-item {
  cursor: pointer;
  width: 22px;
  height: 22px;
  padding: 17px 2px;
}
.bg .baseMapImgUrl {
    padding: 2px 5px;
    width: 140px;
    display: inline-block;
    margin-top: 15px;
    margin-left: 10px;
    display: -webkit-inline-box;
    position: absolute;
}
.aligins {
  position: absolute;
  right: 570px;
  top:0px;
  cursor: pointer;
}
.aligin {
  width: 610px;
  margin-top: 15px;
  display: grid;
  margin-left: 40px;
  text-align: center;
  grid-template-columns:50px 150px 150px 50px 50px 50px 50px;
}
.aligin-item  {
  cursor: pointer;
  position: relative;
  margin-top: 5px;
}
.aligin-item img:hover {
  color: red;
}
.aligin-item.screen {
  z-index: 9999;
  position: fixed;
  right: 18px;
  top: 16px;
 
}
.contrls {
  z-index: 9999;
  position: absolute;
  right: 80px;
  text-align: center;
  width: 200px;
  height: 59px;
  top: -4px;
  border-right:1px solid #cccccc;
}
.contrls img {
  margin: 20px 10px ;
}
.aligin-item label {
    padding: 2px 4px;
    font-size: 12px;
    position: absolute;
    top: 0px;
    left: 0;
}
.aligin-item  input {
  width: 40px;
  padding: 2px 4px;
  margin-left: 15px;
}
.aligin-item img {
  width: 22px;
  height: 22px;
}
.aligin-item .img {
  position: absolute;
  right: 10px;
}
.item {
  padding: 10px;
  min-height: 30px;
  line-height: 30px;
  position: relative;
}
.item .name {
  border-left: 5px solid #ccc;
  padding: 10px;
  position: absolute;
  left: 0px;
  top:0px;
  width: 100%;
  border-bottom: 1px dashed #cccccc;
}
.muls-list{
  font-size: 14px;
  padding-left: 10px;
  border-left: 2px solid #ccc;
  border-bottom:1px dashed #cccccc;
}
.item .nums { 
  font-size: 12px;
  position: absolute;
  right: 10px;
  top: 14px;
  color:#aaa;
  overflow-y: auto;
  height: 479px;

}
.nums .val {
  color: red;
  padding: 5px;
}
.title {
  font-size: 16px;
  color: #777777;
  height: 40px;
  line-height: 40px;
}
.sub {
  margin: 50px;
}
.grid {
  display: grid;
}
.grid-1 {
  grid-template-columns: 100%;
} 
.grid-1 .subs-item {
  display: grid;
  grid-template-columns: 40px 40%;
}
.grid-1 .subs-item .lab {
  width: 40px;
}
.grid-1-1 .subs-item{
  display: grid;
  grid-template-columns: 40px 70%;
}
.grid-2 {
  grid-template-columns: 50% 50%;
}

.grid-1 .lab,.grid-2 .lab {
  text-align: center;
  width: 25px;
  font-size: 14px;
  display: inline-block;
  color:#aaa;
}
.grid-1 .val ,.grid-2 .val {
  width: 50px;
  padding: 2px 4px;
  height: 16px;
}
.val-cb {
  margin: 10px;
}
.val-s {
  width: 170px;
  padding: 5px 10px;
  margin: 5px;
}
.del-item {
  text-align: center;
}
.del {
    position: relative;
    top: 10px;
    width: 25px;
    cursor: pointer;
    border-radius: 50%;
    padding: 5px;
    box-shadow: 0px 0px 5px rgba(255,0,0,0.3);
}
.del:hover {
  box-shadow: 0px 0px 10px #ccc;
}
#download {
  position: absolute;
  right: 50px;
  width: 30px;
  height: 30px;
  cursor: pointer;
  top: 15px;
}
.muls-item {
  display: inline-block;
  width: 100%;
  cursor: pointer;
  position: relative;
  border-bottom: 1px solid #ccc;
}
.ele-index {
  display: inline-block;
  width: 40px;
  text-align: center;
}
.ele-icon {
  width: 20px;
  height: 20px;
  display: inline-block;
  margin-left: 5px;
  margin-right: 15px;
}
.ele-name {
  width: 100px;
  height: 30px;
  color: #888;
}
.ele-name:hover {
  color: #555;
}
.ele-del {
  opacity: 0.5;
  width: 25px;
  position: absolute;
  right: 10px;
  top: 6px;
}
.cols {
  padding: 5px;
  height: 53px;
}
.col-item {
    width: 20px;
    height: 20px;
    display: inline-block;
    background: red;
    cursor: pointer;
    margin: 1px;
}
.subs-item.full {
 grid-template-columns: 40px 80%;
}
.full .active {
  margin: 0;
  border:1px solid #ffffff;
}

</style>
