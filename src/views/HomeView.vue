<template>
  <div>
    <img class="logo" src="@/assets/logo.png" alt="">
    <!-- <h1>characters</h1> -->

    <div>
      <input
        type="text"
        v-model="search"
        placeholder="Search"
      >
    </div>

    <div class="content">
      <div
        class="content-characters" 
        v-for="(character, index) in data" :key="character.id"
        >
          <div class="character">
            <img :src="character.image" alt="">

            <div class="info-character">
              <h2>{{character.name}}</h2>
              <h4>{{character.gender}}</h4>
              <h4>Planeta: {{character.origin.name}}</h4>
            </div>
          </div>
      </div>
      <br>
      <br>
      <br>
    </div>

    <div>
      <button @click="getData(pagination.currentPage -1)">
        <span></span>
        Prev Page
      </button>

      <button>
        PAGE: {{pagination.currentPage}}
      </button>

      <button class="next" @click="getData(pagination.currentPage +1)">
        <span></span>
        Next Page
      </button>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
//import axios from 'axios'

export default {
  name: 'HomeView',
  components: {
  },

  data(){
    return {
      search: '',
      //characters: [],
      pagination: {
        currentPage: 1,
        nextPage: null,
        prevPage: null
      },
      data:[],
      url: 'https://rickandmortyapi.com/api/character'
    }
  },


  // mounted(){
    //console.log('verificando');
    //this.getAll();
  // },

  created(){
    this.getData()
  },

  methods: {
    // getAll(){
    //   //console.log('GET request');
    //   axios.get(`https://rickandmortyapi.com/api/character`)
    //     .then(resp => {
    //       //console.log(resp);
    //       (this.characters = resp.data.results)
    //     })
    //     .catch(error => {
    //       console.log(error);
    //     })
    // }

    async getData(pageNumber){
      const response = await fetch(this.url + '?page=' + (pageNumber || this.pagination.currentPage))
      const {results, info} = await response.json()
      this.data = results
      this.pagination = {
        currentPage: pageNumber ? pageNumber:1,
        nextPage: info.next,
        prevPage: info.prev
      }
    }
  },

  // computed: {
  //   filterSearch(){
  //     return this.characters.filter((character) => {
  //       return character.name.toLowCase().includes(this.search.toLowCase())
  //     })
  //   }
  // }
}
</script>

<style>
body{
  background-color: #081119;
}

/* CHARACTERS */
.content{
  display: grid;
  grid-template-columns: 1fr 1fr 1fr;
  grid-template-rows: 1fr;
  gap: 30px 30px;
  width: 80%;
  margin: 0 auto;
}

.content-characters{
  background-color: #002128;
  padding: 1rem;
  border-radius: 1rem;
}

.content-characters:hover{
  background-color: rgba(38, 184, 221, .2);
}

.character{
  display: flex;
  justify-content: center;
  align-items: center;
}

.info-character{
  display: table-column;
  justify-content: center;
  margin: 0 auto;
}

/* .prevPage svg{
  width: 20;
  height: 20;
  align-items: left;
  justify-content: center;
} */


/* BUTTON */
button{
  margin: 40px;
  position: relative;
  padding: 10px 20px;
  font-size: 15px;
  border: none;
  background: #002128;
  color: rgba(255, 255, 255, .4);
  text-transform: uppercase;
  letter-spacing: 1px;
  cursor: pointer;
  overflow: hidden;
  transition: .3s;
  width: 100px;
  height: 50px;
}

button span{
  /* margin: 35px; */
  position: absolute;
  width: 100%;
  height: 100px;
  border-radius: 50%;
  background: rgba(38, 184, 221, .2);
  top: -50%;
  right: 100%;
  transition: .3s;
}

button:hover span{
  right: -10%;
}

bottom:hover{
  color: #c0e4da;
  background: #033133;
  box-shadow: 0 5px 5px rgba(0, 0, 0, .7);
}

.next{
  margin: 0 40px;
  position: relative;
  padding: 10px;
  font-size: 15px;
  border: none;
  background: #002128;
  color: rgba(255, 255, 255, .4);
  text-transform: uppercase;
  letter-spacing: 1px;
  cursor: pointer;
  overflow: hidden;
  transition: .3s;
  width: 100px;
  height: 50px;
}

.next span{
  /* margin: 35px; */
  position: absolute;
  width: 100%;
  height: 100px;
  border-radius: 50%;
  background: rgba(38, 184, 221, .2);
  top: -50%;
  left: 100%;
  transition: .3s;
}

.next:hover span{
  left: -10%;
}

.next:hover{
  color: #c0e4da;
  background: #033133;
  box-shadow: 0 5px 5px rgba(0, 0, 0, .7);
}



/* IMAGE */
img.logo{
  width: 70%;
  text-align: center;
}

img{
  height: 50%;
  width: 50%;
  border-radius: 2rem;
}

/* TITTLE */
h1{
  color: #00ff97;
}

h2{
  font-weight: bold;
  font-size: 1.2rem;
  padding: 1rem;
  background: #00ff97;
  border-radius: 0.8rem;
  margin: 1rem;
}

h4{
  margin: 1rem;
  color: #ffffff;
  background: #8b8b8b;
  border-radius: 0.4rem;
  font-weight: inherit;
  padding: 0.2rem;
}


/* SEARCH */
input{
  text-align: center;
  background: #002128;
  outline: none;
  border: 0;
  width: 300px;
  margin: 1rem;
  padding: 1rem;
  color: #fff;
  font-weight: 700;
  border-radius: 1rem;
}

@media screen and (max-width:918px){
  .content{
    grid-template-columns: 1fr 1fr; 
  }

  .character{
    display: flex;
    align-items: center;
  }

  h2{
    font-size: 1rem;
  }
}

@media screen and (max-width: 540px){
  .content{
    width: 90%;
    grid-template-columns: 1fr;
  }

  .character{
    display: flex;
    align-items: center;
  }
}
</style>
