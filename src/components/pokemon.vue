<template>
	<div class="pokebox" v-bind:id=pokedex.id>
		<h2 class="pokename">{{pokedex.nome}}</h2>
		<img class="pokeimg" v-bind:src=pokedex.img alt="">
	</div>
</template>

<script>
export default {
	props: {
		pokedex: {type: Object, required: true}
	}
}
</script>

<style>
.pokename {
	font-weight: bold;
	font-size: 16px;
	margin-top: 15px;
}
.pokebox {
	border: 2px solid black;
	border-radius: 5px;
	background: rgb(233, 233, 233);
	margin: 5px;
	padding: 0;
	position: relative;
	display: inline-block;
	width: 150px;
	height: 160px;	
}

</style>