<script>
	import DocumentLink from '$lib/DocumentLink.svelte';
	import Hover from '$lib/Hover.svelte';
	import HintSet from '$lib/HintSet.svelte';
</script>

<section>
	<h5>DocumentLink</h5>
	<DocumentLink
		value={{
			range: {
				end: {
					character: 19,
					line: 1
				},
				start: {
					character: 9,
					line: 1
				}
			},
			target: 'file:///usr/include/stdlib.h'
		}}
	/>
</section>

<section>
	<h5>Hover - plaintext</h5>
	<Hover
		value={{
			contents: {
				kind: 'plaintext',
				value: 'stdlib.h\n\n/usr/include/stdlib.h\n\nprovides exit'
			}
		}}
	/>
</section>
<section>
	<h5>Hover - plaintext</h5>
	<Hover
		value={{
			contents: {
				kind: 'plaintext',
				value:
					"function exit\nprovided by <stdlib.h>\n\n→ void\nParameters:\n- int __status\nCall all functions registered with `atexit' and `on_exit',\nin the reverse of the order in which they were registered,\nperform stdio cleanup, and terminate program execution with STATUS.\n\nextern void exit(int __status)"
			},
			range: {
				end: {
					character: 6,
					line: 5
				},
				start: {
					character: 2,
					line: 5
				}
			}
		}}
	/>
</section>
<section>
	<h5>Hover - markdown</h5>
	<Hover
		value={{
			contents: {
				kind: 'markdown',
				value:
					"### function `exit`  \nprovided by `<stdlib.h>`  \n\n---\n→ `void`  \nParameters:  \n- `int __status`\n\nCall all functions registered with \\`atexit' and \\`on_exit',  \nin the reverse of the order in which they were registered,  \nperform stdio cleanup, and terminate program execution with STATUS.  \n\n---\n```cpp\nextern void exit(int __status)\n```"
			},
			range: {
				end: {
					character: 6,
					line: 5
				},
				start: {
					character: 2,
					line: 5
				}
			}
		}}
	/>
</section>

<section>
	<h5>HintSet</h5>
	<HintSet
		hints={[
			[
				'DocumentLink',
				{
					range: {
						end: {
							character: 19,
							line: 1
						},
						start: {
							character: 9,
							line: 1
						}
					},
					target: 'file:///usr/include/stdlib.h'
				}
			],
			[
				'Hover',
				{
					contents: {
						kind: 'plaintext',
						value: 'stdlib.h\n\n/usr/include/stdlib.h\n\nprovides exit'
					}
				}
			]
		]}
	/>
</section>

<section>
	<h5>HintSet</h5>
	<HintSet
		hints={[
			[
				'DocumentLink',
				{
					range: {
						end: {
							character: 19,
							line: 1
						},
						start: {
							character: 9,
							line: 1
						}
					},
					target: 'file:///usr/include/stdlib.h'
				}
			],
			[
				'Hover',
				{
					contents: {
						kind: 'markdown',
						value: '### function `main`  \n\n---\n→ `int`  \n\n---\n```cpp\nint main()\n```'
					},
					range: {
						end: {
							character: 8,
							line: 3
						},
						start: {
							character: 4,
							line: 3
						}
					}
				}
			]
		]}
	/>
</section>

<style>
	:global(section, .HintSet > div) {
		border: 1px solid black;
	}
</style>
