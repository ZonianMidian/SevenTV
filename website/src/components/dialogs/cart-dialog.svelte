<script lang="ts">
	import { priceFormat } from "$/lib/utils";
	import { Trash, Star, User } from "phosphor-svelte";
	import Button from "../input/button.svelte";
	import Checkbox from "../input/checkbox.svelte";
	import Dialog, { DialogMode } from "./dialog.svelte";
	import Select from "../input/select.svelte";
	import TextInput from "../input/text-input.svelte";

	export let mode: DialogMode = DialogMode.Hidden;

	let gift = false;
</script>

<Dialog width={35} bind:mode>
	<form class="layout">
		<h1>Your Cart</h1>
		<hr />
		<table class="items">
			<thead>
				<tr>
					<th>Item</th>
					<th class="hide-on-mobile">Duration</th>
					<th>Price</th>
					<th></th>
				</tr>
			</thead>
			<tbody>
				{#each Array(3) as _, i}
					<tr>
						<td class="name">
							<div class="center">
								<Star color="var(--subscriber)" />
								Tier 1 Subscription
							</div>
						</td>
						<td class="duration hide-on-mobile">
							<Select
								options={[
									{ value: "1", label: "1 Month" },
									{ value: "3", label: "3 Months" },
									{ value: "12", label: "1 Year" },
								]}
							/>
						</td>
						<td class="price">{priceFormat.format((i + 1) * 7.96)}</td>
						<td class="actions">
							<Button secondary>
								<Trash slot="icon" />
							</Button>
						</td>
					</tr>
				{/each}
			</tbody>
		</table>
		<table class="items">
			<thead>
				<tr>
					<th class="hide-on-mobile">Preview</th>
					<th>Item</th>
					<th>Price</th>
					<th></th>
				</tr>
			</thead>
			<tbody>
				{#each Array(3) as _, i}
					<tr class="hide-on-mobile">
						<td>
							<div class="preview">
								<div class="placeholder"></div>
								<div class="placeholder"></div>
								<div class="placeholder"></div>
							</div>
						</td>
						<td class="name">Christmas Bundle</td>
						<td class="price">{priceFormat.format((i + 1) * 7.96)}</td>
						<td class="actions">
							<Button secondary>
								<Trash slot="icon" />
							</Button>
						</td>
					</tr>
					<tr class="hide-on-desktop">
						<td class="name">Christmas Bundle</td>
						<td class="price">{priceFormat.format((i + 1) * 7.96)}</td>
						<td class="actions">
							<Button secondary>
								<Trash slot="icon" />
							</Button>
						</td>
					</tr>
				{/each}
			</tbody>
		</table>
		<Checkbox bind:value={gift}>Purchase as a gift</Checkbox>
		{#if gift}
			<TextInput placeholder="Search a user">
				<User slot="icon" />
			</TextInput>
		{/if}
		<div class="footer">
			<div class="total">
				<span>Total</span>
				<span>{priceFormat.format(7.96)}</span>
			</div>
			<div class="buttons">
				<Button secondary on:click={() => (mode = DialogMode.Hidden)}>Cancel</Button>
				<Button primary submit>Proceed</Button>
			</div>
		</div>
	</form>
</Dialog>

<style lang="scss">
	.layout {
		padding: 1rem;

		display: flex;
		flex-direction: column;
		gap: 0.5rem;
	}

	h1 {
		font-size: 1rem;
		font-weight: 600;
		margin-block: 0.4rem;
	}

	.items {
		width: 100%;

		border-spacing: 0 0.5rem;
		border-collapse: separate;
		border: none;

		th {
			font-size: 0.75rem;
			color: var(--text-light);
			font-weight: 400;
			text-align: left;

			padding-inline: 0.5rem;
		}

		td {
			padding: 0.5rem;
			background-color: var(--bg-light);

			&:first-child {
				padding-left: 0.5rem;
				border-radius: 0.5rem 0 0 0.5rem;
			}

			&:last-child {
				padding-right: 0.5rem;
				border-radius: 0 0.5rem 0.5rem 0;
			}
		}

		.preview {
			display: flex;
			align-items: center;
			gap: 0.5rem;
		}

		.placeholder {
			width: 1.5rem;
			height: 1.5rem;
			background-color: var(--secondary);
			border-radius: 50%;
		}

		.name {
			font-size: 0.875rem;
			font-weight: 500;

			overflow: hidden;
			text-overflow: ellipsis;
			white-space: nowrap;
		}

		.center {
			display: flex;
			align-items: center;
			gap: 0.5rem;
		}

		.duration {
			// Shrink column
			width: 1px;
		}

		.price {
			font-size: 0.875rem;
			font-weight: 600;
		}

		.actions {
			// Shrink column
			width: 1px;
		}
	}

	.footer {
		margin-top: auto;
	}

	.total {
		display: flex;
		justify-content: space-between;
		font-size: 1.25rem;
		font-weight: 600;

		margin-top: 0.5rem;
		margin-bottom: 1rem;
	}

	.buttons {
		display: flex;
		justify-content: flex-end;
		gap: 0.5rem;
	}
</style>
