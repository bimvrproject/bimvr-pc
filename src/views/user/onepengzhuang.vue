<template>
	<div>
		<div class="zongone">
			<!-- <iframe src="https://www.baidu.com/s?tn=news&rtt=1&bsst=1&wd=%E9%A6%99%E6%B8%AF&cl=2&origin=ps" frameborder="0" style="width:100%;height:100%;"></iframe> -->
		</div>
		<div class="lefttopjzm">
			<div class="leftjzm">
				<img class="logojzm" src="../../assets/image/jinghekeji.png" />
				<Xunilogo v-show="xianyinxuni"></Xunilogo>
			</div>
		</div>
		<div>
			<!-- nav -->
			<div class="hometopjzmone" v-show="hometop">
				<!-- 下拉菜单---项目 -->
				<el-dropdown style="float: left;margin-left:-1.4rem;">
					<div class="el-dropdown-link" @click="fnopxm">
						<img class="xmimgone" src="../../assets/image/bluefz.png" style="vertical-align:text-bottom;"/>
						<span class="xmone">项目</span>
						<i style="display:inline-block;width:0.45rem;height:0.53125rem‬;margin-left:0.2rem;">
							<img src="../../assets/image/shang.png" alt="" style="width: 100%;height: 100%;" />
						</i>
					</div>
					<Newjian v-show="xianyin"></Newjian>
				</el-dropdown>
				<!-- 下拉菜单---项目--结束 -->
				<!-- 下拉菜单---社区 -->
				<el-dropdown style="float: left; margin-left:1.5rem;">
					<div class="el-dropdown-link" @click="fnopsq"  @mouseenter="fnhsq()" @mouseleave="fnhsqlev()">
						<img class="sqimgone" :src="hsq" style="vertical-align:text-bottom;"/>
						<i class="sqone" :style="hsqcolor">社区</i>
						<!-- <i class="el-icon-arrow-down el-icon--right"></i> -->
					</div>
				</el-dropdown>
				<!-- 下拉菜单---社区--结束 -->
				<!-- 下拉菜单---更多 -->
				<div class="moretopcomone" style="height:0.93125rem;" @mouseenter="fnmorone()" @mouseleave="fnmorlevone()">
					<img :src="moretb" alt="" style="width:0.84375rem;height:0.8125rem;margin-right:0.16rem;float:left;vertical-align:text-bottom;">
					   <span class="hgmorecomone">更多</span>
						<i style="display:inline-block;width:0.45rem;height:0.53125rem‬;margin-left:0.2rem;">
						  <img :src="nmgd" alt="" style="width: 100%;height: 100%;" />
						</i>
						  <div class="moocomone" style="margin-top:0.1rem;">
						 	<div class="mores1comone">
						 		<a href="http://www.jh-bim.com/home/solution" target="_blank" style="display:inline-block;color:#666666;width:4.5rem;">帮助</a>
						 	</div>
						 	<div class="mores1comone" @click="fnabout">联系我们</div>
						 	<div class="moresbcomone">版本号: v 1.0.3</div>
						 </div>
				</div>
				<!-- 下拉菜单---更多--结束 -->
			</div>
			<!-- 新建项目/管线综合/图纸 -->
			<div style="width:18.75rem;height:0.6875rem;position: absolute;top:3.93125rem;left:8.21875rem;text-align:left;cursor:pointer;">
				<span style="margin-right:0.1875rem;color:#2180ED;font-size:0.5rem;font-weight:500;cursor:pointer;float:left;line-height:0.6875rem;">
					{{projecttitonepz}}
				</span>
				<i style="font-weight:900;font-style:normal;font-size:0.625rem;cursor:pointer;float:left;line-height:0.6875rem;">/</i>
				<span style="margin-right:0.1875rem;color:#2180ED;font-size:0.5rem;font-weight:500;cursor:pointer;float:left;margin-left:0.15625rem;line-height:0.7575rem;">管线综合</span>
				<i style="font-weight:900;font-style:normal;font-size:0.625rem;cursor:pointer;float:left;line-height:0.6875rem;">/</i>
				<span style="color:#2180ED;font-size:0.5rem;font-weight:500;cursor:pointer;margin-left:0.15625rem;float:left;line-height:0.7575rem;">模型</span>
			</div>
			<!-- 碰撞点数 -->
			<div class="numberonep">
				<div class="numbersonep">此处为第一处碰撞点</div>
				<span class="backonep" @click="backs()">返回</span>
				<span class="lookonep" @click="next1()">前往下一处</span>
			</div>
		</div>
		<!-- 点击联系我们的遮罩 -->
		<div style="width:59.9375rem;height:33.65625rem;position: fixed;top: 0;left: 0;right: 0;bottom: 0;background: rgba(0, 0, 0, 0.2);" v-show="abouts" @click="fnaboutmark"></div>
	</div>
