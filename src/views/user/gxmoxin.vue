<template>
	<div>
		<div class="zonggm"><iframe :src="projectmodel" frameborder="0" style="width:100%;height:100%;" onload="this.focus()"></iframe></div>
		<div class="lefttopjzm">
			<div class="leftjzm">
				<img class="logojzm" src="../../assets/image/jinghekeji.png" />
				<Xunilogo v-show="xianyinxuni"></Xunilogo>
				<Releases v-show="release"></Releases>
				<Gedit v-show="gedits"></Gedit>
			</div>
		</div>
		<div class="box">
			<!-- 除去侧边栏的剩余部分-->
			<!-- 右侧top部分 -->
			<div class="hometopgm" v-show="hometop">
				<!-- 	下拉菜单---项目 -->
				<el-dropdown style="float: left; margin-left:1.1rem;">
					<div class="el-dropdown-link" @click="fngxmxxm()">
						<span :class="{ xmimggm: istruexmgm}" style="vertical-align:text-bottom;"></span>
					<!-- 	<img class="xmimggm" src="../../assets/image/bluefz.png" /> -->
						<span class="xmgm">项目</span>
					<i style="display:inline-block;width:0.45rem;height:0.53125rem‬;margin-left:0.2rem;">
						<img src="../../assets/image/shang.png" alt="" style="width: 100%;height: 100%;" />
					</i>
					</div>
					<Newjian v-show="xianyin"></Newjian>
				</el-dropdown>
				<!-- 下拉菜单---项目--结束
				下拉菜单---社区 -->
				<el-dropdown style="float: left; margin-left:1.5rem;">
					<!-- 	@mouseleave="fnhsqlev()" -->
					<div class="el-dropdown-link sqssgm" @click="fngxmxsq()">
						<span :class="{ sqimggm: istruesqgm, sqimggmf: isfalsesqgm }" style="vertical-align:text-bottom;"></span>
						<!-- <img class="sqimggm" :src="hsq"/> -->
						<i class="sqgm">社区</i>
					</div>
				</el-dropdown>
				<el-dropdown style="float: left; margin-left:1.5rem;">
					<!-- 	@mouseleave="fnhbjlev()" -->
					<div class="el-dropdown-link bjssgm" @click="ceyins()">
						<span :class="{ bjimggms: istruebjgm, bjimggmsf: isfalsebjgm }" style="vertical-align:text-bottom;"></span>
						<!-- <img class="bjimggm" :src="bjtu" /> -->
						<i class="bjgm" :style="bjcolor">编辑</i>
						<i style="display:inline-block;width:0.45rem;height:0.25rem;line-height:height:0.53125rem‬;margin-left:0.2rem;">
							<img :src="nmbj" alt="" style="width: 100%;height: 100%;" />
						</i>
					</div>
				</el-dropdown>
			<el-dropdown style="float: left; margin-left:1.5rem;">
				<!-- @mouseleave="fnhfblev()" -->
				<div class="el-dropdown-link fbss" @click="fnfabug()">
					<span :class="{ fbimg: istrue, fbimgf: isfalse }" style="vertical-align:text-bottom;"></span>
					<!-- <img class="bjimg" :src="fbtu" /> -->
					<i class="bjsg bjf" :style="fbcolor">发布</i>
					<i style="display:inline-block;width:0.45rem;height:0.53125rem‬;margin-left:0.2rem;">
						<img :src="nmfb" alt="" style="width: 100%;height: 100%;" />
					</i>
				</div>
			</el-dropdown>
				<!-- 	下拉菜单---社区--结束
				下拉菜单---更多 -->
				<!-- 	@mouseleave="fnmorlevgxmx()" -->
				<div class="moretopcomgxmx" style="height:0.93125rem;" @mouseenter="fnmorgxmx()" @mouseleave="fnmorlevgxmx()">
				<!-- 	<img :src="moretb" alt="" style="width:0.84375rem;height:0.8125rem;margin-right:0.16rem;float:left;" /> -->
				<span :class="{ gdimgm: istruegdm, gdimgfm: isfalsegdm }" style="vertical-align:text-bottom;"></span>
				<i class="hgmorecomgxmx" :style="gdcolor">更多</i>
					<i style="display:inline-block;width:0.45rem;height:0.53125rem‬;margin-left:0.2rem;">
						<img :src="nmgd" alt="" style="width: 100%;height: 100%;" />
					</i>
					<div class="moocomgxmx" style="margin-top:0.1rem;">
						<div class="mores1comgxmx"><a href="http://www.jh-bim.com/home/solution" target="_blank" style="display:inline-block;color:#666666;width:4.5rem;">帮助</a></div>
						<div class="mores1comgxmx" @click="fnabout">联系我们</div>
						<div class="moresbcomgxmx">版本号: v 1.0.3</div>
					</div>
				</div>
				<!-- 下拉菜单---更多--结束 -->
			</div>
			<!-- 新建项目/管线综合/图纸 -->
			<div style="width:18.75rem;height:0.6875rem;position:absolute;top:3.93125rem;left:8.21875rem;text-align:left;cursor:pointer;">
				<span style="margin-right:0.1875rem;color:#2180ED;font-size:0.5rem;font-weight:500;cursor:pointer;float:left;line-height:0.6875rem;" 
				@click="fnjzmx()">
					{{projecttitss}}
				</span>
				<i style="font-weight:900;font-style:normal;font-size:0.625rem;cursor:pointer;float:left;line-height:0.6875rem;">/</i>
				<span
					style="margin-right:0.1875rem;margin-left:0.15625rem;color:#2180ED;font-size:0.5rem;font-weight:500;cursor:pointer;float:left;line-height:0.7575rem;"
					@click="fnjzmx()"
				>
					管线综合
				</span>
				<i style="font-weight:900;font-style:normal;font-size:0.625rem;cursor:pointer;float:left;line-height:0.6875rem;">/</i>
				<span style="color:#2180ED;font-size:0.5rem;font-weight:500;cursor:pointer;margin-left:0.15625rem;float:left;line-height:0.7575rem;">模型</span>
			</div>
			<!-- 中间图纸总体 -->
			<div class="gxmxdraw" v-show="fileshow">
				<!-- 中间图纸的图片 -->
				<div class="gxmxdrawtop"><img src="../../assets/image/mdraw.png" alt="" /></div>
				<!-- 中间图纸的文字 -->
				<div class="gxmxdrawinghz">这里还没有管线模型,需要上传哦</div>
				<!-- 上传按钮-->
				<div class="gxmxdrawingbtn">
					<div>
						<uploader :file-status-text="statusText" :options="options" @file-complete="onFileSuccess">
							<!-- <uploader-unsupport></uploader-unsupport> -->
							<uploader-drop class="gxmxdrawdrop"><uploader-btn :directory="false" :single="true" class="gxmxdrawdbtn" :attrs="attrs">上传管线模型</uploader-btn></uploader-drop>
							<uploader-list></uploader-list>
						</uploader>
					</div>
				</div>
			</div>
		</div>
		<!-- 点击联系我们的遮罩 -->
		<div
			style="width:59.9375rem;height:33.65625rem;position: fixed;top: 0;left: 0;right: 0;bottom: 0;background: rgba(0, 0, 0, 0.2);z-index:500000;"
			v-show="abouts"
			@click="fnaboutmark"
		></div>
	</div>
