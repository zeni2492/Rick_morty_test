<template>
  <div>
    <h1>Rick and Morty Wiki</h1>
  </div>
</template>

<style scoped>
div {
  width: 100%;
  font-size: 40px;
  background: #fff;
  height: 300px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-image: url('../assets/6602287690a7152964c257976c0fd3c1.jpg');
  background-size: cover;
  background-repeat: no-repeat;
}

h1 {
  font-size: 112px;
  font-family: Rickmorty, sans-serif;
  color: rgb(0, 173, 185);
  text-transform: uppercase;
  font-weight: 900;
  -webkit-text-stroke: 0.01px #d0ff00c4;
  text-shadow: 0 0 10px #d0ff00c4, 0 0 20px #00eeff
    /* Эффект свечения (можно настроить) */
}

@media screen and (max-width: 500px) {
  h1 {
    font-size: 60px;
  }
}
</style>