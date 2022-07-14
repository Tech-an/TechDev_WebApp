<template>
  <div class="main">
    <img alt="県章クイズのlogo" src="../assets/県章一覧.png" class="image" />
    <router-link to="/prefecSymbolQuiz" class="btn">県章クイズ</router-link>
  </div>
</template>

<script>
export default {};
</script>

<style>
.main {
  position: relative;
}
.btn {
  position: absolute;
  top: 50%;
  left: 0%;
  background: #fff;
  color: #000;
  width: 100%;
  font-size: 3rem;
  text-decoration: none;
}
.btn:hover {
  color: #361;
  font-weight: bold;
}
</style>
