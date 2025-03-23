<template>
  <view class="modal-mask" @click="onMaskClick" v-if="isShow">
    <view class="modal-container" @click.stop>
      <view class="modal-title">{{ title }}</view>
      <image :src="imageSrc" mode="aspectFit"></image>
      <input v-model="answer" placeholder="点击这里输入上面红框内文字" />
      <view class="modal-buttons">
        <button @click="closeModal">取消</button>
        <button @click="submitAnswer">提交</button>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  props: {
    title: {
      type: String,
      default: ''
    },
    imageSrc: {
      type: String,
      default: ''
    }
  },
  data() {
    return {
      isShow: false,
      answer: ''
    };
  },
  methods: {
    showModal() {
      this.isShow = true;
    },
    closeModal() {
      this.isShow = false;
      this.answer = '';
      this.$emit('cancel');
    },
    submitAnswer() {
      if (!this.answer) {
        uni.showToast({
          title: '答案不能为空！',
          icon: 'none'
        });
        return;
      }
      this.isShow = false;
      this.$emit('confirm', this.answer);
      this.answer = '';
    },
    onMaskClick(event) {
      if (event.target === event.currentTarget) {
        this.closeModal();
      }
    }
  }
};
</script>

<style scoped>
.modal-mask {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal-container {
  background-color: #fff;
  border-radius: 8px;
  padding: 20px;
  width: 80%;
}

.modal-title {
  font-size: 18px;
  font-weight: bold;
  margin-bottom: 10px;
}

.modal-buttons {
  display: flex;
  justify-content: space-around;
  margin-top: 20px;
}
</style>