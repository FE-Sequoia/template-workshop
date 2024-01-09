<template>
	<view class="page_i_want_to_customize diy_list diy_list_page div_list_tml" id="i_want_to_customize_list">
		<!-- 筛选模块(开始) -->
		<view>
			<view class="container">
				<view>
					<view>
						<view class="">
							<!-- 搜索栏 -->
																													<!-- /搜索栏 -->
						</view>
					</view>
				</view>

				<view>
					<view>
						<view class="tab_view">
							<!-- 筛选栏 -->
																										<uni-section title="定制类别" type="line">
							<uni-data-select
									@change="change_customized_categories"
									v-model="query['customized_categories']"
									:localdata="list_customized_categories"
							></uni-data-select>
							</uni-section>
																				<uni-section title="取货类别" type="line">
							<uni-data-select
									@change="change_pickup_category"
									v-model="query['pickup_category']"
									:localdata="list_pickup_category"
							></uni-data-select>
							</uni-section>
													<!-- /筛选栏 -->
						</view>
					</view>
				</view>

				<view>
					<view>
						<view class="sort_view">
							<!-- 排序 -->
							<view class="list_orderby">
								<bar_orderby :text="o.name" v-model:direction="o.direction" :direction.sync="o.direction"
											 v-for="(o,i) in list_orderby" :key="i" @handle="handleOrderby">
								</bar_orderby>
							</view>
							<!-- /排序 -->
						</view>
					</view>
				</view>
			</view>
		</view>
		<!-- 筛选模块(结束) -->
		<!-- 列表 -->
			<view class="warp" >
			<view class="container">
				<view v-for="(o,i) in list" class="row box_style" :key="i">
							<view class="col" v-if="0 && $check_field('get','product_name')">
						<view class="view">
							<view class="diy_title" v-if="true">
								<span>商品名称</span>
							</view>
										<view class="diy_field diy_text">
								<span>
									{{ o["product_name"] }}
								</span>
							</view>
									</view>
					</view>
							<view class="col" v-if="0 && $check_field('get','seller')">
						<view class="view">
							<view class="diy_title" v-if="true">
								<span>卖家</span>
							</view>
										<view class="diy_field diy_uid">
								<span>
									{{ get_user_seller(o['seller']) }}
								</span>
							</view>
									</view>
					</view>
							<view class="col" v-if="1 && $check_field('get','purchase_quantity')">
						<view class="view">
							<view class="diy_title" v-if="true">
								<span>购买数量</span>
							</view>
										<view class="diy_field diy_text">
								<span>
									{{ o["purchase_quantity"] }}
								</span>
							</view>
									</view>
					</view>
							<view class="col" v-if="1 && $check_field('get','price')">
						<view class="view">
							<view class="diy_title" v-if="true">
								<span>价格</span>
							</view>
										<view class="diy_field diy_text">
								<span>
									{{ o["price"] }}
								</span>
							</view>
									</view>
					</view>
							<view class="col" v-if="0 && $check_field('get','total_amount')">
						<view class="view">
							<view class="diy_title" v-if="true">
								<span>总金额</span>
							</view>
										<view class="diy_field diy_text">
								<span>
									{{ o["total_amount"] }}
								</span>
							</view>
									</view>
					</view>
							<view class="col" v-if="1 && $check_field('get','mall_users')">
						<view class="view">
							<view class="diy_title" v-if="true">
								<span>商城用户</span>
							</view>
										<view class="diy_field diy_uid">
								<span>
									{{ get_user_mall_users(o['mall_users']) }}
								</span>
							</view>
									</view>
					</view>
							<view class="col" v-if="0 && $check_field('get','customization_requirements')">
						<view class="view">
							<view class="diy_title" v-if="true">
								<span>定制要求</span>
							</view>
										<view class="diy_field diy_desc">
									<span>
										{{ obj["customization_requirements"] }}
									</span>
							</view>
									</view>
					</view>
							<view class="col" v-if="0 && $check_field('get','related_images')">
						<view class="view">
							<view class="diy_title" v-if=" false">
								<span>相关图片</span>
							</view>
										<view class="diy_field diy_img">
								<img :src="$fullUrl(o['related_images'])" width="100%" height="100" />
							</view>
									</view>
					</view>
							<view class="col" v-if="0 && $check_field('get','completion_time')">
						<view class="view">
							<view class="diy_title" v-if="true">
								<span>完成时间</span>
							</view>
										<view class="diy_field diy_datetime">
								<span>
									{{ $toTime(o["completion_time"] ,"yyyy-MM-dd hh:mm:ss") }}
								</span>
							</view>
									</view>
					</view>
							<view class="col" v-if="0 && $check_field('get','related_attachments')">
						<view class="view">
							<view class="diy_title" v-if="true">
								<span>相关附件</span>
							</view>
										<view class="diy_field diy_text">
								<span>
									{{ o["related_attachments"] }}
								</span>
							</view>
									</view>
					</view>
							<view class="col" v-if="0 && $check_field('get','customized_video')">
						<view class="view">
							<view class="diy_title" v-if="true">
								<span>定制视频</span>
							</view>
										<view class="diy_field diy_text">
								<span>
									{{ o["customized_video"] }}
								</span>
							</view>
									</view>
					</view>
							<view class="col" v-if="0 && $check_field('get','customized_audio')">
						<view class="view">
							<view class="diy_title" v-if="true">
								<span>定制音频</span>
							</view>
										<view class="diy_field diy_text">
								<span>
									{{ o["customized_audio"] }}
								</span>
							</view>
									</view>
					</view>
							<view class="col" v-if="0 && $check_field('get','required_date')">
						<view class="view">
							<view class="diy_title" v-if="true">
								<span>要求日期</span>
							</view>
										<view class="diy_field diy_date">
								<span>
									{{ $toTime(o["required_date"] ,"yyyy-MM-dd") }}
								</span>
							</view>
									</view>
					</view>
							<view class="col" v-if="0 && $check_field('get','customized_categories')">
						<view class="view">
							<view class="diy_title" v-if="true">
								<span>定制类别</span>
							</view>
										<view class="diy_field diy_text">
								<span>
									{{ o["customized_categories"] }}
								</span>
							</view>
									</view>
					</view>
							<view class="col" v-if="0 && $check_field('get','customization_details')">
						<view class="view">
							<view class="diy_title" v-if="true">
								<span>定制详情</span>
							</view>
										<view class="diy_field diy_desc">
									<span>
										{{ obj["customization_details"] }}
									</span>
							</view>
									</view>
					</view>
							<view class="col" v-if="0 && $check_field('get','pickup_category')">
						<view class="view">
							<view class="diy_title" v-if="true">
								<span>取货类别</span>
							</view>
										<view class="diy_field diy_text">
								<span>
									{{ o["pickup_category"] }}
								</span>
							</view>
									</view>
					</view>
							<view class="bottom-view">
									</view>
					<view class="col">
						<view class="view">
							<view class="create_time_block diy_filed diy_time">
								{{ $toTime(o["create_time"] ,"yyyy-MM-dd hh:mm:ss") }}

							</view>
						</view>
					</view>
					<view class="uni-padding-wrap uni-common-mt">
						<navigator :url="'./details?i_want_to_customize_id=' + o['i_want_to_customize_id']" class="btn btn-primary">查看详情</navigator>

					</view>
				</view>
			</view>
		</view>
			<!-- /列表 -->
		<!-- 分页器 -->
		<uni-pagination
				class="pager"
				show-icon="true"
				:total="count"
				:pageSize="query.size"
				:current="query.page"
				@change="page_change"
		></uni-pagination>
		<!-- /分页器 -->
	</view>
