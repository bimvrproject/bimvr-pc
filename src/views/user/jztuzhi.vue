<template>
	<div>
		<div class="zongjt" @click="cetuend" style="overflow:hidden;">
			<!-- 	<iframe src="https://www.baidu.com/s?tn=news&rtt=1&bsst=1&wd=%E9%A6%99%E6%B8%AF&cl=2&origin=ps" frameborder="0" style="width:100%;height:100%;"></iframe> -->
		</div>
		<div class="lefttopjzm">
			<div class="leftjzm">
				<img class="logojzm" src="../../assets/image/jinghekeji.png" />
				<Xunilogo v-show="xianyinxuni"></Xunilogo>
			</div>
		</div>
		<div style="width:47.8125rem;height:28.4375rem;line-height:28.4375rem;position:absolute;top:5rem;left:6.875rem;"
		 v-if="pmph">
		 <img :src="pmdrawpicture" style="width:100%;height:100%;" alt="">
		 </div>
		<div>
			<!--nav -->
			<div class="hometopjzmjztz" v-show="hometop">
				<!-- 下拉菜单---项目 -->
				<el-dropdown style="float: left;margin-left:-1.4rem;">
					<div class="el-dropdown-link" @click="fnjztz">
						<img class="xmimgjztz" src="../../assets/image/bluefz.png" alt="" style="vertical-align:text-bottom;"/>
						 <span class="xmjztz">项目</span>
						<i style="display:inline-block;width:0.45rem;height:0.53125rem‬;margin-left:0.2rem;">
							<img src="../../assets/image/shang.png" alt="" style="width: 100%;height: 100%;" />
						</i>
					</div>
					<Newjian v-show="xianyin"></Newjian>
				</el-dropdown>
				<!-- 下拉菜单---项目--结束 -->
				<!-- 下拉菜单---社区 -->
				<el-dropdown style="float: left; margin-left:1.5rem;">
					<div class="el-dropdown-link" @click="fnjztzsq" @mouseenter="fnhsq()" @mouseleave="fnhsqlev()">
						<img class="sqimgjztz" :src="hsq" style="vertical-align:text-bottom;"/>
						<i class="sqjztz" :style="hsqcolor">社区</i>
						<!-- 	<i class="el-icon-arrow-down el-icon--right"></i> -->
					</div>
				</el-dropdown>
				<!-- 下拉菜单---社区--结束 -->
				<!-- 下拉菜单---更多 -->
				<div class="moretopcomjztz" style="height:0.93125rem;" @mouseenter="fnmorjztz()" @mouseleave="fnmorlevjztz()">
					<img  :src="moretb"  alt="" style="width:0.84375rem;height:0.8125rem;margin-right:0.16rem;float:left;vertical-align:text-bottom;">
					   <span class="hgmorecomjztz">更多</span>
						 <i style="display:inline-block;width:0.45rem;height:0.53125rem‬;margin-left:0.2rem;">
						   <img :src="nmgd" alt="" style="width: 100%;height: 100%;" />
					   </i>
						  <div class="moocomjztz" style="margin-top:0.1rem;">
						 	<div class="mores1comjztz">
						 		<a href="http://www.jh-bim.com/home/solution" target="_blank" style="display:inline-block;color:#666666;width:4.5rem;">帮助</a>
						 	</div>
						 	<div class="mores1comjztz" @click="fnabout">联系我们</div>
						 	<div class="moresbcomjztz">版本号: v 1.0.3</div>
						 </div>
				</div>
				<!-- 下拉菜单---更多--结束 -->
			</div>
			<!-- 新建项目/管线综合/图纸 -->
				<div style="width:18.75rem;height:0.6875rem;position:absolute;top:3.93125rem;left:8.21875rem;text-align:left;cursor:pointer;">
				<span style="margin-right:0.1875rem;color:#2180ED;font-size:0.5rem;font-weight:500;float:left;line-height:0.6875rem;">
					{{projecttitjtz}}
				</span>
				<i style="font-weight:900;font-style:normal;font-size:0.625rem;float:left;line-height:0.6875rem;">/</i>
				<span style="margin-right:0.1875rem;margin-left:0.15625rem;color:#2180ED;font-size:0.5rem;font-weight:500;float:left;line-height:0.7575rem;">建筑结构</span>
				<i style="font-weight:900;font-style:normal;font-size:0.625rem;float:left;line-height:0.6875rem;">/</i>
				<span style="color:#2180ED;font-size:0.5rem;font-weight:500;margin-left:0.15625rem;float:left;line-height:0.7575rem;">图纸</span>
			</div>
			<!-- 右侧图纸 -->
			<div class="youtu" @click="cetubut" v-if="cetubuts"><img src="../../assets/image/tpzuohua.png" alt="" /></div>
			<!-- 右侧展开图 -->
			<div class="youbigtu" v-if="cetuxy">
				<div class="pmzong">
					<div class="pmtop">
						<div class="pmtopn">
							<!-- 平面图纸 -->
							<div @click="pmtz" style="display:flex;">
								<img :src="pmt" alt="" class="pmt" />
								<span class="pmz">平面图纸</span>
								<img :src="pmjt" alt="" class="pmjt" />
							</div>
						</div>
					</div>
					<!-- 平面图纸展开 -->
					<div class="pmzk" v-if="pmxy">
						<!-- 新建项目 -->
						<ul>
							<!-- projectidsdrawingarr -->
							<li v-for="(item, index) in drawingarrpm" :key="index" class="pmnew" style="position:relative;cursor: pointer;"
							 @click="drawdanji(index)">
								<img src="../../assets/image/zk.png" class="pmt5" alt="" />
								<div>
									<p class="pmtz5"  v-show="!item.changes" @dblclick="xgtz(index)" :title="item.drawName">{{ item.drawName}}</p>
								</div>
								<input type="text" v-show="item.changes" v-model="item.drawName"
								 style="position:absolute;left:1.4rem;top:0.2rem;width:3.3125rem;
								 height:0.875rem;"  @blur="changepm(index)" />
							</li>
						</ul>
						<div class="pm6">
							<div>
								<uploader :file-status-text="statusText" :options="options" @file-complete="onFileSuccess">
									<!-- <uploader-unsupport></uploader-unsupport> -->
									<uploader-drop class="uplm">
										<uploader-btn :directory="false" :single="true" class="upbtn" :attrs="attrs"><span class="pltop"></span></uploader-btn>
									</uploader-drop>
									<!-- <uploader-list></uploader-list> -->
								</uploader>
							</div>
						</div>
					</div>
				</div>
				<!-- 立面图纸 -->
				<div class="pmzong">
					<div class="pmtop">
						<div class="pmtopn">
							<!-- 	立面图纸 -->
							<div class="pmtopnr" @click="lmtz" style="display:flex;">
								<img :src="lmt" alt="" class="pmt" />
								<span class="pmz">立面图纸</span>
								<img :src="lmjt" alt="" class="pmjt" />
							</div>
						</div>
					</div>
					<!-- 立面图纸展开 -->
					<div class="pmzk" v-if="lmxy">
						<!-- 新建项目 -->
						<ul>
							<li v-for="(item, index) in drawingarrlm" :key="index"  class="pmnew" style="position:relative;cursor: pointer;"  @click="drawdanjilimian(index)">
								<img src="../../assets/image/zk.png" class="pmt5" alt="" />
								<div>
									<p class="pmtz5" v-show="!item.changelm" @dblclick="xglmtz(index)" :title="item.drawName">{{item.drawName}}</p>
								</div>
								<input v-model="item.drawName" v-show="item.changelm" type="text" @blur="changelm(index)"
								 style="position:absolute;left:1.4rem;top:0.2rem;width:3.3125rem;
								 height:0.875rem;"/>
							</li>
						</ul>
							<div class="pm6">
								<div>
									 <!-- @file-complete="onFileSuccess" -->
									<uploader :file-status-text="statusText" :options="options">
										<!-- <uploader-unsupport></uploader-unsupport> -->
										<uploader-drop class="uplm">
											<uploader-btn :directory="false" :single="true" class="upbtn" :attrs="attrs"><span class="pltop"></span></uploader-btn>
										</uploader-drop>
										<!-- <uploader-list></uploader-list> -->
									</uploader>
								</div>
							</div>
					</div>
				</div>
			</div>
			<!-- 图纸-->
			<div class="drawing" v-show="centerdra">
				<!-- 图纸中部图片 -->
				<div class="drawingtop">
					<img src="../../assets/image/draw.png" alt="">
				</div>
				<!-- 图纸中的汉字 -->
				<div class="drawinghz">
					这里还没有图纸,需要上传哦
				</div>
				<!-- 平面图纸和立面图纸的按钮 -->
				<div class="drawingbut">
					<!-- 平面 -->
					<div class="drawpm">
						<div>
							<div>
								<uploader :file-status-text="statusText" :options="options" @file-complete="onFileSuccess">
									<!-- <uploader-unsupport></uploader-unsupport> -->
									<uploader-drop class="drawdrop">
										<uploader-btn :directory="false" :single="true" class="drawbtn" :attrs="attrs">上传平面图纸</uploader-btn>
									</uploader-drop>
									<uploader-list class="pingmiancss"></uploader-list>
								</uploader>
							</div>
						</div>
					</div>
					<!-- 立面 -->
					<div class="drawlm">
						<div>
							<div>
								<!--  @file-complete="onFileSuccess" -->
								<uploader :file-status-text="statusText" :options="options" @file-complete="onFileSuccess">
									<!-- <uploader-unsupport></uploader-unsupport> -->
									<uploader-drop class="drawdrop">
										<uploader-btn :directory="false" :single="true" class="drawbtn" :attrs="attrs">上传立面图纸</uploader-btn>
									</uploader-drop>
									<uploader-list class="limiancss"></uploader-list>
								</uploader>
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
		<!-- 点击联系我们的遮罩 -->
		<div style="width:59.9375rem;height:33.65625rem;position: fixed;top: 0;left: 0;right: 0;bottom: 0;background: rgba(0, 0, 0, 0.2);" v-show="abouts" @click="fnaboutmark"></div>
	</div>
