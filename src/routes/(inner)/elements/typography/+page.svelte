<script lang="ts">
	import DocsShell from '$docs/layouts/DocsShell/DocsShell.svelte';
	import { DocsFeature, type DocsShellSettings } from '$docs/layouts/DocsShell/types';

	import CodeBlock from '$lib/utilities/CodeBlock/CodeBlock.svelte';

	// Docs Shell
	const settings: DocsShellSettings = {
		feature: DocsFeature.Element,
		name: 'Typography',
		description: 'Provides a variety of globally scoped typographic styles.',
		stylesheetIncludes: ['all', 'typography'],
		source: 'styles/typography.css'
	};
</script>

<DocsShell {settings}>
	<!-- Slot: Usage -->
	<svelte:fragment slot="usage">
		<section class="space-y-4">
			<h2>Excluding Styles</h2>
			<p>
				Use the <code>.unstyled</code> class to exclude and zero out typography styles for any individual element.
			</p>
			<CodeBlock
				language="html"
				code={`
<h2 class="unstyled">Unstyled H2</h2>
<p class="unstyled">Unstyled paragraph element.</p>
<a href="/" class="unstyled">Unstyled anchor element.</a>
			`}
			/>
			<div class="card variant-glass p-4">
				<h2 class="unstyled" data-toc-ignore>Unstyled H2</h2>
				<p class="unstyled">Unstyled paragraph element.</p>
				<a href="/" class="unstyled">Unstyled anchor element.</a>
			</div>
			<p>You may then append your own styles as desired.</p>
			<CodeBlock language="html" code={`<a href="/" class="unstyled text-orange-500">This link is orange.</a>`} />
			<h3>Tailwind Plugin</h3>
			<!-- prettier-ignore -->
			<p>
				If you're using the <a href="https://tailwindcss.com/docs/typography-plugin" target="_blank" rel="noreferrer">Tailwind Typography plugin</a>, all typography within the <code>.prose</code> class will be auto-excluded, allowing the plugin to handle most styles. Global styles like base text color will remain in effect though. See the plugin documentation for implementing overrides.
			</p>
		</section>
		<!-- Headings -->
		<div class="space-y-4">
			<h2>Headings</h2>
			<CodeBlock
				language="html"
				code={`
<h1>Skeleton H1</h1>
<h2>Skeleton H2</h2>
<h3>Skeleton H3</h3>
<h4>Skeleton H4</h4>
<h5>Skeleton H5</h5>
<h6>Skeleton H6</h6>
`}
			/>
			<div class="card variant-glass p-4 space-y-6">
				<h1>Skeleton H1</h1>
				<h2 data-toc-ignore>Skeleton H2</h2>
				<h3 data-toc-ignore>Skeleton H3</h3>
				<h4>Skeleton H4</h4>
				<h5>Skeleton H5</h5>
				<h6>Skeleton H6</h6>
			</div>
		</div>
		<!-- Paragraph -->
		<div class="space-y-4">
			<h2>Paragraph</h2>
			<CodeBlock language="html" code={`<p>The quick brown fox jumps over the lazy dog.</p>`} />
			<div class="card variant-glass p-4 text-center"><p>The quick brown fox jumps over the lazy dog.</p></div>
		</div>
		<!-- Anchor -->
		<div class="space-y-4">
			<h2>Anchor</h2>
			<CodeBlock language="html" code={`<a href="/">Anchor</a>`} />
			<div class="card variant-glass p-4 text-center space-x-4">
				<a href="https://www.youtube.com/watch?v=XTgFtxHhCQ0" target="_blank" rel="noreferrer">Anchor</a>
			</div>
		</div>
		<!-- Blockquote -->
		<div class="space-y-4">
			<h2>Blockquote</h2>
			<CodeBlock language="html" code={`<blockquote>Skeleton</blockquote>`} />
			<div class="card variant-glass p-4">
				<blockquote class="max-w-[500px] mx-auto">
					Lorem ipsum, dolor sit amet consectetur adipisicing elit. Expedita cupiditate dolores dignissimos maiores doloremque fugiat,
					dolore doloribus nisi, repellendus mollitia nostrum, commodi a minus aperiam deleniti. Velit rerum ut tempora!
				</blockquote>
			</div>
		</div>
		<!-- Pre -->
		<div class="space-y-4">
			<h2>Pre-formatted Text</h2>
			<CodeBlock language="html" code={`<pre>The quick brown fox jumps over the lazy dog.</pre>`} />
			<div class="card variant-glass p-4">
				<pre class="max-w-[500px] mx-auto">The quick brown fox jumps over the lazy dog.</pre>
			</div>
		</div>
		<!-- Code -->
		<div class="space-y-4">
			<h2>Code</h2>
			<CodeBlock language="html" code={`<code>.myExampleClass</code>`} />
			<div class="card variant-glass p-4 text-center"><code>.myExampleClass</code></div>
		</div>
		<!-- Keyboard -->
		<div class="space-y-4">
			<h2>Keyboard</h2>
			<CodeBlock language="html" code={`<p>Press <kbd>⌘ + C</kbd> to copy.</p>`} />
			<div class="card variant-glass p-4 text-center">
				<p>Press <kbd>⌘ + C</kbd> to copy.</p>
			</div>
		</div>
		<!-- Ins/Del -->
		<div class="space-y-4">
			<h2>Insertion / Deletion</h2>
			<CodeBlock language="html" code={`<del><s>Always</s> Gonna Give You Up</del>`} />
			<CodeBlock language="html" code={`<ins cite="https://youtu.be/dQw4w9WgXcQ" datetime="10-31-2022">Never Gonna Give You Up</ins>`} />
			<div class="rounded overflow-hidden">
				<del><s>Always</s> Gonna Give You Up</del>
				<ins cite="https://youtu.be/dQw4w9WgXcQ" datetime="10-31-2022">Never Gonna Give You Up</ins>
			</div>
		</div>
	</svelte:fragment>
</DocsShell>
