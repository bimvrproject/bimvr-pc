<template>
	<div>
		<div class="zongjc">
			<iframe :src="urladdress" frameborder="0" style="width:75%;height:100%;"></iframe>
		</div>
		<div class="lefttopjzm">
			<div class="leftjzm">
				<img class="logojzm" src="../../assets/image/jinghekeji.png" />
				<Xunilogo v-show="xianyinxuni"></Xunilogo>
			</div>
		</div>
		<div class="box">
			<!-- nav -->
			<div class="hometopjzcl" v-show="hometop">
				<!-- 下拉菜单---项目 -->
				<el-dropdown style="float: left;margin-left:-1.4rem;">
					<div class="el-dropdown-link" @click="fnjzclxm">
						<img class="xmimgs" src="../../assets/image/bluefz.png" alt="" style="vertical-align:text-bottom;"/>
						 <span class="xms">项目</span>
						<i style="display:inline-block;width:0.45rem;height:0.53125rem‬;margin-left:0.2rem;">
							<img src="../../assets/image/shang.png" alt="" style="width:100%;height:100%;" />
						</i>
					</div>
					<Newjian v-show="xianyin"></Newjian>
				</el-dropdown>
				<!-- 下拉菜单---项目--结束 -->
				<!-- 下拉菜单---社区 -->
				<el-dropdown style="float: left;margin-left:1.5rem;">
					<div class="el-dropdown-link" @click="fnjzclsq" @mouseenter="fnhsq()" @mouseleave="fnhsqlev()">
						<img class="sqimgsj" :src="hsq" style="vertical-align:text-bottom;"/>
						<i class="sqsj" :style="hsqcolor">社区</i>
						<!-- 	<i class="el-icon-arrow-down el-icon--right"></i> -->
					</div>
				</el-dropdown>
				<!-- 下拉菜单---社区--结束 -->
				<!-- 下拉菜单---更多 -->
				<div class="moretopcomjzcl" style="height:0.93125rem;" @mouseenter="fnmorjzcl()" @mouseleave="fnmorlevjzcl()">
					<img  :src="moretb"  alt="" style="width:0.84375rem;height:0.8125rem;margin-right:0.16rem;float:left;vertical-align:text-bottom;">
					   <span class="hgmorecomjzcl">更多</span>
						<i style="display:inline-block;width:0.45rem;height:0.53125rem‬;margin-left:0.2rem;">
						  <img :src="nmgd" alt="" style="width: 100%;height: 100%;" />
						</i>
						  <div class="moocomjzcl" style="margin-top:0.1rem;">
						 	<div class="mores1comjzcl">
						 		<a href="http://www.jh-bim.com/home/solution" target="_blank" style="display:inline-block;color:#666666;width:4.5rem;">帮助</a>
						 	</div>
						 	<div class="mores1comjzcl" @click="fnabout">联系我们</div>
						 	<div class="moresbcomjzcl">版本号: v 1.0.3</div>
						 </div>
				</div>
				<!-- 下拉菜单---更多--结束 -->
			</div>
			<!-- 新建项目/管线综合/图纸 -->
			<div style="width:18.75rem;height:0.6875rem;position:absolute;top:3.93125rem;left:8.21875rem;text-align:left;cursor:pointer;">
				<span style="margin-right:0.1875rem;color:#2180ED;font-size:0.5rem;font-weight:500;float:left;line-height:0.6875rem;">
					{{projecttitjzcl}}
				</span>
				<i style="font-weight:900;font-style:normal;font-size:0.625rem;float:left;line-height:0.6875rem;">/</i>
				<span style="margin-right:0.1875rem;margin-left:0.15625rem;color:#2180ED;font-size:0.5rem;font-weight:500;float:left;line-height:0.7575rem;">建筑结构</span>
				<i style="font-weight:900;font-style:normal;font-size:0.625rem;float:left;line-height:0.6875rem;">/</i>
				<span style="color:#2180ED;font-size:0.5rem;font-weight:500;margin-left:0.15625rem;float:left;line-height:0.7575rem;">材料</span>
			</div>
			<!-- 中间部分上传 -->
			<div class="jzcldraw" v-show="jzchialiaoshow">
				<!-- 中间图纸的图片 -->
				<div class="jzcldrawtop">
					<img src="../../assets/image/clsc.png" alt="">
				</div>
				<!-- 中间上传图纸的汉字 -->
				<div class="jzcldrawhz">
					这里还没有材料清单,需要上传哦
				</div>
						<!-- 上传按钮-->
				<div class="jzcldrawbtn">
					 <div>
						<uploader :file-status-text="statusText" :options="options"  @file-complete="onFileSuccess">
							<!-- <uploader-unsupport></uploader-unsupport> -->
							<uploader-drop class="jzcldrawdrop"><uploader-btn :directory="false" :single="true" class="jzcldrawbtn" :attrs="attrs">上传材料清单</uploader-btn></uploader-drop>
								<uploader-list class="jzyangshi"></uploader-list>
						</uploader>
					</div>
				</div>
				
			</div>
			<!-- 中间部分上传结束 -->
		</div>
	<!-- 点击联系我们的遮罩 -->
	<div style="width:59.9375rem;height:33.65625rem;position: fixed;top: 0;left: 0;right: 0;bottom: 0;background: rgba(0, 0, 0, 0.2);" v-show="abouts" @click="fnaboutmark"></div>
	</div>
