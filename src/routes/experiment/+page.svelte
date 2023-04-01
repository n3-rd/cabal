<script>
	import { onMount } from 'svelte';
	import Cursor from '../../lib/Cursor.svelte';
	import Julia from '../../lib/experiment-sections/Julia.svelte';
	import SmoothScroll from '../../lib/SmoothScroll.svelte';
	import Lenis from '@studio-freight/lenis';
	import Nora from '../../lib/experiment-sections/Nora.svelte';
	import { gsap } from 'gsap';

	const smoothScroll = () => {
		const lenis = new Lenis();
		function raf(time) {
			lenis.raf(time);
			requestAnimationFrame(raf);
		}

		requestAnimationFrame(raf);
	};

	onMount(async () => {
		const { ScrollTrigger } = await import('gsap/ScrollTrigger');
		gsap.registerPlugin(ScrollTrigger);
		smoothScroll();

		gsap.to('.page', {
			scrollTrigger: {
				trigger: '.julia',
				toggleActions: 'restart pause reverse pause',
				start: 'top bottom',
				end: 'bottom bottom'
			},
			backgroundColor: '#FF553A',
			duration: 1
		});
		gsap.to('.page', {
			scrollTrigger: {
				trigger: '.nora',
				toggleActions: 'restart pause reverse pause',
				start: 'top bottom',
				end: 'bottom bottom'
			},
			backgroundColor: '#419C8D',
			duration: 1
		});
	});
</script>

<div>
	<Cursor color="#fff" mixBlendMode="exclusion" />

	<div
		class=" bg-purple-800 page
    transition duration-500 ease-in-out
    "
	>
		<div class="julia">
			<Julia />
		</div>
		<div class="nora">
			<Nora />
		</div>
	</div>
</div>