</template>
<script>
import Swiper from 'swiper';
import 'swiper/dist/css/swiper.min.css';
import api from '@/api/api.js';
import qs from 'qs';
import Newjian from './newjian';
import Xunilogo from './xunilogo';
import axios from 'axios';
import Releases from './releases';
import Gedit from './gedit';
import addressurls from '@/api/ip.js';
// import Zheader from './header';
export default {
	data() {
		return {
			//显示上传的功能按钮
			fileshow: true,
			title: '18306846355',
			model: '',
			projectmodel: '',
			panduan: false,
			xianyin: false,
			xianyinxuni: false,
			hometop: true,
			// fileshow: true,
			options: {
				target: api.Uploadpipes, //SpringBoot后台接收文件夹数据的接口
				testChunks: false, //是否分片-不分片
				chunkSize: '2048000000'
			},
			statusText: {
				success: '成功了',
				error: '出错了',
				uploading: '上传中',
				paused: '暂停中',
				waiting: '等待中'
			},
			bjtu: require('../../assets/image/bianji.png'),
			bjcolor: 'color:#333333',
			fbtu: require('../../assets/image/fbnav.png'),
			fbcolor: 'color:#333333',
			gdcolor:'color:#333333',
			//发布
			release: false,
			//编辑
			gedits:false,
			//总的等陆头部
			zheaderxy: true,
			// 更多中的下拉
			lmore: require('../../assets/image/pmjtxia.png'),
			//编辑下拉
			nmbj: require('../../assets/image/pmjtxia.png'),
			// 发布下拉
			nmfb: require('../../assets/image/pmjtxia.png'),
			// 更多下拉
			nmgd: require('../../assets/image/pmjtxia.png'),
			// 联系我们
			abouts: false,
			//上传文件的类型限制
			attrs: {
				accept: '.zip, .jar, .war, .rar, .7z'
			},
			// newarrs:[0,0,0,0,0,0,0,0],
			// 社区默认状态
			hsq: require('../../assets/image/sq@2x.png'),
			// hsqcolor:"color:#333333",
			moretb: require('../../assets/image/more@2x.png'),
			// 社区
			istruesqgm: true,
			isfalsesqgm: false,
			// 编辑
			istruebjgm: true,
			isfalsebjgm: false,
			// 发布
			istrue: true,
			isfalse: false,
			// 建筑项目的标题
			projecttitss:'',
			istruexmgm:true,
			istruegdm:true,
			isfalsegdm:false
		};
	},
	components: {
		Newjian,
		Xunilogo,
		Releases,
		Gedit
		// Zheader
	},
	created() {
		// 编辑与发布隐藏事件
		this.$eventbus.$on('ceyinfbs', () => {
			 this.gedits = false;
			 this.release = false;
			 this.xianyinxuni = true
			 this.istruebjgm = true;
			 this.isfalsebjgm = false;
			 this.istruefbgm = true;
			 this.isfalsefbgm = false
			 // this.xianyinxuni = true
			});
		// this.$eventbus.$on('ceyinfb', ite => {
		// 	if (ite == 'fabu') {
		// 		this.release = true;
		// 		this.xianyinxuni = false;
		// 	}
		// 	if (ite == 'xjxm') {
		// 		this.release = false;
		// 		this.xianyinxuni = true;
		// 	}
		// 	if (ite == 'jzjg') {
		// 		this.release = false;
		// 		this.xianyinxuni = true;
		// 	}
		// });
   // 取出tit
	  this.projecttitss = sessionStorage.getItem('projecttit');
		var pipemodelid = sessionStorage.getItem('projectid');
		if (pipemodelid != '' && pipemodelid != null && pipemodelid != undefined) {
			axios.get(api.ShowModel + '/2' + '/' + pipemodelid).then(result => {
				if (
					result.data.modelId != null ||
					(result.data.projectId != null && result.data.url != '') ||
					(result.data.projectId != '' && result.data.url != undefined) ||
					result.data.projectId != undefined
				) {
					this.fileshow = false;
				}
				if (result.data.url != null && result.data.url != '' && result.data.url != undefined) {
					this.fileshow = false;
					this.model = result.data.url;
					this.projectmodel = addressurls.url + this.model;
				}
			});
		}

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
		//管线模型
	},
	mounted() {
		this.$eventbus.$emit('cezhan2', 'moxin');
		this.$eventbus.$emit('hometop')
	},
	methods: {
		// 点击新建项目
		fnjzmx() {
			// this.$eventbus.$emit('cezhan', 'moxin');
			// this.$eventbus.$emit('ceyindj', 'xinjianmoxin');
			// this.$eventbus.$emit('ceyinfb', 'xjxm');
			this.$eventbus.$emit('ceyinfbs');
			this.fbtu = require('../../assets/image/fbnav.png');
			this.bjtu = require('../../assets/image/bianji.png');
			this.bjcolor = 'color:#333333';
			this.fbcolor = 'color:#333333';
		},
		// 点击管线综合
		fnjzmxg() {
			// this.$router.push('/newjzmodel');
			// this.$eventbus.$emit('ceyindj', 'jianzhumoxin');
			// this.$eventbus.$emit('ceyinfb', 'jzjg');
			this.$eventbus.$emit('ceyinfbs');
			this.fbtu = require('../../assets/image/fbnav.png');
			this.bjtu = require('../../assets/image/bianji.png');
			this.bjcolor = 'color:#333333';
			this.fbcolor = 'color:#333333';
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
		fns() {
			this.xianyin = !this.xianyin;
			// this.xianyinxuni = false;
			this.$eventbus.$emit('showyin');
		},
		//上传管道模型保存到数据库
		onFileSuccess: function() {
			axios.post(api.ShowPipe).then(result => {});
			this.fileshow = false;
		},
		fn4() {
			this.loginWindow = 'display:block';
		},
		look() {
			this.$router.push('/onepengzhuang');
		},
		// 点击项目，跳转到login页
		fngxmxxm() {
			this.$router.push('/Login');
		},
		// 点击社区，跳转到社区页
		fngxmxsq() {
			this.$router.push('/');
		},
		// 点击编辑
		ceyins() {
			this.$eventbus.$emit('ceyin');
			this.$eventbus.$emit('ceyinxxs');
			this.istruebjgm = false;
			this.isfalsebjgm = true;
			this.istrue = true;
			this.isfalse = false;
			this.bjcolor = 'color:#2180ED';
			this.release = false;
			this.xianyinxuni = false;
			this.gedits = true;
			this.fbcolor = 'color:#333333';
			this.lmore = require('../../assets/image/pmjtxia.png');
			this.nmbj = require('../../assets/image/shang.png');
			this.nmfb = require('../../assets/image/pmjtxia.png');
		},
		//点击发布
		fnfabug() {
			this.fbcolor = 'color:#2180ED';
			this.istrue = false;
			this.isfalse = true;
			this.istruebjgm = true;
			this.isfalsebjgm = false;
			this.release = true,
			this.xianyinxuni = false,
			this.gedits = false;
			this.bjcolor = 'color:#333333';
			this.nmfb = require('../../assets/image/shang.png');
			this.nmbj = require('../../assets/image/pmjtxia.png');
			this.lmore = require('../../assets/image/pmjtxia.png');
		},
		// 划过更多
		fnmorgxmx() {
			this.moretb = require('../../assets/image/moress.png');
			this.gdcolor = 'color:#2180ED';
			this.nmgd = require('../../assets/image/shang.png');
			this.isfalsegdm = true;
			this.istruegdm = false
		},
		// 移出更多
		fnmorlevgxmx() {
			this.moretb = require('../../assets/image/more@2x.png');
			this.gdcolor = 'color:#333333';
			this.nmgd = require('../../assets/image/pmjtxia.png');
			this.isfalsegdm = false;
			this.istruegdm = true
		}
	}
};
</script>

<style>
/* 划过社区 */
.sqssgm:hover .sqgm {
	color: #2180ed !important;
}
.sqssgm:hover .sqimggm {
	background: url(../../assets/image/shequ.png) no-repeat;
	background-size: 0.84375rem 0.8125rem;
}
/* 划过编辑 */
.bjssgm:hover .bjgm {
	color: #2180ed !important;
}
.bjssgm:hover .bjimggms {
	background: url(../../assets/image/bjblue.png) no-repeat;
	background-size: 0.84375rem 0.8125rem;
}
/* 划过发布 */
.fbss:hover .bjf {
	color: #2180ed !important;
}
.fbss:hover .fbimg {
	color: #2180ed !important;
	background: url(../../assets/image/fbblue.png) no-repeat;
	background-size: 0.84375rem 0.8125rem;
}
/* 更多 */
.moretopcomgxmx {
	position: relative;
	float: left;
	margin-left: -1.4rem;
	font-size: 0.625rem;
	font-family: MicrosoftYaHei;
	font-weight: 400;
	/* color:#2180ED; */
	font-style: normal;
	line-height: 0.93125rem;
	/* background-color:red; */
	margin-top: 0.38rem;
	margin-left: 1.62rem;
	text-align: left;
	cursor: pointer;
}
.hgmorecomgxmx {
	color: #333333;
	width: 1.25rem;
	height: 0.5625rem;
	font-size: 0.625rem;
	font-family: MicrosoftYaHei;
	font-weight: 400;
	padding-left: 0.1875rem;
	font-style: normal;
}
.moocomgxmx {
	width: 4.75rem;
	/* width: 183px;
		height: 195px; */
	/* background: url(../../assets/image/mores.png); */
	background: rgba(225, 225, 225, 0.2);
	padding-left: 0.2rem;
	padding-right: 0.25rem;
	cursor: pointer;
	display: none;
}
.mores1comgxmx {
	width: 4.65rem;
	height: 0.9rem;
	border-bottom: 1px solid #999999;
	text-align: left;
	line-height: 1rem;
	color: #666666;
	font-size: 0.46rem;
	font-weight: 500;
	/* 	background:red; */
}
.moresbcomgxmx {
	border: 0;
	text-align: left;
	line-height: 0.9rem;
	color: #666666;
	font-size: 0.46rem;
	font-weight: 500;
	/* background:red; */
}
.moretopcomgxmx:hover .moocomgxmx {
	display: block;
}
/* .moretopcomgxmx:hover .hgmorecomgxmx {
	color: #2180ed;
}
.moretopcomgxmx:hover .shouye {
	transform: rotate(180deg);
} */
.gxmodelmore {
	background: rgba(225, 225, 225, 0.3);
	position: absolute;
	top: 2.125rem !important;
	left: 25.975rem !important;
	border: none;
	padding: 0.1rem;
	border-radius: 0rem !important;
}
.popper__arrow {
	border-width: 0rem !important;
	left: 0 !important;
	overflow: hidden;
}
.moogx {
	width: 4.75rem;
	/* 		height: 195px; */
	/* 	background: url(../../assets/image/mores.png); */
	padding-left: 0.2rem;
	padding-right: 0.25rem;
	cursor: pointer;
}
.mores1gx {
	width: 4.65rem;
	height: 0.9rem;
	border-bottom: 1px solid rgba(0, 0, 0, 0.2);
	text-align: left;
	line-height: 0.9rem;
	color: #666666;
	font-size: 0.46rem;
	font-weight: 500;
	/* 	background:red; */
}
.moresbgx {
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
body {
	/* width: 1920px; */
	margin: 0 !important;
	/* height:1080px; */
	width: 100%;
	height: 100%;
}
html {
	/* 	width: 1920px;
	height:1080px; */
	width: 100%;
	height: 100%;
}

.zonggm {
	width: 59.9375rem;
	height: 33.65625rem;
	/* background:green; */
	/* background: url(../../assets/image/bjt.jpg);
	background-repeat: no-repeat;
	background-size:100% 100%; */
	position: relative;
}
.el-main {
	/* padding-left:50px; */
	/* padding-top:29px; */
	padding: 0 !important;
}
/* 主页top部分*/
.hometopgm {
	/* width:46.875rem;
	height:1.78125rem; */
	position: absolute;
	top: 0.6275rem;
	left: 7.2rem;
	/* background:red; */
	line-height: 1.78125rem;
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
	width: 6.75rem;
	height: 1.875rem;
	/* 	background-color:green;
			background: url(../../assets/image/homecebian8@2x.png); */
	position: absolute;
	top: 0px;
}
.el-dropdown-link {
	cursor: pointer;
	color: #333333;
}
.xmimggm {
	display: inline-block;
	width: 0.84375rem;
	height: 0.8125rem;
	background: url(../../assets/image/bluefz.png) no-repeat;
	background-size: 0.84375rem 0.8125rem;
}
.xmgm {
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
/* 社区初始的图片 */
.sqimggm {
	width: 0.84375rem;
	height: 0.8125rem;
	display: inline-block;
	background: url(../../assets/image/sq@2x.png) no-repeat;
	background-size: 0.84375rem 0.8125rem;
}
.sqimggmf {
	width: 0.84375rem;
	height: 0.8125rem;
	display: inline-block;
	background: url(../../assets/image/shequ.png) no-repeat;
	background-size: 0.84375rem 0.8125rem;
}
/* 编辑初始图片 */
.bjimggms {
	width: 0.84375rem;
	height: 0.8125rem;
	display: inline-block;
	background: url(../../assets/image/bianji.png) no-repeat;
	background-size: 0.84375rem 0.8125rem;
}
.bjimggmsf {
	display: inline-block;
	width: 0.84375rem;
	height: 0.8125rem;
	background: url(../../assets/image/bjblue.png) no-repeat;
	background-size: 0.84375rem 0.8125rem;
}
.bjsg {
	width: 1.25rem;
	height: 0.5625rem;
	font-size: 0.625rem;
	font-family: MicrosoftYaHei;
	font-weight: 400;
	padding-left: 0.1875rem;
	font-style: normal;
}
.fbimg {
	display: inline-block;
	width: 0.84375rem;
	height: 0.8125rem;
	background: url(../../assets/image/fbnav.png) no-repeat;
	background-size: 0.84375rem 0.8125rem;
}
.fbimgf {
	display: inline-block;
	width: 0.84375rem;
	height: 0.8125rem;
	background: url(../../assets/image/fbblue.png) no-repeat;
	background-size: 0.84375rem 0.8125rem;
}
.gdimgm{
	display: inline-block;
	width: 0.84375rem;
	height: 0.7725rem;
	background: url(../../assets/image/more@2x.png) no-repeat;
	background-size: 0.84375rem 0.8125rem;
}
.gdimgfm{
	display: inline-block;
	width: 0.84375rem;
	height: 0.7725rem;
	background: url(../../assets/image/moress.png) no-repeat;
	background-size: 0.84375rem 0.8125rem;
}
.sqgm {
	width: 1.25rem;
	height: 0.5625rem;
	font-size: 0.625rem;
	font-family: MicrosoftYaHei;
	font-weight: 400;
	padding-left: 0.1875rem;
	font-style: normal;
}
.bjgm {
	width: 1.25rem;
	height: 0.5625rem;
	font-size: 0.625rem;
	font-family: MicrosoftYaHei;
	font-weight: 400;
	padding-left: 0.1875rem;
	font-style: normal;
}
.fbgm {
	display: inline-block;
	width: 0.84375rem;
	height: 0.8125rem;
	background: url(../../assets/image/fbnav.png) no-repeat;
	background-size: 0.84375rem 0.8125rem;
}
.moreimggm {
	width: 0.78125rem‬;
	height: 0.78125rem;
}
.moregm {
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
/* 中间图纸部分 */
.gxmxdraw {
	width: 15.625rem;
	height: 15.625rem;
	/* background:red; */
	position: absolute;
	left: 25rem;
	top: 9rem;
}
.gxmxdrawtop {
	width: 12.84375rem;
	height: 8.59375rem;
	/* 	background:plum; */
	margin-left: 1.4rem;
}
.gxmxdrawtop img {
	width: 100%;
	height: 100%;
}
.gxmxdrawinghz {
	width: 15.625rem;
	height: 3rem;
	/* background:blue; */
	font-size: 0.9375rem;
	font-family: PingFang SC;
	font-weight: 500;
	color: rgba(51, 51, 51, 1);
	line-height: 3.8rem;
}
.gxmxdrawingbtn {
	width: 15.625rem;
	height: 3.9rem;
	/* background:plum; */
}
.gxmxdrawdrop {
	/* padding:0.3125rem; */
	border: 0 !important;
	background-color: #ffffff !important;
	width: 4.76875rem !important;
	height: 1.375rem !important;
	margin-top: 1.06875rem;
	border-radius: 0 !important;
	/* line-height:1.25rem; */
	/* font-size:0.3875rem; */
	font-family: PingFang SC;
	font-weight: 500;
	color: rgba(255, 255, 255, 1);
	background: url(../../assets/image/pmd.png) no-repeat;
	background-size: 100% 75%;
	display: flex;
	justify-content: center;
	margin-left: 5.3rem;
}
.gxmxdrawdbtn {
	/* padding:0.125rem 0.25rem !important; */
	line-height: 0.8rem !important;
	border-radius: 0 !important;
	font-size: 0.6125rem !important;
	width: 4.76875rem !important;
	height: 0.775rem !important;
	border: none !important;
	color: #ffffff !important;
}
</style>
