<template>
  <div v-show="movies">
    <div class="movies__sorting">
      <input
        type="radio"
        name="radio"
        id="sort-1"
        @click="sortAlphabetically()"
      />
      <label for="sort-1"
        >отсортировать блоки по заголовку согласно алфавитного порядка</label
      >
      <br />
      <input type="radio" name="radio" id="sort-2" @click="sortAllLeft()" />
      <label for="sort-2"
        >вывести все блоки в формате “изображения - слева, текст -
        справа”</label
      >
      <br />
      <input type="radio" name="radio" id="sort-3" @click="sortChessWay()" />
      <label for="sort-3"
        >вывести все блоки в формате “изображения - слева, текст - справа” и
        наоборот в шахматном порядке</label
      >
    </div>
    <div v-for="(movie, index) in movies" :key="index">
      <div
        class="movies"
        :class="{
          'movies-odd-item': index === 0 || index === 2,
          'movies-even-item': index === 1 || index === 3 || index === 5,
        }"
      >
        <div class="movies__img">
          <img
            :src="'https://image.tmdb.org/t/p/w500' + movie.poster_path"
            alt=""
          />
        </div>
        <div class="movies__info">
          <h1>{{ movie.original_title }}</h1>
          <p>{{ movie.overview }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      movies: [],
    };
  },

  methods: {
    async getMovies() {
      const url =
        "https://api.themoviedb.org/3/discover/movie?api_key=3685d3eb8695f087227e0ee980f3ae4d&language=en-US&sort_by=popularity.desc&include_adult=false&include_video=false&page=1";
      try {
        const response = await fetch(url);
        const data = await response.json();
        this.movies = data.results;
        this.movies.length = 5;
        console.log(data);
        console.log(this.movies);
      } catch (error) {
        console.log("Rejected", error);
      }
    },

    sortAlphabetically() {
      const list = this.movies.sort((a, b) => {
        if (a.original_title < b.original_title) {
          return -1;
        }
        if (a.original_title > b.original_title) {
          return 1;
        }
        return 0;
      });
      this.movies = list;
    },

    sortAllLeft() {
      const evenItems = document.querySelectorAll(".movies-even-item");
      evenItems.forEach((el) => el.classList.remove("movies-even-item"));
      evenItems.forEach((el) => el.classList.add("movies-even-item-temp"));
    },

    sortChessWay() {
      const evenItems = document.querySelectorAll(".movies-even-item-temp");
      evenItems.forEach((el) => el.classList.add("movies-even-item"));
      evenItems.forEach((el) => el.classList.remove("movies-even-item-temp"));
    },
  },

  mounted() {
    this.getMovies();
  },
};
</script>

<style lang="scss">
.movies {
  width: 75%;
  height: 400px;
  background: rgb(199, 199, 199);
  padding: 20px;
  margin: 20px auto;
  display: flex;

  &__img {
    height: 100%;
    width: 25%;
    overflow: hidden;
    display: flex;
    justify-content: center;

    img {
      height: 100%;
    }
  }

  &__info {
    width: 75%;
    padding: 20px;
    display: flex;
    flex-direction: column;
    justify-content: center;

    h1 {
      margin: 10px 0;
    }
  }

  &-even-item .movies__img {
    order: 2;
  }

  &__sorting {
    width: 60%;
    margin: 20px auto;

    input {
      margin: 10px 10px 20px 0;
    }
  }
}
</style>
