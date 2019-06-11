<template>
  <div class="hello">
    <canvas id="canvas"  width="500" height="500" style=" margin:50px auto; display:block; " ></canvas>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  mounted(){
		this.init()
  },
  methods:{
    init(){
      let dom = document.getElementById('canvas');
      let cxt =dom.getContext('2d');
      //表盘（蓝色）
			cxt.beginPath();  //画笔开始
			cxt.lineWidth = 5;  //设置画笔的线宽
			cxt.strokeStyle="blue";  //设置画笔的颜色
			cxt.arc(250,250,200,0,360,false);  //绘制圆形，坐标250,250 半径200，整圆（0-360度），false表示顺时针
			cxt.stroke();   //绘图
			cxt.closePath();  //结束画布

			let cxt1 = cxt
      //时针刻度
      for(var cnet=0; cnet<12; cnet++){
				console.log(cnet)
				cxt1.save();   //设置旋转环境
				//设置时针的样式
				cxt1.lineWidth=7;
				cxt1.strokeStyle="#000";

				cxt1.translate(250 + cnet*12,250 + cnet*12);//设置异次元空间的原点
				cxt1.rotate(30*Math.PI/180);//设置旋转角度
				cxt1.beginPath();  //画笔开始
				cxt1.moveTo(0,-170);   //画线， 从坐标0，-170开始
				cxt1.lineTo(0,-190);   //到坐标0，-190结束
				cxt1.stroke();   //绘图
				cxt1.closePath();
				cxt1.restore();  //将旋转之后的元素放回原画布
      }

    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
