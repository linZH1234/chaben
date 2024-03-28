
<template>
  <view class="container">
    <web-view :src="externalUrl"></web-view>
  </view>
</template>
 
<script>
export default {
  data() {
    return {
      externalUrl: ''
    };
  },
	 onLoad(e) {
		// 传入需要跳转的链接 使用web-view标签进行跳转
		this.externalUrl = decodeURIComponent(e.url)
		console.log(this.externalUrl)
	}
};
</script>
 
<style scoped>
.container {
  width: 100%;
  height: 100vh;
}
</style>