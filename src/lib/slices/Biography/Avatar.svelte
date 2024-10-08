<script lang="ts">
	import { onMount } from 'svelte';
	import { type ImageField } from '@prismicio/client';
	import { PrismicImage } from '@prismicio/svelte';
	import clsx from 'clsx';
	import gsap from 'gsap';

	export let image: ImageField;
	let className: string = '';
	export { className as class };

	let component: HTMLElement;

	onMount(() => {
		gsap.fromTo(
			'.avatar',
			{
				opacity: 0,
				scale: 1.4,
				rotation: 5
			},
			{
				scale: 1,
				opacity: 1,
				duration: 1.3,
				ease: 'power3.inOut',
				rotation: -2
			}
		);

		window.onmousemove = (e) => {
			if (!component) return; //No animation because no component
			const componentRect = (component as HTMLElement).getBoundingClientRect();
			const componentCenterX = componentRect.left + componentRect.width / 2;

			let componentPercent = {
				x: (e.clientX - componentCenterX) / componentRect.width / 2
			};

			let distFromCenterX = 1 - Math.abs(componentPercent.x);

			gsap
				.timeline({
					defaults: { duration: 0.5, overwrite: 'auto', ease: 'power3.out' }
				})
				.to(
					'.avatar',
					{
						rotation: gsap.utils.clamp(-2, 6, 15 * componentPercent.x)
					},
					0
				)
				.to(
					'.highlight',
					{
						opacity: distFromCenterX - 0.75,
						x: -30 + 30 * componentPercent.x
					},
					0
				);
		};
	});
</script>

<div class={clsx('relative h-full w-full', className)} bind:this={component}>
	<div class="avatar aspect-square overflow-hidden rounded-3xl border-2 border-slate-600 opacity-0">
		<PrismicImage
			field={image}
			class="pfp-image h-full w-full object-fill"
			imgixParams={{ q: 90 }}
		/>
		<div
			class="highlight absolute inset-0 w-full scale-110 bg-gradient-to-tr from-transparent via-purple-200 to-transparent opacity-0"
		></div>
	</div>
</div>

<style>
	.avatar {
		perspective: 500px;
		perspective-origin: 150%;
	}
</style>