</template>

<script>
	import list_tab from "@/components/diy/list_tab.vue";
	import bar_orderby from "@/components/diy/bar_orderby.vue";
    import mixin from "@/libs/mixins/page.js";

	export default {
		mixins: [mixin],
		components: {
			list_tab,
			bar_orderby,
		},
		data() {
			return {
				url_get_list: "~/api/i_want_to_customize/get_list?like=0",
									// 用户列表
					list_user_seller: [],
																// 用户列表
					list_user_mall_users: [],
																						// 定制类别选项列表
				list_customized_categories: [{value:"全部",text:"全部"}],
									// 取货类别选项列表
				list_pickup_category: [{value:"全部",text:"全部"}],
							list_orderby: [
																				{
					name: '发布时间',
					direction: "",
					command_asc: '`create_time` asc',
					command_desc: '`create_time` desc'
				}
			],
					query: {
																						"customized_categories": "", // 定制类别
													"pickup_category": "", // 取货类别
									"examine_state": "已通过", // 审核状态
						"examine_reply": "", // 审核状态
						"i_want_to_customize_id": 0, // ID
						"page": 1,
						"size": 10
			},
			list: [],
					count: 50,
		}
		},
		methods: {


	/**
	 * 获取列表后
	 * @param {Object} json
	 * @param {Object} func
	 */
	get_list_after(json ,func){
		let list = json.result.list;
		if (func) {
			func(json);
		}
	},


	
			
			/**
	 * 获取卖家用户列表
	 */
	async get_list_user_seller() {
		var json = await this.$get("~/api/user/get_list?user_group=卖家");
		if(json.result && json.result.list){
			this.list_user_seller = json.result.list;
		}
		else if(json.error){
			console.error(json.error);
		}
	},
	get_user_seller(id){
		let obj = this.list_user_seller;
		let ret = "";
		for(let i=0;i<obj.length;i++){
			if(obj[i].user_id==id){
				ret = obj[i].nickname+"-"+obj[i].username;
			}
		}
		return ret;
	},
				
			
			
			
			/**
	 * 获取商城用户用户列表
	 */
	async get_list_user_mall_users() {
		var json = await this.$get("~/api/user/get_list?user_group=商城用户");
		if(json.result && json.result.list){
			this.list_user_mall_users = json.result.list;
		}
		else if(json.error){
			console.error(json.error);
		}
	},
	get_user_mall_users(id){
		let obj = this.list_user_mall_users;
		let ret = "";
		for(let i=0;i<obj.length;i++){
			if(obj[i].user_id==id){
				ret = obj[i].nickname+"-"+obj[i].username;
			}
		}
		return ret;
	},
				
			
			
			
			
			
			
						// 改变分类标签
	change_customized_categories(val) {
		if (val === "全部" || val === "") {
			this.query.customized_categories = "";
		}else{
			this.query.customized_categories = val
		}
		this.search_();
	},
			
		/**
	 * 获取定制类别列表
	 */
	async get_list_customized_categories() {
						var json = await this.$get("~/api/classification_information/get_list?");
		if(json.result && json.result.list){
			json.result.list.map((o) => this.list_customized_categories.push({value:o.customized_categories,text:o.customized_categories}));
		}
		else if(json.error){
			$.toast(json.error.message);
			console.error(json.error);
		}
			},
			
						// 改变分类标签
	change_pickup_category(val) {
		if (val === "全部" || val === "") {
			this.query.pickup_category = "";
		}else{
			this.query.pickup_category = val
		}
		this.search_();
	},
			
		/**
	 * 获取取货类别列表
	 */
	async get_list_pickup_category() {
					['送货上门','快递'].map((o) => this.list_pickup_category.push({value:o,text:o}));
					},
		
	input(e, key) {
		this.query[key] = e.value;
	},

	search_() {
		this.query.page = 1;
		this.get_list();
	},

	// 改变分类标签
	changeScreen(idx,key) {
		if (this.query[key] === "全部") {
			this.query[key] = "";
		}
		this.search_()
	},

	// 控制排序
	handleOrderby(o) {
		// console.log(o);
		// 取出对应的orderby

		// 重置其他排序的direction
		this.list_orderby.map(val => {
			if (val.name !== o.text) {
				return val.direction = ""
			}
		})

		// 找到对应的排序项，发送排序请求
		var obj_orderby = this.list_orderby.find(val => val.name === o.text)
		if (o.direction === "") {
			this.query.orderby = ""
			this.search_()
		} else if (o.direction === "up") {
			this.query.orderby = obj_orderby.command_desc
			this.search_()
		} else if (o.direction === "down") {
			this.query.orderby = obj_orderby.command_asc
			this.search_()
		}
	},

	/**
	 * 跳转地址
	 * @param {Object} id
	 */
	to_nav(id) {
		this.$nav('/pages/i_want_to_customize/details?i_want_to_customize_id=' + id)
	},


	},
	created() {
						this.get_list_user_seller();
													this.get_list_user_mall_users();
																				// 初始化定制类别列表
		this.get_list_customized_categories();
							// 初始化取货类别列表
		this.get_list_pickup_category();
			}
	}
