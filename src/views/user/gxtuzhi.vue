<template>
	<div>
		<div class="zonggxtz" @click="cetuend" style="overflow:hidden;"></div>
		<div class="lefttopjzm">
			<div class="leftjzm">
				<img class="logojzm" src="../../assets/image/jinghekeji.png" />
				<Xunilogo v-show="xianyinxuni"></Xunilogo>
			</div>
		</div>
		<div class="pms" v-if="pmph"><img :src="pmdrawpicture" alt="" style="width:100%;height:100%;" /></div>
		<div>
			<!-- 右侧top部分 -->
			<div class="hometopjzmgxtz" v-show="hometop">
				<!-- 下拉菜单---项目 -->
				<el-dropdown style="float: left;margin-left:-1.4rem;">
					<div class="el-dropdown-link" @click="fngxtzmx">
						<img class="xmimggxtz" src="../../assets/image/bluefz.png" style="vertical-align:text-bottom;"/>
						<span class="xmgxtz">项目</span>
						<i style="display:inline-block;width:0.45rem;height:0.53125rem‬;margin-left:0.2rem;">
							<img src="../../assets/image/shang.png" alt="" style="width: 100%;height: 100%;" />
						</i>
					</div>
					<Newjian v-show="xianyin"></Newjian>
				</el-dropdown>
				<!-- 下拉菜单---项目--结束 -->
				<!-- 下拉菜单---社区 -->
				<el-dropdown style="float: left; margin-left:1.5rem;">
					<div class="el-dropdown-link" @click="fngxtzsq" @mouseenter="fnhsq()" @mouseleave="fnhsqlev()">
						<img class="sqimggxtz" :src="hsq" style="vertical-align:text-bottom;"/>
						<i class="sqgxtz" :style="hsqcolor">社区</i>
					</div>
				</el-dropdown>
				<!-- 下拉菜单---社区--结束 -->
				<!-- 下拉菜单---更多 -->
				<div class="moretopcomgxtz" style="height:0.93125rem;" @mouseenter="fnmorgxtz()" @mouseleave="fnmorlevgxtz()">
					<img :src="moretb" alt="" style="width:0.84375rem;height:0.8125rem;margin-right:0.16rem;float:left;vertical-align:text-bottom;"/>
					<span class="hgmorecomgxtz">更多</span>
					<i style="display:inline-block;width:0.45rem;height:0.53125rem‬;margin-left:0.2rem;"><img :src="nmgd" alt="" style="width: 100%;height: 100%;" /></i>
					<div class="moocomgxtz" style="margin-top:0.1rem;">
						<div class="mores1comgxtz"><a href="http://www.jh-bim.com/home/solution" target="_blank" style="display:inline-block;color:#666666;width:4.5rem;">帮助</a></div>
						<div class="mores1comgxtz" @click="fnabout">联系我们</div>
						<div class="moresbcomgxtz">版本号: v 1.0.3</div>
					</div>
				</div>
			</div>
			<!-- 新建项目/管线综合/图纸 -->
			<div style="width:18.75rem;height:0.6875rem;position: absolute;top:3.93125rem;left:8.21875rem;text-align:left;cursor:pointer;">
				<span style="margin-right:0.1875rem;color:#2180ED;font-size:0.5rem;font-weight:500;float:left;line-height:0.6875rem;">{{ projecttitgxtz }}</span>
				<i style="font-weight:900;font-style:normal;font-size:0.625rem;float:left;line-height:0.6875rem;">/</i>
				<span style="margin-right:0.1875rem;margin-left:0.15625rem;color:#2180ED;font-size:0.5rem;font-weight:500;float:left;line-height:0.7575rem;">管线综合</span>
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
							<div @click="pmtz" class="pmtzbox" style="display:flex;">
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
							<li v-for="(item, index) in drawingarr" :key="index" class="pmnew" style="position:relative;cursor: pointer;" @click="drawdanji(index)">
								<img src="../../assets/image/zk.png" class="pmt5" alt="" />
								<p class="pmtz5" v-show="!item.changegp" @dblclick="fnxgtz(index)" :title="item.drawName">{{ item.drawName }}</p>
								<input type="text" v-show="item.changegp" v-model="item.drawName" @blur="changepmg(index)" class="gxpms" />
							</li>
						</ul>
						<div class="pm6gt">
							<div>
								<uploader :file-status-text="statusText" :options="options" @file-complete="onFileSuccess">
									<!-- <uploader-unsupport></uploader-unsupport> -->
									<uploader-drop class="upgt">
										<uploader-btn :directory="false" :single="true" class="upbtngt" :attrs="attrs"><span class="pltop"></span></uploader-btn>
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
							<li v-for="(item, index) in arr" :key="index" @click="fnt()" class="pmnew" style="position:relative;">
								<img src="../../assets/image/zk.png" class="pmt5" alt="" />
								<div>
									<p class="pmtz5" v-show="!item.changelmg" @dblclick="fnlmtzg(index)" :title="item.drawName">{{ item.drawName }}</p>
								</div>
								<input
									v-model="item.drawName"
									v-show="item.changelmg"
									type="text"
									@blur="changelmg(index)"
									class="gxpms"
								/>
							</li>
							<div class="pm6gt">
								<div>
									<uploader :file-status-text="statusText" :options="options" @file-complete="onFileSuccess">
										<!-- <uploader-unsupport></uploader-unsupport> -->
										<uploader-drop class="upgt">
											<uploader-btn :directory="false" :single="true" class="upbtngt" :attrs="attrs"><span class="pltop"></span></uploader-btn>
										</uploader-drop>
										<!-- <uploader-list></uploader-list> -->
									</uploader>
								</div>
							</div>
						</ul>
					</div>
				</div>
			</div>

			<!-- 图纸-->
			<div class="gxtzdrawing" v-show="centerdra">
				<!-- 图纸中部图片 -->
				<div class="gxtzdrawingtop"><img src="../../assets/image/draw.png" alt="" /></div>
				<!-- 图纸中的汉字 -->
				<div class="gxtzdrawinghz">这里还没有图纸,需要上传哦</div>
				<!-- 平面图纸和立面图纸的按钮 -->
				<div class="gxtzdrawingbut">
					<!-- 平面 -->
					<div class="gxtzdrawpm">
						<div>
							<div>
								<uploader :file-status-text="statusText" :options="options" @file-complete="onFileSuccess">
									<!-- <uploader-unsupport></uploader-unsupport> -->
									<uploader-drop class="gxtzdrawdrop"><uploader-btn :directory="false" :single="true" class="gxtzdrawbtn" :attrs="attrs">上传平面图纸</uploader-btn></uploader-drop>
									<uploader-list class="pingmiancss"></uploader-list>
								</uploader>
							</div>
						</div>
					</div>
					<!-- 立面 -->
					<div class="gxtzdrawlm">
						<div>
							<div>
								<uploader :file-status-text="statusText" :options="options" @file-complete="onFileSuccess">
									<!-- <uploader-unsupport></uploader-unsupport> -->
									<uploader-drop class="gxtzdrawdrop"><uploader-btn :directory="false" :single="true" class="gxtzdrawbtn" :attrs="attrs">上传立面图纸</uploader-btn></uploader-drop>
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
import qs from 'qs';
import Newjian from './newjian';
import Xunilogo from './xunilogo';
import addressurls from '@/api/ip.js';
// import Zheader from './header';
export default {
	data() {
		return {
			showname22: true,
			//上传功能
			centerdra: true,
			updraw: true,
			drawpicture: '',
			title: '12312313122',
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
			arr: [],
			drawingarr: [],
			//总的等陆头部
			zheaderxy: true,
			lmore: require('../../assets/image/pmjtxia.png'),
			// 更多下拉
			nmgd: require('../../assets/image/pmjtxia.png'),
			// 联系我们
			abouts: false,
			//上传限制
			attrs: {
				accept: '.dwg'
			},
			options: {
				target: api.Uploadpipepingmian, //SpringBoot后台接收文件夹数据的接口
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
			// 社区默认状态
			hsq: require('../../assets/image/sq@2x.png'),
			hsqcolor: 'color:#333333',
			moretb: require('../../assets/image/more@2x.png'),
			projectidsdrawingarr: [],
			pmdrawpicture: '',
			pmph: true,
			// 新建项目中获取title
			projecttitgxtz: ''
		};
	},
	components: {
		Newjian,
		Xunilogo
		// Zheader
	},
	created() {
		// 右侧平面
		this.drawingarr = localStorage.getItem('pmxgg') ? JSON.parse(localStorage.getItem('pmxgg')) : [{ msg: '', changegp: false }];
		localStorage.getItem('pmxgg');
		// 右侧立面
		this.arr = localStorage.getItem('lmxgg') ? JSON.parse(localStorage.getItem('lmxgg')) : [{ msggs: '', changelmg: false }];
		localStorage.getItem('lmxgg');
		// 接收一下新建项目中的title
		this.projecttitgxtz = sessionStorage.getItem('projecttit');
		this.$eventbus.$on('shows', () => {
			this.xianyinxuni = true;
		});
		this.$eventbus.$on('showyin', () => {
			this.xianyinxuni = false;
		});
		this.$eventbus.$on('hometop', () => {
			this.hometop = true;
		});
		this.$eventbus.$on('xianyin', () => {
			this.xianyin = true;
		});
		this.$eventbus.$emit('shows');
		//展示图纸
		var prid = sessionStorage.getItem('projectid');
		if (prid != null && prid != undefined) {
			//该项目中是否有图纸 如果有则不显示上传图纸功能
			axios.get(api.getprojectids + '/2' + '/' + prid).then(result => {
				this.centerdra = true;
				this.projectidsdrawingarr = result.data;
				this.pmdrawpicture = addressurls.url + result.data[0].url;
				if (this.projectidsdrawingarr.length != 0) {
					this.centerdra = false;
				}
			});
			//绑定平面图纸
			axios.get(api.Pcreddrawing + '/2' + '/' + prid + '/1').then(result => {
				this.drawingarr = result.data;
			});
			//绑定立面图纸
			axios.get(api.Pcreddrawing + '/2' + '/' + prid + '/2').then(result => {
				this.arr = result.data;
			});
		}
	},
	mounted() {
		this.$eventbus.$emit('cezhan2', 'tuzhi');
		this.$eventbus.$emit('hometop');
	},
	methods: {
		// 右侧平面图纸双击事件
		fnxgtz(index) {
			this.$set(this.drawingarr[index], 'changegp', true);
		},
		// 右侧平面失焦事件
		changepmg(index) {
			this.$set(this.drawingarr[index], 'changegp', false);
			localStorage.setItem('pmxgg', JSON.stringify(this.drawingarr));
			console.log(localStorage.getItem('pmxgg'));
		},
		// 右侧立面图纸双击事件
		fnlmtzg(index) {
			this.$set(this.arr[index], 'changelmg', true);
		},
		// 右侧立面图纸失焦事件
		changelmg(index) {
			this.$set(this.arr[index], 'changelmg', false);
			localStorage.setItem('lmxgg', JSON.stringify(this.arr));
		},
		//上传成功事件
		onFileSuccess() {
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
		// 点击项目
		fngxtzmx() {
			this.$router.push('/Login');
		},
		// 点击社区
		fngxtzsq() {
			this.$router.push('/');
		},
		xjlmfn() {
			this.arr.push(6);
		},
		drawdanji(index) {
			var drawid = this.drawingarr[index].resPictureId;
			axios.get(api.SelectByPrimaryKey + '/' + drawid).then(result => {
				// console.log(result.data);
				this.drawpicture = addressurls.url + result.data.url;
			});
		},
		fns() {
			this.xianyin = !this.xianyin;
			this.$eventbus.$emit('showyin');
		},
		fn4() {
			this.loginWindow = 'display:block';
		},
		look() {
			this.$router.push('/onepengzhuang');
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
		// 划过更多
		fnmorgxtz() {
			this.moretb = require('../../assets/image/moress.png');
			this.nmgd = require('../../assets/image/shang.png');
		},
		// 移出更多
		fnmorlevgxtz() {
			this.moretb = require('../../assets/image/more@2x.png');
			this.nmgd = require('../../assets/image/pmjtxia.png');
		},
		// 移入社区的时候
		fnhsq() {
			this.hsq = require('../../assets/image/shequ.png');
			this.hsqcolor = 'color:#2180ED';
		},
		// 移出社区的时候
		fnhsqlev() {
			(this.hsq = require('../../assets/image/sq@2x.png')), (this.hsqcolor = 'color:#333333');
		}
	}
};
</script>

<style>
.moretopcomgxtz {
	position: relative;
	float: left;
	margin-left: -1.4rem;
	font-size: 0.625rem;
	font-family: MicrosoftYaHei;
	font-weight: 400;
	font-style: normal;
	line-height: 0.93125rem;
	margin-top: 0.38rem;
	margin-left: 1.62rem;
	text-align: left;
	cursor: pointer;
}
.hgmorecomgxtz {
	color: #333333;
}
.moocomgxtz {
	width: 4.75rem;
	background: rgba(225, 225, 225, 0.2);
	padding-left: 0.2rem;
	padding-right: 0.25rem;
	cursor: pointer;
	display: none;
}
.mores1comgxtz {
	width: 4.65rem;
	height: 0.9rem;
	border-bottom: 1px solid #999999;
	text-align: left;
	line-height: 1rem;
	color: #666666;
	font-size: 0.46rem;
	font-weight: 500;
}
.moresbcomgxtz {
	border: 0;
	text-align: left;
	line-height: 0.9rem;
	color: #666666;
	font-size: 0.46rem;
	font-weight: 500;
}
.moretopcomgxtz:hover .moocomgxtz {
	display: block;
}
.moretopcomgxtz:hover .hgmorecomgxtz {
	color: #2180ed;
}
.moretopcomgxtz:hover .shouye {
	transform: rotate(180deg);
}
.pingmiancss {
	left: -1.25rem;
	width: 14.375rem;
}
.limiancss {
	left: -7.8rem;
	width: 14.375rem;
}
.gxtzmore {
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
.gxtzmoo {
	width: 4.75rem;
	padding-left: 0.2rem;
	padding-right: 0.25rem;
	cursor: pointer;
}
.gxtzmores1 {
	width: 4.65rem;
	height: 0.9rem;
	border-bottom: 1px solid #999999;
	text-align: left;
	line-height: 0.9rem;
	color: #666666;
	font-size: 0.46rem;
	font-weight: 500;
}
.gxtzmoresb {
	border: 0;
	text-align: left;
	line-height: 0.9rem;
	color: #666666;
	font-size: 0.46rem;
	font-weight: 500;
}
a {
	color: #333333;
	text-decoration: none;
}
* {
	padding: 0;
	margin: 0;
}
.zonggxtz {
	width: 60rem;
	height: 33.75rem;
	position: relative;
}
.el-main {
	padding: 0 !important;
}
.login-img3 {
	cursor: pointer;
	float: left;
	display: inline-block;
}
/* 主页top部分*/
.hometopjzmgxtz {
	position: absolute;
	top: 0.6275rem;
	left: 7.2rem;
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
	position: absolute;
	top: 0rem;
}
.el-dropdown-link {
	cursor: pointer;
	color: #333333;
}
.xmimggxtz {
	width: 0.84375rem;
	height: 0.8125rem;
	padding-left: 2.5rem;
	padding-top: 0.0625rem;
}
.xmgxtz {
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
.sqimggxtz,
.bjimggxtz {
	width: 0.84375rem;
	height: 0.8125rem;
}
.sqgxtz {
	width: 1.25rem;
	height: 0.5625rem;
	font-size: 0.625rem;
	font-family: MicrosoftYaHei;
	font-weight: 400;
	padding-left: 0.1875rem;
	font-style: normal;
}
.moreimggxtz {
	width: 0.78125rem‬;
	height: 0.78125rem;
}
.moregxtz {
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
	font-size: 0.5rem;
	font-weight: 400;
	color: #333333;
	margin-right: 0.25rem;
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
	text-align: left;
	white-space: nowrap;
	overflow: hidden;
	text-overflow: ellipsis;
}
.pm6gt {
	width: 5.03125rem;
	height: 1.375rem;
	border-bottom: 0.03125rem solid #666666;
	line-height: 1.5625rem;
}
.pm6gt img {
	width: 2.46875rem;
	height: 0.59375rem;
}
.pms {
	width: 47.8125rem;
	height: 28.4375rem;
	line-height: 28.4375rem;
	position: absolute;
	top: 5rem;
	left: 6.875rem;
}
/* 中见部分图纸 */
.gxtzdrawing {
	width: 15.625rem;
	height: 15.625rem;
	position: absolute;
	left: 25rem;
	top: 10rem;
}
/* 图片 */
.gxtzdrawingtop {
	width: 12.84375rem;
	height: 7.8125rem;
	margin-left: 1.3rem;
}
.gxtzdrawingtop img {
	width: 100%;
	height: 100%;
}
/* 中间图片的汉字 */
.gxtzdrawinghz {
	width: 15.625rem;
	height: 3rem;
	font-size: 0.9375rem;
	font-family: PingFang SC;
	font-weight: 500;
	color: rgba(51, 51, 51, 1);
	line-height: 4.3rem;
}
/* 平面立面总按钮 */
.gxtzdrawingbut {
	width: 15.625rem;
	height: 4.7rem;
	display: flex;
	justify-content: space-between;
}
.gxtzdrawpm {
	width: 5.46875rem;
	height: 4.7rem;
	margin-left: 2rem;
}
.gxtzdrawlm {
	width: 5.46875rem;
	height: 4.7rem;
	margin-right: 1.6rem;
}
.gxtzdrawdrop {
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
}
.gxtzdrawbtn {
	/* padding:0.125rem 0.25rem !important; */
	line-height: 0.8rem !important;
	border-radius: 0 !important;
	font-size: 0.6125rem !important;
	width: 4.76875rem !important;
	height: 0.775rem !important;
	border: none !important;
	color: #ffffff !important;
	padding: 0.03125rem 0.25rem !important;
}
.gxpms {
	position: absolute;
	left: 1.4rem;
	top: 0.2rem;
	width: 3.3125rem;
	height: 0.875rem;
}
/* 右侧 */
.upgt {
	width: 4.13125rem !important;
	height: 1.052rem !important;
	background: #ffffff;
	margin-top: 0rem;
	margin-bottom: 0rem;
	padding: 0.14rem 0rem 0.14rem 0.48rem !important;
	border: 0 !important;
	background-color: #ffffff !important;
	border-radius: 0 !important;
	/* line-height:1.25rem; */
	/* font-size:0.3875rem; */
	font-family: PingFang SC;
	font-weight: 500;
	color: rgba(255, 255, 255, 1);
	/* background:url(../../assets/image/pmd.png) no-repeat; */
	/* background-size:100% 75%; */
	display: flex;
	justify-content: center;
}
.upbtngt {
	width: 4.03125rem !important;
	height: 0.75rem !important;
	color: #333333 !important;
	font-size: 0.2rem !important;
	line-height: 0.75rem !important;
	border-radius: 0 !important;
	font-size: 0.4225rem !important;
	border: none !important;
	margin-top: 0.16rem;
}
.pltop {
	width: 2.6rem;
	height: 0.6rem;
	background: red;
	display: inline-block;
	float: left;
	background: url(../../assets/image/xjtz.png) no-repeat;
	background-size: 2.6rem 0.6rem;
}
</style>