</template>
<script>
import api from '@/api/api.js';
import axios from 'axios';
import qs from 'qs';
import Newjian from './newjian';
import Xunilogo from './xunilogo';
// import Zheader from './header';
export default {
	data() {
		return {
			urladdress:"", //exceltohtml的地址
			jzchialiaoshow:true,		//显示上传功能
			title: '12312313122',
			panduan: false,
			xianyin: false,
			xianyinxuni: false,
			hometop: true,
			// 联系我们
			abouts: false,
			lmore: require('../../assets/image/pmjtxia.png'),
			// 更多下拉
			nmgd: require('../../assets/image/pmjtxia.png'),
			options: {
				target: api.Uploadjzprice, //SpringBoot后台接收文件夹数据的接口
				testChunks: false, //是否分片-不分片
				chunkSize: '2048000000000'
			},
			statusText: {
				success: '成功了',
				error: '出错了',
				uploading: '上传中',
				paused: '暂停中',
				waiting: '等待中'
			},
				//总的等陆头部
			// zheaderxy:true
			// 社区默认状态
			hsq:require('../../assets/image/sq@2x.png'),
			hsqcolor:"color:#333333",
			moretb: require('../../assets/image/more@2x.png'),
			//上传文件的类型限制
			attrs: {
				accept: ' .xls, .xlsx'
			},
			projecttitjzcl:""
		};
	},
	components: {
		Newjian,
		Xunilogo,
		// Zheader
	},
	created() {
		// 接收一下title
		this.projecttitjzcl = sessionStorage.getItem('projecttit');
		var projectid=sessionStorage.getItem("projectid");
		this.$eventbus.$on('shows', () => {
			this.xianyinxuni = true;
		});
		this.$eventbus.$on('showyin', () => {
			this.xianyinxuni = false;
		});
		// console.log(this.xianyinxuni)
		this.$eventbus.$on('hometop', () => {
			this.hometop = true;
		});
		this.$eventbus.$on('xianyin', () => {
			this.xianyin = true;
		});
		this.$eventbus.$emit('shows');
		//初始化显示exceltohtml
		axios.get(api.Addressurl+"/"+projectid+"/"+1).then(result=>{
			if(result.data!=null){
				this.jzchialiaoshow=false;
				axios.get(api.Exceltohtml+'?addressurl='+result.data.url).then(result=>{
					this.urladdress=result.data;
				})
			}
		})
		
	},
	mounted() {
		this.$eventbus.$emit('cezhan', 'cailiao');
		this.$eventbus.$emit('hometop');
	},
	methods: {
		//上传成功后的事件 显示exceltohtml
		onFileSuccess(){
			var projectid=sessionStorage.getItem("projectid");
			axios.get(api.Addressurl+"/"+projectid+"/"+1).then(result=>{
				if(result.data!=null){
					axios.get(api.Exceltohtml+'?addressurl='+result.data.url).then(result=>{
						this.urladdress=result.data;
						this.jzchialiaoshow=false;
					})
				}
			})
		},
		// 点击联系我们
		fnabout() {
			this.$eventbus.$emit('abouts');
			this.abouts = true;
		},
		// 点击联系之后出现的遮罩
		fnaboutmark() {
			this.$eventbus.$emit('aboutsbi');
			this.abouts = false;
		},
		// 划过更多
		fnmorjzcl(){
			this.moretb = require('../../assets/image/moress.png');
			this.nmgd = require('../../assets/image/shang.png');
		},
		// 移出更多
		fnmorlevjzcl(){
			 this.moretb = require('../../assets/image/more@2x.png');
			 this.nmgd = require('../../assets/image/pmjtxia.png');
		},
		// 移出社区
		fnleave() {
			this.lmore = require('../../assets/image/pmjtxia.png');
		},
		fns() {
			this.xianyin = !this.xianyin;
			// this.xianyinxuni = false;
			this.$eventbus.$emit('showyin');
		},
		// fnxuni(){
		// 	this.xianyin = false;
		// },
		// 点击项目
		fnjzclxm(){
			this.$router.push('/Login');
		},
	// 点击社区
	fnjzclsq(){
		this.$router.push('/');
	},
	// 移入社区的时候
	fnhsq(){
		this.hsq = require('../../assets/image/shequ.png')
		this.hsqcolor = "color:#2180ED"
	},
	// 移出社区的时候
	fnhsqlev(){
		this.hsq = require('../../assets/image/sq@2x.png'),
		this.hsqcolor = "color:#333333"
		}
	}
};
</script>

