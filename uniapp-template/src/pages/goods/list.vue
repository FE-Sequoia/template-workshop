<template>
  <view class="page_goods" id="goods_list">
    <uni-search-bar
      placeholder="搜索产品"
      @confirm="search_"
      @cancel="cancel"
      cancelText="取消"
      @input="input($event, 'title')"
    >
      <uni-icons slot="searchIcon" color="#999999" size="18" type="home" />
    </uni-search-bar>
	<view class="list_goods_wrapper a-start j-between">
		<view class="goods-type-wrapper">
			<view :class="'goods-type ' + selected_[index]" v-for="(item, index) in types" :key="index" @click="searchType(item.value, index)">{{item.text}}</view>
		</view>
		<view class="goods_wrapper" v-if="$check_action('/goods/list', 'get')">
			<list_goods :list="list"></list_goods>
		</view>
	</view>
    <uni-pagination
      class="pager"
      show-icon="true"
      :total="count"
      :pageSize="query.size"
      :current="query.page"
      @change="page_change"
    ></uni-pagination>
  </view>
</template>

<script>
import list_goods from "@/components/diy/list_goods.vue";
import list_tab from "@/components/diy/list_tab.vue";
import bar_orderby from "@/components/diy/bar_orderby.vue";
import mixin from "@/libs/mixins/page.js";

export default {
  mixins: [mixin],
  components: {
    list_goods,
    list_tab,
    bar_orderby,
  },
  data() {
    return {
      url_get_list: getApp().globalData.host + "/api/goods/get_list?like=0",
      list: [],
	  selected_: ["selected"],
      query: {
        title: "",
        page: 1,
        size: 6,
        type: "",
		orderby: "hits desc"
      },
      // 分类
      types: [{value:"",text:"全部"}],
      list_orderby: [
        {
          name: "销量",
          direction: "",
          command_asc: "`sales` asc",
          command_desc: "`sales` desc",
        },
        {
          name: "上架日期",
          direction: "",
          command_asc: "`create_time` asc",
          command_desc: "`create_time` desc",
        },
        {
          name: "价格",
          direction: "",
          command_asc: "`price` asc",
          command_desc: "`price` desc",
        },
        {
          name: "点击量",
          direction: "",
          command_asc: "`hits` asc",
          command_desc: "`hits` desc",
        },
      ],
    };
  },
  methods: {
    /**
     * 添加商品过滤
     */
    get_goods_type() {
      this.$get(getApp().globalData.host + "/api/goods_type/get_list", {}, (res) => {
        if (res.result) {
          let list = res.result.list;
          list.map((obj) => {
            this.types.push({value:obj.name,text:obj.name});
          });
        }
      });
    },

    input(e, key) {
      this.query[key] = e.value;
    },

    search_() {
      this.query.page = 1;
      this.get_list();
    },
    cancel() {
      this.query.title = "";
      this.search_();
    },
    // 改变分类标签
    searchType(v, index){
		var selected_ = []
		selected_[index] = "selected"
		this.selected_ = selected_
		this.query.type = v;
		this.query.page = 1;
		this.get_list();
	 
    },
    // 控制排序
    handleOrderby(o) {
      // console.log(o);
      // 取出对应的orderby

      // 重置其他排序的direction
      this.list_orderby.map((val) => {
        if (val.name !== o.text) {
          return (val.direction = "");
        }
      });

      // 找到对应的排序项，发送排序请求
      var obj_orderby = this.list_orderby.find((val) => val.name === o.text);
      if (o.direction === "") {
        this.query.orderby = "";
        this.search_();
      } else if (o.direction === "up") {
        this.query.orderby = obj_orderby.command_desc;
        this.search_();
      } else if (o.direction === "down") {
        this.query.orderby = obj_orderby.command_asc;
        this.search_();
      }
    },
  },
  mounted() {
    this.get_goods_type();
  },
};
</script>

<style lang="scss" scoped>
.page_goods {
  padding: var(--padding_base);
  .select {
    padding: 0 10px;

    &:after {
      content: "";
      display: block;
      clear: both;
    }
  }
}
.goods-type-wrapper {
	width: 20%;
}
.goods_wrapper {
	width: 80%;
}
.goods-type {
	box-sizing: border-box;
	padding: 5px 3px;
	border-radius: 5px;
	text-align: center;
	margin-bottom: 10px;
}
.goods-type.selected {
	border: 1px solid #f00;
	color: #f00;
}
</style>
