<template>
  <div class="userPage">
    <h2>登録フォーム</h2>
    <div class="wrapper">
      <div class="nameForm">
        <label>
          <span>
            name：　
          </span>
          <input type="text" v-model="user.name" class="nameBox">
        </label>
      </div>
      <div class="emailForm">
        <label>
          <span>
            email：　
          </span>
          <input type="text"  v-model="user.email" class="emailBox">
        </label>
      </div>
      <div class="prefectureForm">
        <span>address：</span>
        <select name="pref_id" v-model="user.prefecture" class="prefectureBox">
          <option value=""><div id="user.prefecture" />選択してください</option>
          <option value="北海道">北海道</option>
          <option value="青森県">青森県</option>
          <option value="岩手県">岩手県</option>
          <option value="宮城県">宮城県</option>
          <option value="秋田県">秋田県</option>
          <option value="山形県">山形県</option>
          <option value="福島県">福島県</option>
          <option value="茨城県">茨城県</option>
          <option value="栃木県">栃木県</option>
          <option value="群馬県">群馬県</option>
          <option value="埼玉県">埼玉県</option>
          <option value="千葉県">千葉県</option>
          <option value="東京都">東京都</option>
          <option value="神奈川県">神奈川県</option>
          <option value="新潟県">新潟県</option>
          <option value="富山県">富山県</option>
          <option value="石川県">石川県</option>
          <option value="福井県">福井県</option>
          <option value="山梨県">山梨県</option>
          <option value="長野県">長野県</option>
          <option value="岐阜県">岐阜県</option>
          <option value="静岡県">静岡県</option>
          <option value="愛知県">愛知県</option>
          <option value="三重県">三重県</option>
          <option value="滋賀県">滋賀県</option>
          <option value="京都府">京都府</option>
          <option value="大阪府">大阪府</option>
          <option value="兵庫県">兵庫県</option>
          <option value="奈良県">奈良県</option>
          <option value="和歌山県">和歌山県</option>
          <option value="鳥取県">鳥取県</option>
          <option value="島根県">島根県</option>
          <option value="岡山県">岡山県</option>
          <option value="広島県">広島県</option>
          <option value="山口県">山口県</option>
          <option value="徳島県">徳島県</option>
          <option value="香川県">香川県</option>
          <option value="愛媛県">愛媛県</option>
          <option value="高知県">高知県</option>
          <option value="福岡県">福岡県</option>
          <option value="佐賀県">佐賀県</option>
          <option value="長崎県">長崎県</option>
          <option value="熊本県">熊本県</option>
          <option value="大分県">大分県</option>
          <option value="宮崎県">宮崎県</option>
          <option value="鹿児島県">鹿児島県</option>
          <option value="沖縄県">沖縄県</option>
        </select>
      </div>
      <div class="adddbUser">
        <button type="button" @click="submit" class="addUserBtn">保存</button>
      </div>
      <div class="getdataPage">
        <button @click="getData" class="getdataPageBtn">確認する</button>
      </div>
      <div class="userHome">
        <button><nuxt-link to="/">HOMEへ戻る</nuxt-link></button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      user: {
        name: "",
        email: "",
        prefecture: "",
      },
  }
},
  methods: {
    submit() {
      const dbSet = this.$firestore.collection('users')
      dbSet.doc('ag53CThTWnsHvabWGbEK')
      .set({
        name: this.user.name,
        email: this.user.email,
        prefecture: this.user.prefecture
      })

      .then(ref => {
        // ref.idでidを確認できる
        //console.log('Add ID: ', ref.id);
        this.user.name = "",
        this.user.email = "",
        this.user.prefecture = ""
      })
    },
    // データ取得
    // dataの中に入れてバインドさせる
      getData() {
        const dbGet = this.$firestore.collection('users')
        dbGet.doc('ag53CThTWnsHvabWGbEK')
        .get().then((doc) => {
          // console.log(doc.data().name);
          this.user.name = doc.data().name
          this.user.email = doc.data().email
          this.user.prefecture = doc.data().prefecture
        })
      }
  }
}
</script>

<style scoped>
.wrapper {
  width: 400px;
  margin-left: auto;
  margin-right: auto;
}
.nameForm,
.emailForm,
.prefectureForm,
.adddbUser,
.getdataPage,
.userHome {
  margin-top: 15px;
}
.prefectureBox,
.nameBox,
.emailBox,
.prefectureBox {
  width: 200px;
}
.nameBox,
.emailBox,
.prefectureBox,
.addUserBtn,
.getdataPageBtn {
  border: solid 1px black;
  border-radius: 5px;
}
.addUserBtn,
.getdataPageBtn {
  margin-top: 50px;
  margin-left: auto;
  margin-right: auto;
  width: 100px;
  height: 30px;
  text-align: center;
  background-color: PaleTurquoise;
  display: block;
  text-decoration: none;
  color: black;
  box-shadow: 2px 2px gray;
}
.userHome {
  width: 100px;
  margin-top: 100px;
  margin-left: auto;
  margin-right: auto;
}
</style>
