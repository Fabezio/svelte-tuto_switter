<script>
	export let name;
	import Message from './Message.svelte'
	let messages = []
	let isVisible = true
	function toggle() {
		isVisible = !isVisible
		console.log(isVisible)
	}
	function addMessage(event) {
		console.log(event.detail)
		messages = [event.detail, ...messages]
	}
	const options = {
		weekday: "long",
		year: "numeric",
		month: "long",
		day: "numeric", 
		hour12: true,
		hour: "numeric",
		minute: "2-digit",
		second: "2-digit"
	}
	const formatter = new Intl.DateTimeFormat("en-US", options)
</script>

<style>
	h1 {
		color: purple;
		text-align: center;
	}
		
	.author {
		font-weight: bold;
		margin-bottom: .5em;
	}
		
	.grey {
		color: grey;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
			margin: 0 auto;
			display: block;
		}
	}
</style>

<svelte:head>
	<title>Switter</title>
</svelte:head>

<main>
	<h1>{name.toUpperCase()}</h1>
	<!-- <p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p> -->
	<button on:click={toggle}>{isVisible ? 'hide' : 'show'}</button>
	<br>
	{#if isVisible}
		<Message on:message={addMessage}/>
	{/if}
	<div>
	<!-- <h3>Preview</h3>
	<p>
	{#if messages.length}
	{message}
	{:else}
	<span class='grey'>Nothin' to say now</span>
	{/if}
	</p> -->
	<h2>Messages: <small>{messages.length}</small></h2>
	{#each messages as message}
		{#if "John Doe"}
			<div class="grey" >{message.author} <small>said:</small></div>
		{:else}
			<div class="author" >{message.author} <small>said:</small></div>
		{/if}
		<q><em>{message.text}</em></q>
		<div>published: {formatter.format(message.date)}</div>
		<hr>
	{/each}
	</div>
</main>