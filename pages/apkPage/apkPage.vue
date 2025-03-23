<template>
  <view class="container">
    <button @click="sendRequest">点击我</button>
  </view>
</template>

<script>
export default {
  methods: {
    sendRequest() {
      uni.request({
        url: 'https://cors.thezuxbbaabb.top/?https://httpbin.org/post',
        method: 'POST',
        header: {
          'x-foo': 'bar',
          'x-bar': 'foo',
          'x-cors-headers': JSON.stringify({
            'cookies': 'x=123'
          })
        },
        success: (res) => {
          const headers = JSON.parse(res.header['cors-received-headers']);
          console.log(headers);
          console.log(res.data);
        },
        fail: (err) => {
          console.error('请求失败:', err);
        }
      });
    }
  }
}
</script>

<style>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

button {
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  border: none;
  background-color: #4CAF50;
  color: white;
}
</style>