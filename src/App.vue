<template>
    <!-- ナビゲーションバー -->
    <nav class="bg-white shadow-md mb-10">
      <ul class="flex justify-center space-x-6 py-4">
        <li><router-link class="text-gray-700 hover:text-black transition" to="/home">MRB</router-link></li>
        <li v-if="isAuthenticated" class="cursor-pointer text-gray-700 hover:text-black transition" @click="logout">Logout</li>
      </ul>
    </nav>
    <!-- ルートで指定されたコンポーネントを表示 -->
    <router-view />
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      isAuthenticated: !!localStorage.getItem('token') // ログインしているかどうかの状態を確認
    };
  },
  methods: {
    logout() {
      // 誤操作によるログアウトを防止する確認フォーム
      if(confirm("ログアウトしますか？")){
        // ログアウト処理
        localStorage.removeItem('token'); // トークンを削除
        
        this.$router.push('/login'); // ログインページ
      }
    }
  },
  watch: {
    // 認証状態が変わったときに再評価
    // 値が更新されないままルーターに評価されることを防ぐ
    $route() {
      this.isAuthenticated = !!localStorage.getItem('token');
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
