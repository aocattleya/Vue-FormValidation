<template>
  <div>
    <p>
      <b>{{title}}</b>
    </p>
    <form v-on:submit.prevent="onSubmit">
      <span>ID :</span>
      <input type="text" placeholder="input your id" v-model="loginForm.loginId">
      <p>Input loginId is {{ loginForm.loginId }}</p>
      <p class="error">{{ Validation.loginReult }}</p>
      <button v-on:click="checkFrom">送信する</button>
    </form>
  </div>
</template>

<script>
export default {
  props: {
    title: String
  },
  data: function() {
    return {
      loginForm: {
        loginId: null
      },
      Validation: {
        loginReult: ""
      }
    };
  },
  methods: {
    checkFrom: function(event) {
      var LoginId = false;

      //IDの入力フォームのバリデーション
      if (!this.loginForm.loginId) {
        this.Validation.loginReult = "ログインIDを入力してください";
      } else if (!this.checkString(this.loginForm.loginId)) {
        this.Validation.loginReult = "半角英数で入力してください";
      } else {
        LoginId = true;
      }

      if (LoginId == true) {
        this.Validation.loginReult = "";
        alert("Hello," + this.loginForm.loginId + "!");
      }
      event.preventDefault();
    },
    checkString: function(inputdata) {
      var re = /^[A-Za-z0-9]*$/;
      return re.test(inputdata);
    }
  }
};
</script>

<style scoped>
.error {
  color: red;
}
</style>