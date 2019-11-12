<template>
	<view>
		<view>
		<text class="tips"><image src="../../static/content_icon.png" style="width: 20px;height: 20px;align-items: center;"></image>想记录的内容：</text>
		<textarea type="text" v-model="contents" value=""></textarea>
		<text class="tips"><image src="../../static/title_icon.png" style="width: 20px;height: 20px;align-items: center;"></image>取个标题吧：</text>
		<input type="text" v-model="title" value="">
		<text class="tips"><image src="../../static/tip_icon.png" style="width: 20px;height: 20px;align-items: center;"></image>需要备注嘛：</text>
		<input type="text" v-model="note" value="">
			<button type="primary" @click="add(index)" :class="['add']">记录</button>
			</view>
			
		<view class="tipcontent">
		<uni-card v-for="(item,index) in tip" :key="index"  :class="['tiptxt']"
		 :title="item.title" 
		 :extra="item.currentTime " 
			:note="item.note" 
			thumbnail="https://image.flaticon.com/icons/svg/148/148828.svg"
			mode="title"
			>
			{{item.contents}}
			<view><button :class="['delbtn']" @click="del(index)" type="warn">删除</button></view>
		</uni-card>
		<br>
		</view>
		
	</view>
</template>

<script>
	import uniCard from "@/components/uni-card/uni-card"
	export default {
		components:{uniCard},
		data(){
			 return{
				tip:[],
				title:'',
				contents:'', 
				note:'',
				timer:'', // 定时器
				currentTime: new Date()
			 }
		},
		created() {
		    var _this = this; 
		    this.timer = setInterval(function() {
		      _this.currentTime = 
		        new Date().getFullYear() +
		        "-" +
		        (new Date().getMonth() + 1) +
		        "-" +
		        new Date().getDate() +
		        " " +
		        new Date().getHours() +
		        ":" +
		        new Date().getMinutes() +
		        ":" +
		        new Date().getSeconds();
		    }, 1000);
		  },
		beforeDestroy() {
		    if (this.timer) {
		      clearInterval(this.timer); 
		    }
		  },
		 	appendZero(obj) {
		 	if (obj < 10) {
		 	return "0" + obj;
		 	} else {
		 	return obj;
		 	} 
		 	},
			getStorage: function(){
				uni.setStorage({
				key:'index',
				data:{},
				success:function(){
					console.log('存入成功');
				},
				fail:function(){
					console.log('存入失败');
				}
		})
		},
		 methods:{
			add(index){
				if(this.contents.length == 0){
					uni.showToast({
						title:'内容为空',
						mask:true,
						image:'/static/cuowu.png',
					})
				}else{
				this.tip.unshift({contents:this.contents,title:this.title,note:this.note,icon:this.icon,currentTime:this.currentTime});
				// 置空输入框
				this.contents='';
				this.note='';
				this.title='';
				}
			},
			del(index){
				this.tip.splice(index,1)
			},
		}
}
</script>

<style>
input[type=text]{
	width:95%;
	height: 35px;
	border:1px solid #ebebeb;
	border-radius: 8px;
	background-color: #F8F8F8;
	font-size:15px;
}
textarea{
		width:95%;
		height: 100px;
		border:1px;
		border-radius: 8px;
		background-color: #F8F8F8;
		font-size:15px
}
.icon{
	width: 50px;
	height: 50px;
	margin: 10px 20px;
}
 .delbtn{
	width: 70px;
	height: 30px;
	border: 1px;
	border-radius:9px;
	float: right;
	text-align: center;
	font-size: 17px;
	font-weight: 400;
}
.add{
	margin: 20px auto;
}
.tips{
	color: gray;
	font-size:16px
}
</style>