</template>
<script>
import api from '@/api/api.js';
import qs from 'qs';
import Newjian from './newjian';
import Xunilogo from './xunilogo';
// import Zheader from './header';
export default {
	data() {
		return {
			panduan: false,
			xianyin: false,
			xianyinxuni: false,
			hometop: true,
			//总的等陆头部
			zheaderxy: true,
			lmore: require('../../assets/image/pmjtxia.png'),
			// 更多下拉
			nmgd: require('../../assets/image/pmjtxia.png'),
			// 联系我们
			abouts: false,
			// 社区默认状态
			hsq:require('../../assets/image/sq@2x.png'),
			hsqcolor:"color:#333333",
			moretb: require('../../assets/image/more@2x.png'),
			projecttitonepz:''
		};
	},
	components: {
		Newjian,
		Xunilogo
		// Zheader
	},
	created() {
		// 接收一下title
		this.projecttitonepz = sessionStorage.getItem('projecttit');
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
	},
	mounted() {
		this.$eventbus.$emit('cezhan2', 'pengzhuang');
		this.$eventbus.$emit('hometop');
	},
	methods: {
		// 点击新建项目
		fnon() {
			this.$router.push('/gxmoxin');
		},
		// 点击管线综合
		fnong() {
			this.$router.push('/gxmoxin');
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
	  fnmorone(){
	  	this.moretb = require('../../assets/image/moress.png');
	  },
	  // 移出更多
	   fnmorlevone(){
	  	 this.moretb = require('../../assets/image/more@2x.png');
	  },
		// 点击项目
		fnopxm() {
			this.$router.push('/Login');
		},
		// 点击社区
		fnopsq() {
			this.$router.push('/');
		},
		fns() {
			this.xianyin = !this.xianyin;
			// this.xianyinxuni = false;
			this.$eventbus.$emit('showyin');
		},
		// fnxuni(){
		// 	this.xianyin = false;
		// },
		// fn4() {
		// 	this.loginWindow = 'display:block';
		// },
		// look() {
		// 	this.$router.push('/onepengzhuang');
		// },
		next1() {
			this.$router.push('/twopengzhuang');
		},
		backs() {
			this.$router.push('/gxpengzhuang');
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
.moretopcomone{
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
.hgmorecomone{
	color:#333333;
}
.moocomone{
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
.mores1comone{
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
.moresbcomone{
		border: 0;
		text-align: left;
		line-height:0.9rem;
		color: #666666;
		font-size:0.46rem;
		font-weight: 500;
		/* background:red; */
	}
	.moretopcomone:hover .moocomone{
		  display:block;
	}
	.moretopcomone:hover .hgmorecomone{
		 color:#2180ED
	}
	.moretopcomone:hover .shouye{
		 transform:rotate(180deg);
	}
.onemore {
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
.onemoo {
	width: 4.75rem;
	/* 		height: 195px; */
	/* 	background: url(../../assets/image/mores.png); */
	padding-left: 0.1rem;
	padding-right: 0.25rem;
	cursor: pointer;
}
.onemores1 {
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
.onemoresb {
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
.zongone {
	width: 59.9375rem;
	height: 33.65625rem;
	/* background:green; */
	background: url(../../assets/image/onep.png) no-repeat;
	background-repeat: no-repeat;
	background-size: 100% 100%;
	background-color: rgba(225, 225, 225, 0.9);
	position: relative;
}
.el-main {
	/* padding-left:50px; */
	/* padding-top:29px; */
	padding: 0 !important;
}
/* 主页top部分*/
.hometopjzmone {
	/* width:46.875rem;
	height:1.78125rem; */
	position: absolute;
	top:0.6275rem;
	left:7.2rem;
	/* background:red; */
	line-height: 1.78125rem;
}
/* 左侧边栏 */
.left {
	width: 217px;
	height: 987px;
	/* background:blue; */
	padding-right: 10px;
}
.logojzm {
	width: 3.65625rem;
	height: 0.875rem;
	padding-left: 0.65625rem;
	padding-top: 0.90625rem;
	padding-right: 0rem;
}
.lefttopjzm {
	width: 6.75rem;
	height: 1.875rem;
	/* 	background-color:green;
			background: url(../../assets/image/homecebian8@2x.png); */
	position: absolute;
	top: 0rem;
}
.el-dropdown-link {
	cursor: pointer;
	color: #333333;
}
.xmimgone {
	width: 0.84375rem;
	height: 0.8125rem;
	padding-left: 2.5rem;
	padding-top: 0.0625rem;
}
.xmone {
	width: 0.84375rem;
	height: 0.53125‬;
	font-size: 0.625rem;
	font-family: MicrosoftYaHei;
	font-weight: 400;
	color: #2180ed;
	font-style: normal;
	padding-left: 0.15625rem;
	line-height: 0.53125rem;
}
.sqimgone,
.bjimgone {
	width: 0.84375rem;
	height: 0.8125rem;
}
.sqone {
	width: 1.25rem;
	height: 0.5625rem;
	font-size: 0.625rem;
	font-family: MicrosoftYaHei;
	font-weight: 400;
	padding-left: 0.1875rem;
	font-style: normal;
}
.moreimgone {
	width: 0.78125rem‬;
	height: 0.78125rem;
}
.moreone {
	width: 1.21875rem;
	height: 0.59375rem;
	font-size: 0.625rem;
	font-style: normal;
	padding-left: 0.15625rem;
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
/* 查看碰撞点 */
.numberonep {
	width: 12.5rem;
	height: 5.5625rem;
	/* 	background: rgba(225, 225, 225, 0.3); */
	background: url(../../assets/image/onchu.png) no-repeat;
	background-size: 12.5rem 5.5625rem;
	position: absolute;
	top: 9.625rem;
	left: 17.4rem;
	/* border-radius:0.3125rem;
	border:0.0625rem solid #ffffff; */
	cursor: pointer;
}
.numbersonep {
	width: 12.4rem;
	height: 1.575rem;
	font-size: 0.9375rem;
	color: #333333;
	line-height: 1.975rem;
	font-weight: 500;
	font-family: PingFang;
	/* 	background:red; */
	margin-top: 1.3rem;
}
.lookonep {
	width: 5.3125rem;
	height: 1.25rem;
	background: #2180ed;
	display: inline-block;
	font-size: 0.6875rem;
	color: rgba(255, 255, 255, 1);
	font-weight: 500;
	font-family: PingFang;
	margin-top: 0.78125rem;
	border-radius: 0.625rem;
	line-height: 1.25rem;
}
.backonep {
	width: 5.3125rem;
	height: 1.25rem;
	background: #ffffff;
	display: inline-block;
	font-size: 0.6875rem;
	color: rgba(102, 102, 102, 1);
	font-weight: 500;
	font-family: PingFang;
	margin-top: 0.78125rem;
	border-radius: 0.625rem;
	line-height: 1.25rem;
	margin-right: 0.46875rem;
}
</style>
