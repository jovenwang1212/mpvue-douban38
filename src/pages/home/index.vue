<template>
  <div>
    <!-- 头部 -->
    <div class="header">
      <span>豆瓣</span>
      <icon type="search"
            size="18"
            color="#00b600">
      </icon>
      <button>打开豆瓣App</button>
    </div>

    <div class="content">
      <!-- 影院热映 -->
      <div>
        <p class="title">
          <span>影院热映</span>
          <span class="more">更多</span>
        </p>

        <!-- 横向滚动 -->
        <scroll-view class="scroll-view_H"
                     scroll-x="true"
                     bindscroll="scroll"
                     style="width: 100%">
          <view id="demo1"
                class="scroll-view-item_H demo-text-1">1</view>
          <view id="demo2"
                class="scroll-view-item_H demo-text-2">2</view>
          <view id="demo3"
                class="scroll-view-item_H demo-text-3">3</view>
          <view id="demo3"
                class="scroll-view-item_H demo-text-3">4</view>
          <view id="demo3"
                class="scroll-view-item_H demo-text-3">5</view>
          <view id="demo3"
                class="scroll-view-item_H demo-text-3">6</view>
          <view id="demo3"
                class="scroll-view-item_H demo-text-3">7</view>
        </scroll-view>

      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      // 影院热映的电影列表
      theaterMovies: []
    }
  },

  onLoad () {
    // console.log('发请求')
    this.getTheaterMovies()
  },
  methods: {
    // 获取的电影
    getTheaterMovies () {
      wx.request({
        url: 'https://api.douban.com/v2/movie/in_theaters?apikey=0df993c66c0c636e29ecbb5344252a4a',
        header: {
          'content-type': 'application/x-www-form-urlencoded'
        },
        success: res => {
          // console.log(res)
          const { statusCode, data: { subjects } } = res
          if (statusCode === 200) {
            console.log(subjects)
            this.theaterMovies = subjects
          }
        }
      })
    }
  }

}
</script>

<style lang="less">
.header {
  display: flex;
  align-items: center;
  border: 1rpx solid #eee;
  height: 94rpx;
  padding: 0 36rpx;
  span {
    font-size: 18px;
    color: #00b600;
  }
  icon {
    flex: 1;
    margin: 4rpx 0 0 28rpx;
  }
  button {
    width: 200rpx;
    height: 58rpx;
    background-color: #42bd56;
    color: #fff;
    line-height: 58rpx;
    font-size: 12px;
  }
}

.title {
  height: 88rpx;
  line-height: 88rpx;
  display: flex;
  justify-content: space-between;
  padding: 0 38rpx;
  .more {
    color: #42bd56;
  }
}

.scroll-view_H {
  white-space: nowrap;
}
.scroll-view-item_H {
  width: 200rpx;
  height: 200rpx;
  background-color: green;
  display: inline-block;
}
</style>