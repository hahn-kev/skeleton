<script lang="ts">
	import { fade } from 'svelte/transition';

	import DocsShell from '$docs/layouts/DocsShell/DocsShell.svelte';
	import { DocsFeature, type DocsShellSettings } from '$docs/layouts/DocsShell/types';

	import CodeBlock from '$lib/utilities/CodeBlock/CodeBlock.svelte';

	// Docs Shell
	const settings: DocsShellSettings = {
		feature: DocsFeature.Element,
		name: 'Alerts',
		description: 'Display customizable alerts to garner attention and provide critical actions.',
		stylesheetIncludes: ['all', 'elements'],
		stylesheets: ['elements/alerts'],
		source: 'styles/elements/alerts.css',
		classes: [
			['<code>alert</code>', '', 'Provide basic alert styles to a block element.'],
			['<code>alert-message</code>', '', 'The message body styles, contains a title and message.'],
			['<code>alert-actions</code>', '', 'The message action styles, contains buttons.']
		]
	};

	// Local
	let visible = true;
	let message =
		'Lorem ipsum dolor sit, amet consectetur adipisicing elit. Eligendi, cupiditate eveniet in neque magnam quos ad cumque quae numquam voluptatum magni atque vitae dolore voluptatibus.';

	// Functions
	function triggerAction(): void {
		alert('Action button was triggered!');
	}
	function toggleVisible(): void {
		visible = !visible;
	}
</script>

<DocsShell {settings}>
	<!-- Slot: Sandbox -->
	<svelte:fragment slot="sandbox">
		<div class="space-y-4">
			<!-- Default -->
			<div class="space-y-4">
				<!-- Primary -->
				{#if visible}
					<aside class="alert variant-ghost" transition:fade|local={{ duration: 200 }}>
						<i class="fa-solid fa-triangle-exclamation text-4xl" />
						<div class="alert-message" data-toc-ignore>
							<h3 data-toc-ignore>Warning</h3>
							<p>{message}</p>
						</div>
						<div class="alert-actions">
							<button class="btn variant-filled" on:click={triggerAction}>Action</button>
							<button class="btn-icon variant-ghost" on:click={toggleVisible}>
								<i class="fa-solid fa-xmark" />
							</button>
						</div>
					</aside>
				{:else}
					<div class="text-center">
						<button class="btn variant-filled-secondary" on:click={toggleVisible}>Toggle {!visible ? 'On' : 'Off'}</button>
					</div>
				{/if}
				<!-- Success / Error -->
				<div class="grid grid-cols-1 lg:grid-cols-2 gap-4">
					<aside class="alert variant-ghost-primary">
						<h3 class="alert-message" data-toc-ignore>Primary</h3>
						<button class="btn variant-filled-primary" on:click={triggerAction}>Action</button>
					</aside>
					<aside class="alert variant-ghost-secondary">
						<h3 class="alert-message" data-toc-ignore>Secondary</h3>
						<button class="btn variant-filled-secondary" on:click={triggerAction}>Action</button>
					</aside>
					<aside class="alert variant-ghost-tertiary">
						<h3 class="alert-message" data-toc-ignore>Tertiary</h3>
						<button class="btn variant-filled-tertiary" on:click={triggerAction}>Action</button>
					</aside>
					<aside class="alert variant-ghost-warning">
						<h3 class="alert-message" data-toc-ignore>Warning</h3>
						<button class="btn variant-filled-warning" on:click={triggerAction}>Action</button>
					</aside>
					<aside class="alert variant-ghost-success">
						<i class="fa-solid fa-circle-check text-2xl" />
						<h3 class="alert-message" data-toc-ignore>Success</h3>
						<button class="btn variant-filled-success" on:click={triggerAction}>Action</button>
					</aside>
					<aside class="alert variant-ghost-error">
						<i class="fa-solid fa-circle-xmark text-2xl" />
						<h3 class="alert-message" data-toc-ignore>Error</h3>
						<button class="btn variant-filled-error" on:click={triggerAction}>Action</button>
					</aside>
				</div>
			</div>
		</div>
	</svelte:fragment>

	<!-- Slot: Usage -->
	<svelte:fragment slot="usage">
		<section class="space-y-4">
			<p>Create an element with the <code>.alert</code> class. Wrap in a Svelte <em>if</em> statement to handle the visible state.</p>
			<CodeBlock language="ts" code={`let visible: boolean = true;`} />
			<CodeBlock
				language="html"
				code={`
{#if visible}
    <aside class="alert variant-ghost">
        <!-- Icon -->
        <div>(icon)</div>
        <!-- Message -->
        <div class="alert-message">
            <h3>(title)</h3>
            <p>{message}</p>
        </div>
        <!-- Actions -->
        <div class="alert-actions">(buttons)</div>
    </aside>
{/if}
            `}
			/>
			<h3>Message Content</h3>
			<p>Use the <code>.alert-message</code> to create a vertical set of text information that fills the available width of the alert.</p>
			<CodeBlock language="html" code={`<div class="alert-message">\n\t<h3>(title)</h3>\n\t<p>{message}</p>\n</div>`} />
			<CodeBlock language="html" code={`<h3 class="alert-message">(title)</h3>`} />
			<h3>Action Buttons</h3>
			<p>Use the <code>.alert-actions</code> to create a trailing area to house interactive action buttons.</p>
			<CodeBlock language="html" code={`<div class="alert-actions">(buttons)</div>`} />
		</section>
		<section class="space-y-4">
			<h2>Variants</h2>
			<p>Supports all standard variant styles via <code>.variant-[style]-[color]</code>.</p>
			<CodeBlock language="html" code={`<div class="alert variant-ghost-warning">...</div>`} />
		</section>
		<section class="space-y-4">
			<h2>Adding Animations</h2>
			<!-- prettier-ignore -->
			<p><a href="https://svelte.dev/tutorial/transition" target="_blank" rel="noreferrer">Svelte Transitions</a> can provide smooth transitions when the alert state changes.</p>
			<CodeBlock language="html" code={`<aside class="alert" transition:fade|local={{ duration: 200 }}>...</div>`} />
		</section>
	</svelte:fragment>
</DocsShell>
