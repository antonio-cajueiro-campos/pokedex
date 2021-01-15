<template>
  <div id="app">
    <header class="navbar">
      <section class="navbar-section">
        <h1 class="titulo">Pokédex - API de pokémons</h1>
      </section>
    </header>
    <div class="container">
      <!-- loop para cada um dos pokémons -->
      <Pokemon v-for="p in pokedex" :key="p.id" :pokedex="p"/>
    </div>
    <footer>
      <p>Antonio Carlos - <a href="https://github.com/antonio-cajueiro-campos">GitHub</a> | Powered By <a target="_blank" href="https://pokeapi.co/">pokeapi.co</a></p>
    </footer>
  </div>
</template>

<script>
//importando componente pokemon
import Pokemon from "./components/pokemon";

export default {
  name: 'App',
  components: { Pokemon },
  data() {
    return { pokedex: [] };
  },
  beforeMount(){
    //iniciando método assim que é carregado a aplicação
    this.carregarApi()
  },
  methods: {
    //carregar api com os dados no array pokedex
    carregarApi() {
      //array de promisses da api
      const pokePro =  [];

      // const/function pra reger uma template string diferente para cada pokémon
      const pokeUrl = id => `https://pokeapi.co/api/v2/pokemon/${id}`;

      //para cada um dos 150 pokémons da api, fazer um fetch com id diferente e dar push da promise no array de promises
      for (let i = 1; i <= 150; i++) {
        let pro = fetch(pokeUrl(i))
          .then(response => response.json())
        pokePro.push(pro)
      }

      // capturar todas as promises e então inserir cada uma delas resolvidas no array de objetos pokedex com os atributos id, nome e a sprite dele
      Promise.all(pokePro)
      .then(pokemons => {
        for (let i = 0; i < 150; i++) {
          this.pokedex.push({
            id: pokemons[i].id,
            nome: pokemons[i].name,
            img: pokemons[i].sprites.front_default
          })
        }
      })
    }
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0;
}
.titulo {
  color: white;
  font-family: cursive;
  margin: 15px auto;
  font-size: 28px;
}
header {
  background: rgb(206, 206, 206);
}
header {
  margin: 0;
  position: fixed;
  top: 0;
  height: 60px;
  width: 100%;
  z-index: 5;
}
header > h1 {
  margin: 0;
  color: white;
}
.container {
  margin-top: 100px;
}
footer {
  position: relative;
  bottom: 0;
  margin-top: 20px;
  background: rgb(199, 199, 199);
  width: 100%;
  height: 50px;

}
footer > p {
  font-weight: bold;
  margin: auto 20px;
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
