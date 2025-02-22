<script lang="ts">
	import DocsShell from '$docs/layouts/DocsShell/DocsShell.svelte';
	import { DocsFeature, type DocsShellSettings } from '$docs/layouts/DocsShell/types';

	import CodeBlock from '$lib/utilities/CodeBlock/CodeBlock.svelte';
	import { clipboard } from '$lib/actions/Clipboard/clipboard';

	// Docs Shell
	const settings: DocsShellSettings = {
		feature: DocsFeature.Action,
		name: 'Clipboard',
		description: 'Allows you to quickly copy data to the clipboard.',
		imports: ['clipboard'],
		source: 'actions/Clipboard',
		parameters: [
			['<code>element</code>', 'string', '-', '-', `HTML element's <em>data-clipboard</em> ID value.`],
			['<code>input</code>', 'string', '-', '-', `Input element's <em>data-clipboard</em> ID value.`]
		]
	};
</script>

<DocsShell {settings}>
	<!-- Slot: Sandbox -->
	<svelte:fragment slot="sandbox">
		<section class="grid grid-cols-1 md:grid-cols-2 gap-4">
			<!-- Element -->
			<div class="card variant-glass p-4 space-y-4">
				<div class="bg-surface-200-700-token p-4 rounded-container-token h-20" data-clipboard="exampleElement" contenteditable>
					This <em>div</em> is set to 'contenteditable'. Make changes then tap copy.
				</div>
				<button use:clipboard={{ element: 'exampleElement' }} class="btn variant-filled-secondary">Copy Inner HTML</button>
			</div>
			<!-- Input -->
			<div class="card variant-glass p-4 space-y-4">
				<textarea class="textarea h-20" data-clipboard="exampleInput">Make changes to this textarea and then tap copy.</textarea>
				<button use:clipboard={{ input: 'exampleInput' }} class="btn variant-filled-secondary">Copy Input Value</button>
			</div>
		</section>
	</svelte:fragment>

	<!-- Slot: Usage -->
	<svelte:fragment slot="usage">
		<div class="space-y-4">
			<p>If your data is available as a primitive data type (string, integer, etc), you can provide it directly to the action.</p>
			<CodeBlock language="ts" code={`const exampleData: string = 'Your data here.';`} />
			<CodeBlock language="html" code={`<button use:clipboard={exampleData}>Copy</button>`} />
		</div>
		<!-- Element -->
		<div class="space-y-4">
			<h2>Copying HTML Contents</h2>
			<p>
				To copy the <em>innerHTML</em> for an element, set a <code>data-clipboard</code> data attribute on your target, then provide
				<code>element</code> reference to the action.
			</p>
			<CodeBlock
				language="html"
				code={`
<!-- Source -->
<div data-clipboard="exampleElement">(contents)</div>

<!-- Trigger -->
<button use:clipboard={{ element: 'exampleElement' }}>Copy</button>
			`}
			/>
		</div>
		<!-- Inputs -->
		<div class="space-y-4">
			<h2>Copying Input Values</h2>
			<p>
				To copy a form input <em>value</em>, set a <code>data-clipboard</code> data attribute on your target, then provide
				<code>input</code> reference to the action.
			</p>
			<CodeBlock
				language="html"
				code={`
<!-- Source -->
<input type="text" value="(contents)" data-clipboard="exampleInput"></input>

<!-- Trigger -->
<button use:clipboard={{ input: 'exampleInput' }}>Copy</button>
			`}
			/>
		</div>
	</svelte:fragment>
</DocsShell>
