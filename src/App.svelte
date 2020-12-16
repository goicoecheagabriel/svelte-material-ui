<script>
	import Button from '@smui/button';
	import Textfield, {Input, Textarea} from '@smui/textfield';
	import Icon from '@smui/textfield/icon/index';
  	import HelperText from '@smui/textfield/helper-text/index';
	export let name;

	let valueClickable = '';
  	let dirtyClickable = false;
	  let invalidClickable = false;
	  
	function clickableHandler() {
		alert(`Sending to ${valueClickable}!`);
		valueClickable = '';
		dirtyClickable = false;
	}
</script>

<main>
	<h1>Hello {name}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
	<Button on:click={()=>alert('Fantastic !!')}>svelte-material-ui</Button>
</main>

<div>
    <div class="margins">
      <!--
        Notice that when you bind to `invalid`, but you only want to monitor it
        instead of updating it yourself, you also should include
        `updateInvalid`.
      -->
      <Textfield type="email" withTrailingIcon={valueClickable !== ''} bind:dirty={dirtyClickable} bind:invalid={invalidClickable} updateInvalid bind:value={valueClickable} label="To" style="min-width: 250px;" input$autocomplete="email">
        {#if valueClickable !== '' && dirtyClickable && !invalidClickable}
          <Icon class="material-icons" role="button" on:click={clickableHandler}>send</Icon>
        {/if}
      </Textfield>
      <HelperText validationMsg>That's not a valid email address.</HelperText>
    </div>

    <pre class="status">Dirty: {dirtyClickable}, Invalid: {invalidClickable}</pre>
  </div>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: #ff3e00;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}



	.margins {
    margin: 18px 0 24px;
  }
  
  * :global(.shaped) {
    border-radius: 16px 16px 0 0;
  }
  * :global(.shaped-outlined .mdc-text-field__input) {
    padding-left: 32px;
    padding-right: 32px;
  }
  * :global(.shaped-outlined .mdc-notched-outline .mdc-notched-outline__leading) {
    border-radius: 28px 0 0 28px;
    width: 28px;
  }
  * :global(.shaped-outlined .mdc-notched-outline .mdc-notched-outline__trailing) {
    border-radius: 0 28px 28px 0;
  }
  * :global(.shaped-outlined .mdc-notched-outline .mdc-notched-outline__notch) {
    max-width: calc(100% - 28px * 2);
  }
  * :global(.shaped-outlined + .mdc-text-field-helper-line) {
    padding-left: 32px;
    padding-right: 28px;
  }





	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}
</style>