<template>
	<view v-if="list.length > 0">
		<uni-drawer ref="showLeft" mode="left">
			<scroll-view style="height: 100%;" scroll-y="true">
				<text class="chapter_list_title">章节列表</text>
				<view style="margin-top: 5px;">
					<view @click="changeChapter(index)" v-for="(item, index) in list" :key="index" class="chapter_list" :class="{active: currentChapterIndex === index}">
						<text class="chapter_index">第{{index + 1}}章</text>
						<view class="chapter_name">{{item.chapter_name}}</view>
					</view>
				</view>
			</scroll-view>
		</uni-drawer>
		<view class="chapter_content">
			<text class="chapter_content_title">
				{{list[currentChapterIndex].chapter_name}}
			</text>
			<rich-text :style="{fontSize: fontSize + 'px'}" style="padding: 0 5px;" :nodes="list[currentChapterIndex].chapter_content"></rich-text>
		</view>
		<view style="display: flex;flex-direction: row;align-items: center;padding: 5px;">
			<text>字体大小</text>
			<view style="width: 80px;margin-left: 10px;">
				<uni-easyinput v-model="fontSize"></uni-easyinput>
			</view>
		</view>
		<view class="chapter_button">
			<button :disabled="currentChapterIndex <= 0" size="mini" @click="changeChapter('prev')">上一章</button>
			<button size="mini" @click="$refs.showLeft.open();">小说目录</button>
			<button :disabled="currentChapterIndex >= list.length -1" size="mini" @click="changeChapter('next')">下一章</button>
		</view>
	</view>
</template>

<script>
	import mixin from "@/libs/mixins/page.js";

	export default {
		mixins: [mixin],
		data() {
			return {
				field: 'novel_reading_id',
				url_get_list: "~/api/novel_chapters/get_list?",
				query: {
					"size": 7,
					"page": 1,
					"chapter_name": "",
					"novel_reading_id": 0,
					"orderby": `sort`
				},
				list: [],
				currentChapterIndex: 0,
				fontSize:16
			}
		},
		methods: {
			changeChapter(operate) {
				switch (operate) {
					case "prev": {
						this.currentChapterIndex--
						break;
					}
					case "next": {
						this.currentChapterIndex++
						break;
					}
					default: {
						this.currentChapterIndex = operate
					}
				}
			}
		}
	}
</script>

<style>
	.chapter_list_title{
		display: block;
		padding: 5px;
	}
	.chapter_list {
		padding: 5px;
		display: flex;
		flex-direction: row;
	}

	.active {
		background-color: #eeeeee;
	}

	.chapter_index {
		margin-left: 10px;
	}

	.chapter_name {
		margin-left: 10px;
	}

	.chapter_content {
		padding: 5px;
	}

	.chapter_content_title {
		display: block;
		width: 100%;
		text-align: center;
		font-size: 2rem;
		font-weight: bold;
	}

	.chapter_button {
		display: flex;
		flex-direction: row;
		justify-content: space-between;
		margin-top: 10px;
	}
</style>