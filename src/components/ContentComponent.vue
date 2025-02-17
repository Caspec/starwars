<template>
    <div class="text-center">
      <h2 class="text-warning">Explore the Star Wars Universe</h2>
      <p>Find information about your favorite characters, planets, and age.</p>
  
      <div class="d-flex justify-content-center mb-3">
      <div class="dropdown mx-2">
        <button class="btn btn-outline-warning dropdown-toggle" type="button" id="dropdownGender" data-bs-toggle="dropdown" aria-expanded="false">
            Filter by Gender: {{ genderOptions[genderFilter] || genderOptions.all }}
        </button>
        <ul class="dropdown-menu" aria-labelledby="dropdownGender">
          <li>
            <a class="dropdown-item" href="#" @click="setGenderFilter('')">All</a>
          </li>
          <li>
            <a class="dropdown-item" href="#" @click="setGenderFilter('male')">Male</a>
          </li>
          <li>
            <a class="dropdown-item" href="#" @click="setGenderFilter('female')">Female</a>
          </li>
        </ul>
      </div>

      <div class="dropdown mx-2">
        <button class="btn btn-outline-warning dropdown-toggle" type="button" id="dropdownBirthYear" data-bs-toggle="dropdown" aria-expanded="false">
           Filter by Birth Year:  {{ birthYearFilter.min === 0 && birthYearFilter.max === 1000 ? 'All Years' : (birthYearFilter.min === 20 && birthYearFilter.max === 40 ? '20 - 40 BBY' : `${birthYearFilter.min} - ${birthYearFilter.max} BBY`) }}
    </button>
    <ul class="dropdown-menu" aria-labelledby="dropdownBirthYear">
      <li>
        <a class="dropdown-item" href="#" @click="setBirthYearFilter(0, 1000)">All Years</a>
      </li>
      <li>
        <a class="dropdown-item" href="#" @click="setBirthYearFilter(20, 40)">20 - 40 BBY</a>
      </li>
    </ul>
      </div>
    </div>
  
      <div v-if="loading" class="mt-3">
        <div class="spinner-border text-warning"></div>
        <p>Loading...</p>
      </div>
  
      <p v-if="error" class="text-danger mt-3">{{ error }}</p>
  
      <div class="row mt-4">
        <div v-for="char in filteredCharacters" :key="char.name" class="col-md-4 mb-4">
          <div class="card bg-dark text-light border-warning">
            <div class="card-body">
              <h5 class="card-title text-warning">{{ char.name }}</h5>
              <p class="card-text">
                <strong>Gender:</strong> {{ char.gender }} <br>
                <strong>Homeworld:</strong> {{ char.homeworldName }} <br />
                <strong>Birth Year:</strong> {{ char.birth_year }} <br />
                <strong>Height:</strong> {{ char.height }} cm <br />
                <strong>Mass:</strong> {{ char.mass }} kg <br />
                <strong>Films:</strong> {{ char.films.length }} <br />
                <strong>Created:</strong> {{ new Date(char.created).toLocaleDateString() }}
              </p>
            </div>
          </div>
        </div>
      </div>

      <p v-if="filteredCharacters.length === 0 && !loading" class="text-warning mt-3">No characters found.</p>
        
      <Pagination 
      :currentPage="currentPage" 
      :totalPages="totalPages" 
      @update:currentPage="changePage"
    />
    </div>
  </template>
  
  <script>
  import { useCharacterStore } from '../stores/characterStore';
  import { storeToRefs } from 'pinia';
  import { onMounted } from 'vue';
  import Pagination from './UI/Pagination.vue';
  
  export default {
    components: {
      Pagination
    },

    setup() {
     const characterStore = useCharacterStore();
     const { characters, loading, error, filteredCharacters, currentPage, totalPages, genderFilter, genderOptions, birthYearFilter } = storeToRefs(characterStore);
     const { fetchCharacters, setGenderFilter, setBirthYearFilter, setPage } = characterStore;

      onMounted(() => {
        fetchCharacters();
      });

      function changePage(page) {
      setPage(page);
    }
  
      return { characters, loading, error, filteredCharacters, setGenderFilter, setBirthYearFilter, currentPage, totalPages, changePage, genderFilter, genderOptions, birthYearFilter };
    },
  };
  </script>
  
  <style scoped>
  .card-img-top {
    height: 200px;
    object-fit: cover;
  }
  </style>
  