</template>
<script>
	import api from '@/api/api.js';
	import axios from 'axios';
	import Newjian from './newjian';
	import Xunilogo from './xunilogo';
	import addressurls from '@/api/ip.js';
	// import Zheader from './header';
	export default {
		data() {
			return {
				// 中间显示图纸部分
				pmph:false,
				// 中间初始样式
				centerdra:true,
				pmdrawpicture: '',
				panduan: false,
				xianyin: false,
				xianyinxuni: false,
				hometop: true,
				cetuxy: false,
				cetubuts: true,
				pmxy: false,
				lmxy: false,
				pmt: require('../../assets/image/pmtz.png'),
				lmt: require('../../assets/image/pmtz.png'),
				pmjt: require('../../assets/image/pmjtxia.png'),
				lmjt: require('../../assets/image/pmjtxia.png'),
				lmore: require('../../assets/image/pmjtxia.png'),
				// 更多下拉
				nmgd: require('../../assets/image/pmjtxia.png'),
				// 联系我们
				abouts: false,
				drawingarrpm: [],		//接收平面图纸
				drawingarrlm: [],		//接收立面图纸
				projectidsdrawingarr: [],
				title: '12312313122',
				statusText: {
					success: '成功了',
					error: '出错了',
					uploading: '上传中',
					paused: '暂停中',
					waiting: '等待中'
				},
				options: {
					target: api.UploadPicture, //SpringBoot后台接收文件夹数据的接口
					testChunks: false, //是否分片-不分片
					chunkSize: '2048000000000'
				},
				//总的等陆头部
				// zheaderxy: true,
				//上传限制
				attrs: {
					accept: '.dwg'
				},
				fontdrawingarrpm:true,//平面图纸字体
				inputdrawingarrpm:false, //平面图纸input框
				inputdrawingar:"",//平面图纸input框字体
				// 社区默认状态
				hsq:require('../../assets/image/sq@2x.png'),
				hsqcolor:"color:#333333",
				moretb: require('../../assets/image/more@2x.png'),
				// 新建项目中获取到title
				projecttitjtz:''
			};
		},
		components: {
			Newjian,
			Xunilogo,
			// Zheader
		},
		created() {
			//右侧平面
			this.drawingarrpm = localStorage.getItem('pmxg')
			? JSON.parse(localStorage.getItem('pmxg'))
			: [{msg:'',changes:false}];
			// 获取存储的值
			localStorage.getItem('pmxg');
			// 右侧立面
			this.drawingarrlm = localStorage.getItem('lmxg')
			? JSON.parse(localStorage.getItem('lmxg'))
			: [{msglm:'',changelm:false}];
			// 获取存储的值
			localStorage.getItem('lmxg');
			// 接收一下title
			this.projecttitjtz = sessionStorage.getItem('projecttit');
			var prid = sessionStorage.getItem("projectid");
			if(prid!=null && prid!=undefined){
				//该项目中是否有图纸 如果有则不显示上传图纸功能
				axios.get(api.getprojectids + "/1"+'/' + prid).then(result => {
					this.pmph=true;
					this.projectidsdrawingarr = result.data;
					// console.log(this.projectidsdrawingarr)
					this.pmdrawpicture=addressurls.url+result.data[0].url
					if (this.projectidsdrawingarr.length != 0) {
						this.centerdra = false;
					}
				});
				//绑定平面图纸
				axios.get(api.Pcreddrawing + '/1' + '/' + prid + "/1").then(result => {
					this.drawingarrpm = result.data;
				});
				//绑定立面图纸
				axios.get(api.Pcreddrawing + '/1' + '/' + prid + "/2").then(result => {
					this.drawingarrlm = result.data;
				});
			}
			
			// console.log(localStorage.getItem('xnjztz'));
			// console.log(localStorage.getItem('wallss1s'))
			// this.arr = localStorage.getItem('wallss1s') ? JSON.parse(localStorage.getItem('wallss1s')) : [{msg:平面,change:false},{msg:50,change:false},{id:2,msg:50,change:false},{msg:50,change:false}],
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
			this.$eventbus.$emit('cezhan', 'tuzhi');
			this.$eventbus.$emit('hometop');
		},
		methods: {
			//上传成功事件
			onFileSuccess(){
				this.centerdra = false;
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
			fnmorjztz(){
				this.moretb = require('../../assets/image/moress.png');
				this.nmgd = require('../../assets/image/shang.png');
			},
			// 移出更多
			 fnmorlevjztz(){
				this.moretb = require('../../assets/image/more@2x.png');
				this.nmgd = require('../../assets/image/pmjtxia.png');
			},
			// 移出社区
			fnleave() {
				this.lmore = require('../../assets/image/pmjtxia.png');
			},
			// 右侧平面图纸双击事件
			xgtz(index){
				this.$set(this.drawingarrpm[index],'changes',true);
			},
			// 右侧平面图纸失焦事件
			changepm(index){
				this.$set(this.drawingarrpm[index],'changes',false);
				// 设置localStroage
			localStorage.setItem('pmxg',JSON.stringify(this.drawingarrpm));
			console.log(localStorage.getItem('pmxg'))
			},
			// 右侧立面图纸双击事件
			xglmtz(index){
				this.$set(this.drawingarrlm[index],'changelm',true);
			},
			// 右侧立面图纸失焦事件
			changelm(index){
				this.$set(this.drawingarrlm[index],'changelm',false);
				// 设置localStorage
				localStorage.setItem('lmxg',JSON.stringify(this.drawingarrlm));
				console.log(localStorage.getItem('lmxg'))
			},
			//点击平面图纸名称显示图纸
			drawdanji(index) {
				this.pmph=true;
				this.centerdra = false;
				var drawid = this.drawingarrpm[index].resPictureId;
				axios.get(api.SelectByPrimaryKey + '/' + drawid).then(result => {
					this.pmdrawpicture = addressurls.url + result.data.url;
				});
			},
			//点击立面图纸名称显示图纸
			drawdanjilimian(index){
				this.pmph=true;
				this.centerdra = false;
				var drawid = this.drawingarrlm[index].resPictureId;
				axios.get(api.SelectByPrimaryKey + '/' + drawid).then(result => {
					this.pmdrawpicture = addressurls.url + result.data.url;
				});
			},
			// 点击项目，跳转到login页
			fnjztz() {
				this.$router.push('/Login');
			},
			//点击社区，跳转到社区页
			fnjztzsq() {
				this.$router.push('/');
			},
			// xjlmfn() {
			// 	this.arr.push(6);
			// },
			// xjfn() {
			// 	this.drawingarr.push(6);
			// },

			changename() {
				// this.wang = wang,
				(this.showname = true), (this.showrename = false);
				//设置localStroage值
				sessionStorage.setItem('wang', this.wang);
			},
			cetuend() {
				this.cetuxy = false;
				this.cetubuts = true;
			},
			cetubut() {
				this.cetuxy = true;
				this.cetubuts = false;
			},
			pmtz() {
				(this.pmxy = true),
				(this.lmxy = false),
				(this.pmt = require('../../assets/image/zkwj.png')),
				(this.pmjt = require('../../assets/image/pmshang.png')),
				(this.lmt = require('../../assets/image/pmtz.png')),
				(this.lmjt = require('../../assets/image/pmjtxia.png'));
			},
			lmtz() {
				this.lmxy = true;
				this.pmxy = false;
				(this.lmt = require('../../assets/image/zkwj.png')),
				(this.lmjt = require('../../assets/image/pmshang.png')),
				(this.pmt = require('../../assets/image/pmtz.png')),
				(this.pmjt = require('../../assets/image/pmjtxia.png'));
			},
			help2() {
				location.href = 'http://www.jh-bim.com/home/solution';
			},
			Preservation2() {
				this.$router.push('/baocun');
			},
			xiugai3() {
				this.$router.push('/xiugai');
			},
			abouts4() {
				this.$router.push('/about');
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
	.moretopcomjztz{
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
	.hgmorecomjztz{
		color:#333333;
	}
	.moocomjztz{
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
	.mores1comjztz{
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
	.moresbcomjztz{
			border: 0;
			text-align: left;
			line-height:0.9rem;
			color: #666666;
			font-size:0.46rem;
			font-weight: 500;
			/* background:red; */
		}
		.moretopcomjztz:hover .moocomjztz{
			  display:block;
		}
		.moretopcomjztz:hover .hgmorecomjztz{
			 color:#2180ED
		}
		.moretopcomjztz:hover .shouye{
			 transform:rotate(180deg);
		}
	
	
	.pingmiancss{
		left: -1.25rem;
		width: 14.375rem;
	}
	.limiancss{
		left: -7.8rem;
		width: 14.375rem;
	}
	/* 更多 */
	.jztzmore {
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
	.jztzmoo {
		width: 4.75rem;
		/* 		height: 195px; */
		/* 	background: url(../../assets/image/mores.png); */
		padding-left: 0.1rem;
		padding-right: 0.25rem;
		cursor: pointer;
	}
	.jztzmores1 {
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
	.jztzmoresb {
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
	.zongjt {
		width: 60rem;
		height: 33.75rem;
		/* 	background:green; */
		/* 	background: url(../../assets/image/bjt.jpg); */
		/* background-repeat: no-repeat;
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
	.hometopjzmjztz {
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
		padding-right: 0px;
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

	.xmimgjztz {
		width: 0.84375rem;
		height: 0.8125rem;
		padding-left: 2.5rem;
		padding-top: 0.0625rem;
	}

	.xmjztz {
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

	.sqimgjztz,
	.bjimgjztz {
		width: 0.84375rem;
		height: 0.8125rem;
	}

	.sqjztz {
		width: 1.25rem;
		height: 0.5625rem;
		font-size: 0.625rem;
		font-family: MicrosoftYaHei;
		font-weight: 400;
		padding-left: 0.1875rem;
		font-style: normal;
	}

	.moreimgjztz {
		width: 0.78125rem‬;
		height: 0.78125rem;
	}

	.morejztz {
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

	/* 右侧图纸 */
	.youtu {
		width: 1.5625rem;
		height: 5.03125rem;
		position: absolute;
		top: 14.375rem;
		right: 0rem;
		cursor: pointer;
	}

	.youtu img {
		width: 100%;
		height: 100%;
	}

	/* 右侧大图 */
	.youbigtu {
		width: 5.03125rem;
		height: 31.3125rem;
		position: absolute;
		top: 1.21875rem;
		left: 54.96875rem;
		background: url(../../assets/image/touju.png) no-repeat;
		background-size: 5.03125rem 31.3125rem;
	}

	.pmtop {
		width: 5.03125rem;
		height: 1.40625rem;
		/* 	background:red; */
	}

	.pmtopn {
		width: 5.03125rem;
		height: 1.375rem;
		background: rgba(225, 226, 226, 0.3);
		border-bottom: 0.03125rem solid #666666;
		line-height: 1.375rem;
		cursor: pointer;
	}

	.pmt {
		display: inline-block;
		width: 0.6875rem;
		height: 0.59375rem;
		float: left;
		margin-left: 0.4375rem;
		margin-right: 0.25rem;
		margin-top: 0.4rem;
	}

	.pmz {
		display: inline-block;
		/* float: left; */
		font-size: 0.5rem;
		font-weight: 400;
		color: #333333;
		margin-right: 0.25rem;
		/* flex:1; */
		/* 	background:blue; */
		/* height:1.2rem; */
	}

	.pmjt {
		display: inline-block;
		float: left;
		width: 0.46875rem;
		height: 0.25rem;
		margin-top: 0.6rem;
		margin-left: 0rem;
	}

	.pm1,
	.pm2,
	.pm3,
	.pm4,
	.pm5,
	.pmnew {
		list-style: none;
		width: 5.03125rem;
		height: 1.375rem;
		/* 	background:red; */
		border-bottom: 0.03125rem solid #666666;
		line-height: 1.375rem;
	}

	.pmt1,
	.pmt2,
	.pmt3,
	.pmt4,
	.pmt5 {
		display: inline-block;
		width: 0.5625rem;
		height: 0.6875rem;
		float: left;
		margin-left: 0.8rem;
		margin-top: 0.3rem;
	}

	.pmtz1,
	.pmtz2,
	.pmtz3,
	.pmtz4,
	.pmtz5 {
		color: #666666;
		font-size: 0.4375rem;
		font-weight: 400;
		float: left;
		margin-left: 0.25rem;
		width: 3rem;
		height: 1.2rem;
		/* background:red; */
		text-align: left;
		/* 	background:red; */
		white-space:nowrap;
		overflow:hidden;
		text-overflow:ellipsis;
	}

	.pm6 {
		width: 5.03125rem;
		height: 1.375rem;
		border-bottom: 0.03125rem solid #666666;
		line-height: 1.5625rem;
		/* background:red; */
	}

	/* 中见部分图纸 */
	.drawing {
		width: 15.625rem;
		height: 15.625rem;
		/* background:red; */
		position: absolute;
		left: 25rem;
		top: 10rem;
	}

	/* 图片 */
	.drawingtop {
		width: 12.84375rem;
		height: 7.8125rem;
		/* background:plum; */
		margin-left: 1.3rem;
	}

	.drawingtop img {
		width: 100%;
		height: 100%;
	}

	/* 中间图片的汉字 */
	.drawinghz {
		width: 15.625rem;
		height: 3rem;
		/* background:blue; */
		font-size: 0.9375rem;
		font-family: PingFang SC;
		font-weight: 500;
		color: rgba(51, 51, 51, 1);
		line-height: 4.3rem;
	}

	/* 平面立面总按钮 */
	.drawingbut {
		width: 15.625rem;
		height: 4.7rem;
		/* background:plum; */
		display: flex;
		justify-content: space-between;
	}

	.drawpm {
		width: 5.46875rem;
		height: 4.7rem;
		/* background:blue; */
		margin-left: 2rem;
	}

	.drawlm {
		width: 5.46875rem;
		height: 4.7rem;
		/* background:blue; */
		margin-right: 1.6rem;
	}

	.drawdrop {
		/* padding:0.3125rem; */
		border: 0 !important;
		background-color: #FFFFFF !important;
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
	}

	.drawbtn {
		/* padding:0.125rem 0.25rem !important; */
		line-height: 0.8rem !important;
		border-radius: 0 !important;
		font-size: 0.6125rem !important;
		width: 4.76875rem !important;
		height: 0.775rem !important;
		border: none !important;
		color: #FFFFFF !important;
		padding:0.03125rem 0.25rem !important;
	}

	/* 右侧 */
	.uplm {
		width: 4.16125rem !important;
		height: 1.052rem !important;
		background: #ffffff;
		margin-top: 0rem;
		margin-bottom: 0rem;
		padding: 0.14rem 0rem 0.14rem 0.48rem  !important;
		border: 0 !important;
		background-color: #ffffff !important;
		border-radius: 0 !important;
		/* line-height:1.25rem; */
		/* font-size:0.1875rem; */
		font-family: PingFang SC;
		font-weight: 500;
		color: rgba(255, 255, 255, 1);
		/* background:url(../../assets/image/pmd.png) no-repeat; */
		/* background-size:100% 75%; */
		display: flex;
		justify-content: center;
	}

	.upbtn {
		width: 5.03125rem !important;
		height: 0.75rem !important;
		color: #333333 !important;
		line-height: 0.75rem !important;
		border-radius: 0 !important;
		font-weight: 500;
		font-size: 0.4225rem !important;
		border: none !important;
		margin-top:0.16rem;
	}
 .pltop{
 	width:2.6rem;
 	height:0.6rem;
 	background:red;
 	display:inline-block;
 	float:left;
 	background:url(../../assets/image/xjtz.png) no-repeat;
 	background-size:2.6rem 0.6rem;
 }
</style>
