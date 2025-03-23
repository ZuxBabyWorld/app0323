<template>
  <view class="container">
    <view class="card">
      <view class="card-body">
        <view class="card-title">
          <text style="color: red;">警告</text>:ID<text style="color: red;">只能登录App Store苹果商店</text>下载 更新, <text style="color: #ff00ff;">禁止(设置内登录iCloud)</text>否则后果自负登录
        </view>
        <view class="card-title">
          安全提示必选[<text style="color: #ff00ff;">其他选项</text>]在选[<text style="color: #ff00ff;">不升级</text>]
        </view>
        <view class="card-title">
          <button @click="openTutorial">登录 教程图 新手必看 否则后果自负</button>
        </view>
        <button @click="copyUsername">点击复制账号</button>
        <button @click="startQuiz">点击复制密码</button>
      </view>
    </view>
    <question-modal
      ref="questionModal1"
      :title="question1Title"
      :imageSrc="question1Image"
      @confirm="handleQuestion1Confirm"
      @cancel="handleQuestionCancel"
    ></question-modal>
    <question-modal
      ref="questionModal2"
      :title="question2Title"
      :imageSrc="question2Image"
      @confirm="handleQuestion2Confirm"
      @cancel="handleQuestionCancel"
    ></question-modal>
  </view>
</template>

<script>
import QuestionModal from '@/components/questionModal.vue';

export default {
  components: {
    QuestionModal
  },
  data() {
    return {
      username: 'qwe3333r@163.com',
      password: 'Rr112211',
      tutorialImage: '/static/appleid登录教程.jpg',
      question1Title: '1.登录App Store出现AppleID安全提示，点什么？',
      question1Image: '/static/其他选项.png',
      question2Title: '2.点击其他选项后，弹出的新窗口应该点什么？',
      question2Image: '/static/不升级.png'
    };
  },
  methods: {
    copyUsername() {
      uni.setClipboardData({
        data: this.username,
        success: () => {
          uni.showToast({
            title: '账号复制成功',
            icon: 'success',
            duration: 1000
          });
        }
      });
    },
    openTutorial() {
      uni.previewImage({
        urls: [this.tutorialImage],
        current: this.tutorialImage
      });
    },
    startQuiz() {
      this.$refs.questionModal1.showModal();
    },
    handleQuestion1Confirm(answer) {
      if (answer === '其他选项') {
        this.$refs.questionModal2.showModal();
      } else {
        uni.showToast({
          title: '回答错误，请查看下方App Store登录教程。',
          icon: 'none'
        });
      }
    },
    handleQuestion2Confirm(answer) {
      if (answer === '不升级') {
        this.copyPassword();
      } else {
        uni.showToast({
          title: '回答错误，请查看下方App Store登录教程。',
          icon: 'none'
        });
      }
    },
    handleQuestionCancel() {
      // 用户取消回答问题的处理逻辑
    },
    copyPassword() {
      uni.setClipboardData({
        data: this.password,
        success: () => {
          uni.showToast({
            title: '密码复制成功',
            icon: 'success',
            duration: 1000
          });
        }
      });
    }
  }
};
</script>

<style>
.container {
  padding: 20px;
}

.card {
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
}

.card-title {
  margin-bottom: 10px;
}

button {
  margin-top: 10px;
  padding: 10px 20px;
  background-color: #4CAF50;
  color: white;
  border: none;
  border-radius: 5px;
}
</style>