<style>
	/* 更多 */
.moretopcomjzcl{
	position:relative;
	 float: left;
	 margin-left:-1.4rem;
	 font-size: 0.625rem;
	 font-family: MicrosoftYaHei;
	 font-weight: 400;
	/* color:#2180ED; */
	 font-style: normal;
	 line-height: 0.93125rem;
	/* background-color:red; */
	 margin-top:0.380rem;
	 margin-left:1.62rem;
	 text-align:left;
	 cursor:pointer;
}
.hgmorecomjzcl{
	color:#333333;
}
.moocomjzcl{
		width:4.75rem;
	/* width: 183px;
	height: 195px; */
	/* background: url(../../assets/image/mores.png); */
	background:rgba(225,225,225,.2);
	padding-left:0.2rem;
	padding-right:0.25rem;
	cursor: pointer;
	display:none;
}	
.mores1comjzcl{
	width:4.65rem;
		height:0.9rem;
		border-bottom: 1px solid #999999;
		text-align: left;
		line-height:1rem;
		color: #666666;
		font-size:0.46rem;
		font-weight: 500;
	/* 	background:red; */
}
.moresbcomjzcl{
		border: 0;
		text-align: left;
		line-height:0.9rem;
		color: #666666;
		font-size:0.46rem;
		font-weight: 500;
		/* background:red; */
	}
	.moretopcomjzcl:hover .moocomjzcl{
		  display:block;
	}
	.moretopcomjzcl:hover .hgmorecomjzcl{
		 color:#2180ED
	}
	.moretopcomjzcl:hover .shouye{
		 transform:rotate(180deg);
	}
		
	
	
