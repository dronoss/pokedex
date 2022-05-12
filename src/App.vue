<template>
  <div id="app">
    <div class="main">
      <input v-model="pesquisa" type="search" class="search_toolbar" placeholder="Search">
      <div class="escopo">
        <div class="card" v-for="pokemon in filtar_pokemons" :key="pokemon">
          <div @click="show_pokemon(get_id(pokemon))">
            <img :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${get_id(pokemon)}.png`" :alt="pokemon.name">
            <div class="textCard">
                <div class="nome_pokemon">
                  <p>{{get_maiuscula(pokemon)}}</p>
                </div>
                <div class="num_pokedex">
                  <p>#{{get_id(pokemon)}}</p>
                </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="flex" @click="show_grid_pokemon()">
        <article class="card_pokemon">
          <img src="../src/assets/bg-pattern-card.svg" alt="image header card" class="card-header">
          <div class="card-body">
            <img :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${img_card}.png`" alt="img-pokemon">
            <h1 class="card-body-title" id="nome_p">
              {{Nome_nome}}
              <span id="num_p">id</span>
            </h1>
          </div>
            <div class="card-footer">
              <div class="card-footer-social">
                <h3>grass</h3>
                <p></p>
              </div>
              <div class="card-footer-social">
                <h3>7</h3>
                <p>Height</p>
              </div>
              <div class="card-footer-social">
                <h3>69</h3>
                <p>Weight</p>
              </div>
            </div>
        </article>
    </div>    
  </div>
</template>

<script>
import axios from "axios"

export default {
  name: 'App',

  components: {},

  data()  {
    return{
      pokemons: [],
      pesquisa: "",
      id_pokemon: "",
    };
  },

  mounted() {
    axios
    .get("https://pokeapi.co/api/v2/pokemon?limit=151")
    .then((response) => {
      this.pokemons = response.data.results;
    })
  
  },

  methods: {
    get_maiuscula(pokemon){
      return pokemon.name.charAt(0).toUpperCase() + pokemon.name.slice(1);
    },

    get_id(pokemon) {
      return Number (pokemon.url.split("/")[6]);
    },

    show_pokemon() {

      /*axios.get(`https://pokeapi.co/api/v2/pokemon?${id}`).then((response) => {
        this.selected_pokemon = response.data
      })
           
      const popup_body = document.querySelector('.main')
      const popup_card = document.querySelector('.flex')
      popup_card.style.display = 'flex'
      popup_body.style.display = 'none'*/
      

    },

    show_grid_pokemon() {
      
      const popup_body = document.querySelector('.main')
      const popup_card = document.querySelector('.flex')
      popup_card.style.display = 'none'
      popup_body.style.display = 'grid'

    },
  },

  computed: {
    filtar_pokemons() {
      return this.pokemons.filter((item) => {
        return item.name.includes(this.pesquisa);
      })
    }
  }

}
</script>

<style>

body{
    background: linear-gradient(
    to bottom right, rgb(234, 255, 213), rgb(83, 241, 44)
  )
  no-repeat center center fixed !important;
  background-position: center;
  -moz-background-size: cover;
  -webkit-background-size: cover;
  background-size: cover !important;
}

main{
  display: flex;
}


.escopo{
  text-align: center;  
  overflow: hidden;
  display: grid;
  grid-template-columns: repeat(6,16.67%);
}

.search_toolbar {
  text-align: left;
  border-top-color: rgba(195, 243, 147,0.0);
  border-left-color: rgba(195, 243, 147,0.0);
  border-right-color: rgba(195, 243, 147,0.0);
  border-bottom-color: black;
  height: 50px;
  width: 99.3%;
  overflow: hidden;
  margin-left: 8px;
  margin-bottom: 8px;
  background: linear-gradient(to bottom right, rgb(234, 255, 213), rgb(83, 241, 44))
  no-repeat center center fixed !important;
  background-position: center;
  -moz-background-size: cover;
  -webkit-background-size: cover;
  background-size: cover !important;

}

.textCard{
  display: grid;
  grid-template-columns: repeat(2,50%);
  overflow: hidden;
  
}

.nome_pokemon{
  text-align: left;
  margin-left: 8px;
  width: 125%;
}

.num_pokedex{

  margin-right: 8px;
  text-align: right;

}


.card{
  margin: 5px;
  background-color: aliceblue;
}

/*Parte do Pop UP*/

  .flex {
    display: -webkit-box;
    display: -ms-flexbox;
    display: none;
    -webkit-box-pack: center;
        -ms-flex-pack: center;
            justify-content: center;
    -webkit-box-align: center;
        -ms-flex-align: center;
            align-items: center;
    height: 100vh;
  }
  
  .card_pokemon {
    background-color: white;
    width: 326px;
    border-radius: 16px;
    overflow: hidden;
    -webkit-box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
            box-shadow: 2px 2px 4px rgba(0, 0, 0, 0.7);
  }
  
  .card-header {
    width: 100%;
    display: block;
  }
  
  .card-body {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-orient: vertical;
    -webkit-box-direction: normal;
        -ms-flex-direction: column;
            flex-direction: column;
    -webkit-box-align: center;
        -ms-flex-align: center;
            align-items: center;
    border-bottom: 1px solid rgba(153, 153, 153, 0.383);
  }
  
  .card-body-img {
    border: 5px solid white;
    border-radius: 50%;
    margin-top: calc(-48px - 5px);
    background-color: white;
  }
  
  .card-body-title {
    margin-top: 2rem;
    font-size: 1.8rem;
  }
  
  .card-body-title span {
    color: var(--dark-gray);
    font-weight: 400;
  }
  
  
  .card-footer {
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -ms-flex-pack: distribute;
        justify-content: space-around;
  }
  
  .card-footer-social {
    text-align: center;
    margin-top: 2rem;
    margin-bottom: 2rem;
  }
  
  .card-footer-social p {
    letter-spacing: 1px;
  }
</style>
