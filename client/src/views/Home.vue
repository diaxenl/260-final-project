<template>
<div class="home">
  <section class="character-lsit">
    <div class="list" v-for="character in characters" :key="character.id">
      <h2>{{character.name}}</h2>
      <h2>{{character.profession}}</h2>
    </div>
  </section>


</div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios';
export default {
  name: 'Home',
  data() {
    return {
     characters: [],
    }
  },
  created() {
    this.getCharacters();
  },
  methods: {
    async getCharacters() {
      try {
        let response = await axios.get("/api/character");
        this.characters = response.data;
        return true;
      } catch (error) {
        console.log(error);
      }
    },
  }
}
</script>


<style scoped>
.home {
  display: flex;
  justify-content: center;
}

.list {
  padding: 10px;;
  margin: 5px;
  border: 5px solid black;
}


/* Masonry on large screens */
@media only screen and (min-width: 1024px) {
  .image-gallery {
    column-count: 4;
  }
}

/* Masonry on medium-sized screens */
@media only screen and (max-width: 1023px) and (min-width: 768px) {
  .image-gallery {
    column-count: 3;
  }
}

/* Masonry on small screens */
@media only screen and (max-width: 767px) and (min-width: 540px) {
  .image-gallery {
    column-count: 2;
  }
}
</style>