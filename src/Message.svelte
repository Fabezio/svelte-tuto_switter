<script>
  import { createEventDispatcher} from 'svelte'
  const dispatch = createEventDispatcher()
  
  let message = "" 
  let author = ""
  const defaultAuthor = "John Doe"
  // import {messages} from './messages.js'
  // export {messages}
  const maxlength = 255

  $: nbChars = message.length
  $: disabled = message.length > maxlength ? true : false 

	function displayMessage() {
		const newMessage = {
			id: Date.now(),
      text: message,
      author: author || defaultAuthor,
      date: new Date()
		}
    // messages = [newMessage, ...messages] 
    console.log('newMessage', newMessage)
    dispatch('message', newMessage)
    author = ""
    message = ''
	}
</script>

<style>
.text {
  width: 33%;
}
.disabled {
  color: grey;
  background: #444;
}
.alert {
  color: orangered;
}
button {
  border-radius: 1em;
  padding:  .33em .66em;
  text-transform: uppercase;
  background: solid 1px white;
  margin-right: .5em;
}

</style>

<!-- <p>This is a component message</p> -->
<input class="text" type="text" bind:value={author}><br>
<textarea class="text"  rows="6" bind:value={message}></textarea>
<br>
<button disabled={disabled} on:click={displayMessage}>submit message</button>
{#if disabled}
<span class="alert" >(message too long, do not exceed {maxlength} chars)</span>
{:else}
<span class:alert={ nbChars > maxlength } >{nbChars}</span>
{/if}
	