</script>
<style scoped>
.container {
  box-shadow: none;
  -webkit-box-shadow: none;
}
.pager {
  margin-top: 1rem;
}
.uni-collapse {
  background-color: inherit;
}

.pager {
  margin-top: 1rem;
}

.tab_view {
  /* background-color: #ffffff; */
  margin: 0 auto;
}

.list_orderby {
  display: flex;
  justify-content: flex-start;
  /* background-color: #ffffff; */
  /* border-top: 5px double #ccc;
		border-bottom: 5px double #ccc; */
  margin-right: -1px;
}

.list_orderby .bar_orderby {
  border-left: 1px solid #ccc;
}
.change_table {
  height: 50px;
  margin: 0 var(--margin_base);
}
.btn_change_table {
  margin-left: auto;
  font-weight: bold;
  width: 100px;
  height: 37px;
  text-align: center;
  font-size: 0.875rem;
  border: 1px solid #cccccc;
  border-radius: 1rem;
  margin: 0.25rem;
  float: right;
}
.end-title {
  display: flex;
}
.end-title view {
  flex-grow: 1;
  text-align: center;
}
.end-cont {
  display: none;
  /* background: #c8c7cc; */
}
.btna {
  color: #ffffff;
  background: #00a0ff;
}
.dis {
  display: block;
}
.box_style {
  width: 44%;
  margin-bottom: 0.75rem;
  padding: 0.375rem;
  display: inline-block !important;
  border: 0.075rem solid #ccc;
  border-radius: 0.375rem;
  overflow: hidden;
}
.box_style:nth-child(even) {
  margin-left: 0.6rem;
}
.box_style:nth-child(even) {
  margin-left: 0.6rem;
}
.bottom-view,
.create_time_block {
  font-size: 12px;
  color: #666666;
}
.bottom-view view {
  display: inline-block;
}
.bottom-view span {
  margin-left: 5px;
  margin-right: 10px;
}
</style>
<style>
/* 新加样式 */
.uni-searchbar {
  background-color: #22b8b8;
}
.search_div .uni-searchbar .uni-searchbar__box {
  border-radius: 8px !important;
  height: auto;
}