.jzclmore {
	background: rgba(225, 225, 225, 0.3);
	position: absolute;
	top: 2.125rem !important;
	left: 16.175rem !important;
	border: none;
	padding: 0.1rem;
	border-radius: 0rem !important;
}
.popper__arrow {
	border-width: 0rem !important;
	left: 0 !important;
	overflow: hidden;
}
.jzclmoo {
	width: 4.75rem;
	/* 		height: 195px; */
	/* 	background: url(../../assets/image/mores.png); */
	padding-left: 0.1rem;
	padding-right: 0.25rem;
	cursor: pointer;
}
.jzclmores1 {
	width: 4.65rem;
	height: 0.9rem;
	border-bottom: 1px solid #999999;
	text-align: left;
	line-height: 0.9rem;
	color: #666666;
	font-size: 0.46rem;
	font-weight: 500;
	/* 	background:red; */
}
.jzclmoresb {
	border: 0;
	text-align: left;
	line-height: 0.9rem;
	color: #666666;
	font-size: 0.46rem;
	font-weight: 500;
	/* 	background:red; */
}
a {
	color: #333333;
	text-decoration: none;
}
* {
	padding: 0;
	margin: 0;
}
.zongjc {
  width:60rem;
	height:33.75rem;
	/* 	background:green; */
	/* background: url(../../assets/image/bjt.jpg);
	background-repeat: no-repeat;
	background-size: 100% 100%; */
	/* 	background-attachment: fixed; */
	position: relative;
}
.el-main {
	/* padding-left:50px; */
	/* padding-top:29px; */
	padding: 0 !important;
}
/* 主页top部分*/
.hometopjzcl {
	position: absolute;
	top:0.6275rem;
	left:7.2rem;
	/* background:red; */
	line-height:1.78125rem;
}
/* 左侧边栏 */
.left {
	width: 217px;
	height: 987px;
	padding-right: 10px;
}
.logojzm {
	width: 3.65625rem;
	height: 0.875rem;
	padding-left: 0.65625rem;
	padding-top: 0.90625rem;
	padding-right: 0px;
}
.lefttopjzm {
	width:6.75rem;
	height:1.875rem;
	/* 	background-color:green;
			background: url(../../assets/image/homecebian8@2x.png); */
	position: absolute;
	top: 0rem;
}
.el-dropdown-link {
	cursor: pointer;
	color: #333333;
}
.xmimgs {
	width:0.84375rem;
	height:0.8125rem;
	padding-left:2.5rem;
	padding-top:0.0625rem;
}
.xms {
	width:0.84375rem;
	height:0.53125‬;
	font-size:0.625rem;
	font-family: MicrosoftYaHei;
	font-weight: 400;
	color: #2180ed;
	font-style: normal;
	padding-left: 0.15625rem;
	line-height: 0.53125rem;
}
.sqimgsj{
	width:0.84375rem;
	height: 0.8125rem;
}
.sqsj {
	width:1.25rem;
	height:0.5625rem;
	font-size:0.625rem;
	font-family: MicrosoftYaHei;
	font-weight: 400;
	padding-left:0.1875rem;
	font-style: normal;
}
.bj {
	width: 40px;
	height: 18px;
	font-size: 20px;
	font-family: MicrosoftYaHei;
	font-weight: 400;
	padding-left: 6px;
	font-style: normal;
}
.moreimg {
	width: 0.78125rem‬;
	height: 0.78125rem;
}
.more {
	width:1.21875rem;
	height:0.59375rem;
	font-size:0.625rem;
	font-style: normal;
	padding-left:0.15625rem;
	font-family: MicrosoftYaHei;
	font-weight: 400;
	color: rgba(51, 51, 51, 1);
}
.el-dropdown-link2 {
	cursor: pointer;
	color: #2180ed;
}
.el-icon-arrow-down {
	font-size: 20px;
}
/* 中间部分上传总体 */
.jzcldraw{
	width:15.625rem;
	height:15.625rem;
/* 	background:red; */
	position:absolute;
	left:25rem;
	top:9rem;
}
.jzcldrawtop{
  width:12.84375rem;
	height:8.28125rem;
	/* background:plum; */
	margin-left:1.4rem;
}
.jzcldrawtop img{
	width:100%;
	height:100%;
}
.jzcldrawhz{
	width:15.625rem;
			 height:3rem;
			/* background:blue; */
			 font-size:0.9375rem;
			 font-family:PingFang SC;
			 font-weight:500;
			 color:rgba(51,51,51,1);
			 line-height:3.8rem;
	}
 .jzcldrawdrop{
 	/* padding:0.3125rem; */
 	 border:0 !important;
 	 background-color:#FFFFFF !important;
 	 width:4.76875rem !important;
 	 height:1.375rem !important;
 	 margin-top:1.06875rem;
 	 border-radius:0 !important;
 	/* line-height:1.25rem; */
 	/* font-size:0.3875rem; */
 	font-family:PingFang SC;
 	font-weight:500;
 	color:rgba(255,255,255,1);
 	background:url(../../assets/image/pmd.png) no-repeat;
 	background-size:100% 75%;
 	display:flex;
 	justify-content:center;
	margin-left:5.3rem;
  }
 .jzcldrawbtn{
 	/* padding:0.125rem 0.25rem !important; */
 	line-height:0.8rem !important;
 	border-radius:0 !important;
 	font-size:0.6125rem !important;
 	width:4.76875rem !important;
 	height:0.775rem !important;
	border: none !important;
	color: #ffffff !important;
	padding:0.03125rem 0.25rem !important;
 }
 .jzyangshi{
 	left: 1rem;
 	width: 14.375rem;
 }
</style>
