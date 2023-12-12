<script>
	import DocumentLink from './DocumentLink.svelte';
	import Hover from './Hover.svelte';

	/**
	 * @typedef DocumentLinkHintEntry
	 * @type {["DocumentLink", import("vscode-languageserver-types").DocumentLink]}
	 */

	/**
	 * @typedef HoverHintEntry
	 * @type {["Hover", import("vscode-languageserver-types").Hover]}
	 */

	/**
	 * @typedef HintEntry
	 * @type {DocumentLinkHintEntry | HoverHintEntry}
	 */

	/** @type {HintEntry[]} */
	export let hints = [];

	const map = /** @type {const} */ ({
		Hover: [Hover, 1],
		DocumentLink: [DocumentLink, 2]
	});

	/**
	 * @typedef SortedEntry
	 * @type {[typeof map[keyof typeof map], HintEntry]}
	 */

	$: sorted = hints
		.map((x) => /** @type {SortedEntry} */ ([map[x[0]], x]))
		.sort((a, b) => a[0][1] - b[0][1]);
</script>

<div class="HintSet">
	{#each sorted as entry (entry[1][0])}
		<svelte:component this={entry[0][0]} value={entry[1][1]} />
	{/each}
</div>