.tab_view {
  margin: 8px auto;
  font-size: 14px;
}
.list_orderby {
  margin: 1rem;
}
.list_orderby .bar_orderby {
  margin-right: 0.5rem;
  border-left: 1px solid #ccc;
  background-color: #22b8b8;
  border-radius: 10px;
  padding: 5px;
}
.sort_view .bar_orderby .text {
  color: #fff;
}
/* 列表样式 */
.dis {
  width: 50%;
  display: inline-block;
}
.end-cont .warp .container {
  font-family: Arial, Helvetica, sans-serif;
  border: 2px solid #22b8b8;
  padding: 5px;
  /* margin-top: 10px; */
  border-radius: 8px;
  margin: 10px 5px 0 5px;
  font-size: 14px;
}
.col {
  padding: 5px;
}
.end-cont .warp .container .diy_img img {
  width: 100%;
  height: 100px;
  padding: 5px 0;
}
.diy_dj {
  display: inline-block;
  width: 50%;
}
.uni-common-mt {
  width: 100%;
}
.uni-common-mt .btn {
  font-size: 14px;
  color: #fff;
  background-color: #22b8b8;
  line-height: 2;
  margin-bottom: 8px;
  display: inline-block;
	  width: 100%;
	  text-align: center;
}
.diy_text{
	padding-left: 10px;
	 color:#22b8b8;
	 text-decoration: dashed;
}
.uni-common-mt .btn{
	display: inline-block;
	  width: 100%;
	  text-align: center;
}
.container {
  padding: 8px 0s;
}
.delete_btn{
	display: inline-block;
	padding-left: 8px;
	color: #22B8B8;
	text-decoration: underline;
}
.tab-wrapper {
	width: 20%;
}
.warp .container {
	width: 80%;
}
.page_i_want_to_customize .warp {
	display: flex;
	justify-content: space-between;
}
</style>
