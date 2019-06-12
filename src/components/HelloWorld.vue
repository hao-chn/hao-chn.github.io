<template>
  <div class="hello">
    <canvas id="canvas"  width="1000" height="1000" style=" margin:50px auto; display:block; " ></canvas>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
			chinesecNum:['零','一','二','三','四','五','六','七','八','九','十'],
			unit:['十','百','千','万'],
			season:['春','夏','秋','冬'],
			year:'2019',
			
    }
  },
  mounted(){
		this.init()
  },
  methods:{
		timeCount(){
			let _time = new Date()
			_time.getYear(); //获取当前年份(2位)  
			_time.getFullYear(); //获取完整的年份(4位,1970-????)  
			_time.getMonth(); //获取当前月份(0-11,0代表1月)         // 所以获取当前月份是_time.getMonth()+1;   
			_time.getDate(); //获取当前日(1-31)  
			_time.getDay(); //获取当前星期X(0-6,0代表星期天)  
			_time.getTime(); //获取当前时间(从1970.1.1开始的毫秒数)  
			_time.getHours(); //获取当前小时数(0-23)  
			_time.getMinutes(); //获取当前分钟数(0-59)  
			_time.getSeconds(); //获取当前秒数(0-59)  
			_time.getMilliseconds(); //获取当前毫秒数(0-999)  
			_time.toLocaleDateString(); //获取当前日期  
			var mytime=_time.toLocaleTimeString(); //获取当前时间  
			_time.toLocaleString( ); //获取日期与时间  
			
		},
		month(data){
			// console.log(data)
			data++
			console.log(data)
			return this._switch(data) + '月'
		},
		// month(data){
		// 	// console.log(data)
		// 	console.log(data)
		// 	return this._switch(data) + '月'
		// },
		_switch(data){
			data++;
			if(data > 100 ){
				return this.chinesecNum[parseInt(data/100)] + this.unit[1] + this.chinesecNum[parseInt(data/10)] + this.unit[0] + chinesecNum[data%10]
			}else if(data > 10 ){
				return  (parseInt(data/10) == 1?'':this.chinesecNum[parseInt(data/10)]) + this.unit[0] + (parseInt(data%10)==0?'':this.chinesecNum[data%10])
			}else{
				return this.chinesecNum[data]
			}
		},
    init(){
      let dom = document.getElementById('canvas');
      let cxt =dom.getContext('2d');
			let _r = 450
			let _inner = 70;
			cxt.font="12px Arial";
			// 月份刻度
			for(var i=0; i<12; i++){
				cxt.save();   //设置旋转环境
				cxt.lineWidth=3;//设置时针的样式
				// cxt.strokeStyle="#000";
				cxt.translate(_r,_r);//设置异次元空间的原点
				cxt.rotate(i * 30*Math.PI/180);//设置旋转角度
				cxt.fillText(this._switch(i) + ' 月',_inner,0);
				cxt.closePath();
				cxt.restore();  //将旋转之后的元素放回原画布
			}
			// 日刻度
			for(var i=0; i<30; i++){
				cxt.save();   //设置旋转环境
				cxt.lineWidth=3;//设置时针的样式
				// cxt.strokeStyle="#000";
				cxt.translate(_r,_r);//设置异次元空间的原点
				cxt.rotate(i * 12*Math.PI/180);//设置旋转角度
				cxt.fillText(this._switch(i) + " 号",_inner*2,0);

				cxt.closePath();
				cxt.restore();  //将旋转之后的元素放回原画布
			}
      //时针刻度
      for(var i=0; i<12; i++){
				cxt.save();   //设置旋转环境
				cxt.lineWidth=3;//设置时针的样式
				cxt.strokeStyle="#000";
				cxt.translate(_r,_r);//设置异次元空间的原点
				cxt.rotate(i * 30*Math.PI/180);//设置旋转角度
				cxt.fillText(this._switch(i) + " 点",_inner*3,0);
				cxt.closePath();
				cxt.restore();  //将旋转之后的元素放回原画布
      }
			//分针刻度
			for(var j=0; j<60; j++){
				cxt.save();
				cxt.lineWidth=4;
				cxt.strokeStyle="#000";
				cxt.translate(_r,_r);
				cxt.rotate(j * 6 *Math.PI/180);
				cxt.fillText(this._switch(j) + " 分",_inner*4,0);
				cxt.closePath();
				cxt.restore();  
			}
			//秒针刻度
			for(var j=0; j<60; j++){
				cxt.save();
				cxt.lineWidth=2;
				// cxt.strokeStyle="#000";
				cxt.translate(_r,_r);
				cxt.rotate(j * 6 * Math.PI/180);
				cxt.fillText(this._switch(j) + " 秒",_inner*5,0);
				cxt.closePath();
				cxt.restore();  
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
