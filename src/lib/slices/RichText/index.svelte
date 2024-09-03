<script lang="ts">
	import Button from '$lib/components/Button.svelte';
import type { Content } from '@prismicio/client';
	import { PrismicRichText } from '@prismicio/svelte';

	export let slice: Content.RichTextSlice;
</script>

<div class="max-w-prose">
	<PrismicRichText
		field={slice.primary.content}
	/>
	{#if slice.primary.button_label && slice.primary.button_link}
		<Button class='prose prose-sm mx-auto md:mx-0 no-underline' githubIcon={true} linkField={slice.primary.button_link} label={slice.primary.button_label} />
	{/if}
	
</div>
