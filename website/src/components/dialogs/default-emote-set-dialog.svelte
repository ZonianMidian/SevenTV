<script lang="ts">
	import EmoteSetPicker from "../emote-set-picker.svelte";
	import Dialog, { DialogMode } from "./dialog.svelte";

	export let mode: DialogMode = DialogMode.Hidden;
</script>

<Dialog width={30} bind:mode>
	<div class="layout">
		<h1>Default Emote Set</h1>
		<hr />
		<EmoteSetPicker radioName="default-set" />
	</div>
</Dialog>

<style lang="scss">
	.layout {
		padding: 1rem;

		display: flex;
		flex-direction: column;
		gap: 1rem;
	}

	h1 {
		font-size: 1rem;
		font-weight: 600;
	}
</style>
