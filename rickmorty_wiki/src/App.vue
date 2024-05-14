<template>
  <Header></Header> 
  <div style="margin:  0 auto;">
    <CardList></CardList>
  </div>

</template>

<script setup>
  import CardList from './components/CardList.vue';
  import Header from './components/Header.vue';
</script>

<style>
.App {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
</style>