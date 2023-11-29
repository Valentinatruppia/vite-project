
<script>
	import { fade } from 'svelte/transition';
    import menu from '/src/assets/menu.png'
	
	const fadeIn = {
		delay: 100,
		duration: 200
	}
	
	const fadeOut = {
		delay: 0,
		duration: 100
	}
	
	let isExpanded = false;
</script>

<nav class:expanded={isExpanded}>
	<button on:click={() => isExpanded = !isExpanded}>
		{#if isExpanded}
        <a>
            <img src="menu" >
        </a>
		{:else}
        <a>
            <img src="menu" >
        </a>
		{/if}
	</button>
	<ul>
		<li>🚀 {#if isExpanded}<span in:fade="{fadeIn}" out:fade="{fadeOut}">Home</span>{/if}</li>
		<li>⭐️ {#if isExpanded}<span in:fade="{fadeIn}" out:fade="{fadeOut}">Statistiche</span>{/if}</li>
		
	</ul>
	{#if isExpanded}
	<section in:fade="{fadeIn}" out:fade="{fadeOut}" >
		<hr />
		<ul>
			<h3>
				Contatti:
			</h3>
			<li>valentinatruppia@gmail.com</li>
			<li>3665436483</li>
		</ul>
	</section>
	{/if}
</nav>

<style>
	nav {
		grid-area: nav;
		height: 100vw;
		background-color: #324754;
		color: #A2B7C4;
		transition: ease-out 200ms;
		width: 60px;
		overflow: hidden;
	}

	.expanded {
		transition: ease-out 200ms;
		width: 200px;
	}
	
	ul {
		list-style: none;
		padding: 20px;
		margin: 0;
	}
	
	li {
		width: 200px;
	}
	
	h3 {
		text-transform: uppercase;
		margin: 0;
		padding: 10px 0;
	}
	
	hr {
	  color: white;
		width: 80%;
	}
	
	button {
		border: none;
		background: none;
		color: #A2B7C4;
		text-transform: uppercase;
	}
</style>