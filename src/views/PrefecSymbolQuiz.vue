<template>
  <div class="container">
    <h1 class="title">県章クイズ!!</h1>
    <p>連続正解数:{{ consecutiveCorrectNum }}</p>
    <p>正解数:{{ correctNum }}</p>
    <div class="quiz_image">
      <img :src="require(`@/assets/symbols/${targetName}.webp`)" alt="" />
    </div>
    <div class="choices" v-if="doing">
      <div
        class="choice"
        v-for="choice in choices"
        :key="choice"
        @click="answer(choice)"
      >
        {{ choice }}
      </div>
    </div>
    <div v-else>
      <div class="feedback">{{ feedback }}</div>
      <button @click="setQuiz()">次へ</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      doing: null,
      feedback: null,
      targetNum: null,
      targetName: null,
      correctNum: 0,
      consecutiveCorrectNum: 0,
      prefectures: [
        "北海道",
        "青森県",
        "岩手県",
        "宮城県",
        "秋田県",
        "山形県",
        "福島県",
        "茨城県",
        "栃木県",
        "群馬県",
        "埼玉県",
        "千葉県",
        "東京都",
        "神奈川県",
        "新潟県",
        "富山県",
        "石川県",
        "福井県",
        "山梨県",
        "長野県",
        "岐阜県",
        "静岡県",
        "愛知県",
        "三重県",
        "滋賀県",
        "京都府",
        "大阪府",
        "兵庫県",
        "奈良県",
        "和歌山県",
        "鳥取県",
        "島根県",
        "岡山県",
        "広島県",
        "山口県",
        "徳島県",
        "香川県",
        "愛媛県",
        "高知県",
        "福岡県",
        "佐賀県",
        "長崎県",
        "熊本県",
        "大分県",
        "宮崎県",
        "鹿児島県",
        "沖縄県",
      ],
      questions: [],
      choices: [],
    };
  },
  created() {
    this.questions = this.prefectures;
    this.setQuiz();
  },
  methods: {
    getChoices(num) {
      const copys = [...this.prefectures];
      return this.prefectures.map((_, i) => {
        if (i == 0) {
          copys.forEach((item, index) => {
            if (item === this.targetName) {
              copys.splice(index, 1);
            }
          });
          return this.targetName;
        } else if (i++ < num) {
          const i = Math.floor(Math.random() * copys.length);
          return copys.splice(i, 1)[0];
        } else {
          return null;
        }
      });
    },
    answer(choice) {
      this.doing = false;
      if (choice === this.targetName) {
        this.feedback = "正解!!!";
        this.correctNum++;
        this.consecutiveCorrectNum++;
      } else {
        this.feedback = "不正解...";
        this.consecutiveCorrectNum = 0;
      }
    },
    setQuiz() {
      this.doing = true;
      this.targetNum = Math.floor(Math.random() * this.questions.length);
      this.targetName = this.questions.splice(this.targetNum, 1)[0];
      this.choices = this.getChoices(4).splice(0, 4);
      console.log(this.questions.length);
    },
  },
};
</script>

<style>
.choice {
  cursor: pointer;
  margin: 20px 20px;
}
.choices {
  display: flex;
  justify-content: center;
}
</style>
