<script lang="ts">
	import type { KeyTextField, LinkField } from '@prismicio/client';
	import { PrismicLink } from '@prismicio/svelte';

	import IconArrow from '~icons/ic/round-arrow-outward';
	import IconGithub from '~icons/fa-brands/github';

	export let linkField: LinkField;
	export let label: KeyTextField;
	export let showIcon: boolean = true;
	export let githubIcon: boolean = false;
	let className: string = '';
	export { className as class };
</script>

<PrismicLink
	field={linkField}
	class={`group text-slate-900 relative flex w-fit items-center justify-center overflow-hidden rounded-md border-2 border-slate-900 bg-slate-50 px-4 py-2 font-bold transition-transform ease-out hover-scale-105 ${className}`}
>
	<span
		class={`absolute inset-0 z-0 h-full rounded bg-purple-400 transition-transform duration-300 ease-in-out group-hover:translate-y-0 translate-y-9`}
	></span>

	{#if showIcon}
		{#if githubIcon}
			<IconGithub class="mr-2 z-10" />
			<span class="relative flex items-center justify-center gap-2">{label}</span>
		{:else}
			<span class="relative flex items-center justify-center gap-2">{label}</span>
			<IconArrow class="z-10"/>
		{/if}
	{/if}
</PrismicLink>
