<script>
	import  CountryRandom from './CountryRandom.svelte';
	import Notes from './CountryNotes.svelte';
	import Button from './ButtonRandom.svelte';
	import {onMount, onDestroy, beforeUpdate, afterUpdate} from 'svelte';
	import {fade, fly} from 'svelte/transition';

	let mouse = {"x": 0, "y": 0}
	let emojis = ['🇮🇩', '🇯🇵', '🇰🇷', '🇺🇸', '🇩🇪', '🇬🇧', '🇦🇺', '🇧🇷', '🇧🇳', '🇫🇷', '🇲🇾', '🇸🇦', '🇸🇬']; 
	let names = ['Indonesia', 'Japan', 'South Korean', 'United States', 'Germany', 'United Kingdom', 'Australia', 'Brazil', 'Brunei Darussalam', 'France', 'Malaysia', 'Saudi Arabia', 'Singapore'];
	let country = {
		emoji: '🌎',
		name: '🌎'
	};
	let isLoaded = false;
	function emojiRandom(){
		let number = Math.floor(Math.random() * emojis.length);
		let dataCountry = {
			flag: emojis[number],
			country: names[number]
		}
		return dataCountry;
	}
	function handleEmojiRandom(){
		let pickCountry = emojiRandom();
		let countryData = {
			emoji: pickCountry.flag,
			name: pickCountry.country
		}
		country = countryData;
	}
	function handleMouseMove(event){
		mouse.x = event.clientX;
		mouse.y = event.clientY;
	}
	function handleToggle(){
		isLoaded = !isLoaded;
	}
	onMount, onDestroy, beforeUpdate, afterUpdate(function(){
		console.log("Lifecycle Function Worked");
	})
</script>
<style>
</style>
<div on:mousemove={handleMouseMove}>
	<h1>Emoji Randomizer</h1>
	<p>Available Emoji : 
		{#each emojis as emoji}
		<span>{emoji} - </span>
		{/each}
	</p>
	{#if isLoaded}
		<div in:fly={{y: 200, duration: 1000}}>
			<CountryRandom {country}/>
			<Notes />
			<Button on:click={handleEmojiRandom} title={"🎲 Random Now"}/>
		</div>
	{/if}
	<Button on:click={handleToggle} title={"✅ Toggle"}/>
	<p>The point of mouse is {mouse.x} x {mouse.y}</p>
</div>