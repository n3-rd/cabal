<script>
	import { onMount } from 'svelte';
	import { goto } from '$app/navigation';
	import ArrowDiagonalUpRight from './icons/ArrowDiagonalUpRight.svelte';
	import { gsap } from 'gsap';
	const tl = gsap.timeline();

	onMount(() => {
		const heroImage = document.querySelector('.hero-image');
		heroImage.classList.remove('invisible');
		const animateCabalText = tl.from('.cabal-text div', {
			duration: 1,
			y: 100,
			opacity: 0,
			stagger: 0.2,
			ease: 'power2.out'
		});
		const animateEnterBtn = tl
			.from('.arrow', {
				duration: 1,
				y: 100,
				opacity: 0,
				ease: 'power2.out'
			})
			.to('.arrow', {
				duration: 1,
				rotate: 180
			});

		const arrow = document.querySelector('.arrow');
		arrow.addEventListener('click', () => {
			tl.to('.arrow-icon', {
				duration: 0.5,
				opacity: 0
			})
				.to('.arrow', {
					duration: 0.5,
					height: 0,
					width: 0
				})
				.to('.cabal-text div', {
					duration: 1,
					y: -100,
					opacity: 0,
					stagger: 0.2,
					ease: 'power2.out'
				})
				.to('.hero-image', {
					duration: 1,
					y: -100,
					opacity: 0,
					ease: 'power2.out',
					onComplete() {
						goto('/experiment');
					}
				});
		});
	});
</script>

<div class="h-screen w-screen bg-purple-800 flex justify-center items-center">
	<div
		class="h-[90%] w-[90%] bg-[url(/img/connor-botts-YxKBT84-nm0-unsplash.jpg)] bg-cover bg-center rounded-2xl flex justify-between flex-col hero-image invisible"
	>
		<div class="text-6xl font-bold pl-5 pt-5 w-1/3 text-[#c7baa1] cabal-text">
			<div class="h-14 overflow-hidden">Cabal is an</div>
			<div class="h-14 overflow-hidden">aesthetic</div>
			<div class="h-14 overflow-hidden">experiment</div>
		</div>
		<div class="h-[12rem] w-full flex justify-center items-center">
			<button
				class="enter-btn h-24 w-24 border-2 border-[#c7baa1] rounded-full flex justify-center items-center overflow-hidden arrow hoverable"
			>
				<div class="arrow-icon">
					<ArrowDiagonalUpRight size={64} />
				</div>
			</button>
		</div>
	</div>
</div>
