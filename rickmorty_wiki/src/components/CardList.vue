<template>
    <form class="SearchForm">
        <div class="SearchBlock">
            <div class="SearchBlockInput">
                <select class="FullWidthSelect" v-model="status"> 
                    <option value="" selected>Select Status</option>
                    <option value="Alive">Alive</option>
                    <option value="Dead">Dead</option>
                    <option value="Unknown">Unknown</option>
                </select>
                <input type="text" name="" placeholder="Search Name" id="" class="FullWidthInput" v-model="name">
            </div>
            <div class="FullWidthButton">
                <button class="FullWidthButton" @click="filterData">Search</button>
            </div>
        </div>
    </form>

    <div class="CardsBody">
        <div class="CardListContainer">
            <div class="CardList" v-for="cartoon in CartoonInfoData.results" :key="cartoon.id">
                <div class="CharacterCard">
                    <CharacterCard :cartoon="cartoon"></CharacterCard>
                </div>
            </div>
        </div>
    </div>

    <div class="ButtonPaginationContainer">
        <button v-if="page >= 2" class="ButtonPagination" @click="scrollToTopAndSetPage(1)">
            First
        </button> 
        <button v-if="page >= 2" class="ButtonPagination" @click="scrollToTopAndSetPage(page - 1)">
            Previous
        </button>
        <div class="DisplayPage">{{page}}</div>
        <button v-if="page < 41" class="ButtonPagination" @click="scrollToTopAndSetPage(page + 1)">
            Next
        </button>
        <button v-if="page <= 42" class="ButtonPagination" @click="scrollToTopAndSetPage(42)">
            Last
        </button>
    </div>
</template>

<script setup>
import CharacterCard from './CharacterCard.vue';
import { ref, watchEffect, computed } from 'vue';

const CartoonInfoData = ref({});
const page = ref(1);
const name = ref('');
const status = ref('');

const getPageUrl = computed(() => {
    let url = `https://rickandmortyapi.com/api/character/?page=${page.value}`;
    return url;
});

const scrollToTopAndSetPage = (newPage) => {
    window.scrollTo({
        top: 0,
        behavior: 'smooth',
    })
    page.value = newPage; // Установка нового значения страницы
};

async function getCartoonInfo() {
    const response = await fetch(getPageUrl.value);
    const data = await response.json();
    CartoonInfoData.value = data;
    console.log(data);
}

const filterData = async (e) => {
    e.preventDefault();
    page.value = 1; 
    let url = `https://rickandmortyapi.com/api/character/?page=${page.value}`;
    if(name.value){
        url += `&name=${name.value}`;
    }
    if(status.value){
        url += `&status=${status.value}`;
    }
    const response = await fetch(url);
    const data = await response.json();
    CartoonInfoData.value = data
    console.log(CartoonInfoData.value);
}



watchEffect(() => {
    getCartoonInfo();
});
</script>

<style scoped>
.SearchForm {
    display: flex;
    justify-content: center;
    margin-top: 32px;
}

.SearchBlock {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.SearchBlockInput {
    display: flex;
    justify-content: center;
    align-items: center;
}

.FullWidthInput{
    width: 100%;
    padding: 10px 20px;
    border-top-right-radius: 8px;
    border: none;
    font-size: clamp(16px, 2vw, 24px);
    background: #9a9a9a;
    color: white;
}

.FullWidthSelect{
    width: 100%;
    padding: 10px 20px;
    border-top-left-radius: 8px;
    font-size: clamp(16px, 2vw, 23px);
    background: #9a9a9a;
    color: white;
    border: none;
    
}

.FullWidthButton {
    width: 100%;
    padding: 0px 0px;
    height: 40px;
    border-bottom-right-radius:8px ;
    border-bottom-left-radius:8px ;
    border: 1px solid #818181;
    font-size: clamp(16px, 2vw, 24px);
    background: #9a9a9a;
    color: white;
    cursor: pointer;

}
.FullWidthSelect, .FullWidthInput, .FullWidthButton {
    width: 100%;
    outline: none;
}



.CardsBody {
    width: 100%;
    display: flex;
    justify-content: center;
    margin-top: 32px;
}

.CardListContainer {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}

.CharacterCard {
    width: 100%;
    /* Фиксированная ширина карточки */
    margin: 10px;
    /* Опционально, устанавливаем отступ вокруг карточки */
}

.ButtonPaginationContainer {
    width: 100%;
    display: flex;
    justify-content: center;
    margin: 24px 0px;
}

.ButtonPagination {
    padding: 10px;
    background-color: #818181;
    color: white;
    margin: 0 5px;
    border-radius: 8px;
    cursor: pointer;
    width: clamp(200px, 20vw, 300px);
    font-size: clamp(16px, 2vw, 24px);
}
.DisplayPage{
    padding: 10px;
    color: white;
    font-size: clamp(16px, 2vw, 24px);
}
</style>