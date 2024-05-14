<template>

    <main class="Card">
      <div class="image">
        <img class="CharacterImage" :src="cartoon.image">
      </div>
      <aside>
        <ul class="CharacterInfoList">
          <li><span ><h1 class="CharacterName" >{{ cartoon.name }}</h1></span></li>
          <li><span><span class="CharacterStatus"><span class="indicator" :class="{'IfAlive': cartoon.status === 'Alive', 'IfDead': cartoon.status === 'Dead', 'IfUnknown': cartoon.status === 'unknown'}">•</span> {{ cartoon.status }} - {{ cartoon.species }}</span> </span></li>
          <li>
            <div class="InfoTooltip"> known location</div>
            <span class="CharacterInfo">{{ cartoon.location.name }}</span></li>
          <li>
            <div class="InfoTooltip"> seen in</div>
            <span class="CharacterInfo">  {{ cartoon.origin.name }}</span>
          </li>
        </ul>
      </aside>
    </main>

</template>

<script setup>
import {defineProps } from 'vue';
defineProps({
  cartoon: Object
})
</script>

<style scoped>

.Card {
  width: 700px; /* Adjust the width based on your layout */
  height: 220px;
  border-radius: 10px;
  display: flex;
  flex-direction: row;
  background-color: #818181;
  box-shadow: 0 0 5px 3px rgb(75, 75, 75);
  transition: all 0.2s ease-in-out;
  margin: 5px 5px;
}

.CharacterImage{
  max-width:  190px;
  height: 220px;
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
}

.image {
  width: 190px;
}

.CharacterInfoList{
  margin-left: 16px;
}

.CharacterInfoList li {
  list-style-type: none; /* Убираем стандартные маркеры у всех элементов списка */
  color: green;
  margin: 0;
  padding: 0;
}


.CharacterInfo{
  color: white;
  font-size: 1.4rem;
}

.InfoTooltip{
  color: rgba(0, 0, 0, 0.638);
  font-size: 1.2rem;
  margin-top: 12px;
}

.CharacterStatus {
  font-size: 24px;
  color: white;
}

.TopText{
  display: flex;
  flex-direction: column;
}

.CharacterName{
  font-size: 1.8rem;
  font-weight: 900;
  color: rgb(255, 255, 255)
}

.indicator {
  font-size: 30px;
}

.IfDead{
  color: red;
}

.IfAlive{
  color: green;
}

.ifUnknown{
  color: white;
}

.Card:hover {
  box-shadow: 0 0 10px 5px rgb(37, 37, 37);
  background: #9e9e9e;
  transform: scale(1.05);
}

@media screen and (max-width: 750px) {
  .Card{
    display: flex;
    flex-direction: column;
    width: 300px;
    height: auto;
  }
  .CharacterImage{
    max-width:  300px;
    width: 300px;
    border-bottom-left-radius:0px;
    border-top-right-radius: 10px;
  }
}
@media screen and (max-width: 300px) {
  .Card{
    display: flex;
    flex-direction: column;
    width: 200px;
  }
  .CharacterImage{
    max-width:  200px;
    width: 200px;
  }
}
</style>