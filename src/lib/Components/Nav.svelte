<script lang="ts">
	import { onMount } from 'svelte';
    import { page } from '$app/state';
    import { resolve } from '$app/paths';


	let isOpen = $state(false);
	let isMobile = $state(false);
	let projectsOpen = $state(false);

	// Detect screen size for mobile menu toggle
	onMount(() => {
		const checkSize = () => {
			isMobile = window.innerWidth < 768 ;
			if (!isMobile) isOpen = false; // Close menu on resize to desktop
		};
		
		checkSize();
		window.addEventListener('resize', checkSize);
		return () => window.removeEventListener('resize', checkSize);
	});

	function toggleMenu() {
		isOpen = !isOpen;
	}

	function closeMenu() {
		isOpen = false;
	}

	function toggleProjects() {
		projectsOpen = !projectsOpen;
		console.log('projectsOpen:', projectsOpen);
	}
</script>

<nav class="sticky top-0 w-full max-w-3/4 bg-[#c1a882]/95 backdrop-blur-md border-b border-[#333]/10 shadow-sm">
	<div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
		<div class="flex items-center justify-between h-16">

			<!-- Desktop Menu -->
             {#if !isMobile}
			<div>
				<a
						href={resolve("/")}
						class="text-xl font-bold transition-colors duration-200
							   {page.url.pathname === "/" 
								? 'text-black underline decoration-2 underline-offset-4' 
								: 'text-[#333] hover:text-black'}"
					>
						Home
					</a>
			</div>

			<div class="item">
				<button
				onclick={toggleProjects}
				aria-haspopup="true">
					<a href="#top" class="text-[#333] hover:text-black text-xl font-bold transition-colors duration-200">Projects</a>
				</button>

				{#if projectsOpen}
				<ul class="dropdown">
			
					<li>
						<a
							href={resolve("/Projects/Professional")}
							class="text-xl font-bold transition-colors duration-200
							   {page.url.pathname === "/Projects/Professional" 
								? 'text-black underline decoration-2 underline-offset-4' 
								: 'text-[#333] hover:text-black'}"
								onclick={toggleProjects}
						>
						Professional
						</a>
					</li>

					<li>
						<a
							href={resolve("/Projects/Personal")}
							class="text-xl font-bold transition-colors duration-200
							   {page.url.pathname === "/Projects/Personal" 
								? 'text-black underline decoration-2 underline-offset-4' 
								: 'text-[#333] hover:text-black'}"
								onclick={toggleProjects}
						>
						Personal
						</a>
					</li>
				</ul>
				{/if}
			</div>

			<div>
				<a
						href={resolve("/About")}
						class="text-xl font-bold transition-colors duration-200
							   {page.url.pathname === "/About" 
								? 'text-black underline decoration-2 underline-offset-4' 
								: 'text-[#333] hover:text-black'}"
					>
						About
					</a>
			</div>

			<div>
				<a
					href={resolve("/Certs")}
					class="text-xl font-bold transition-colors duration-200
					   {page.url.pathname === "/Certs" 
							? 'text-black underline decoration-2 underline-offset-4' 
							: 'text-[#333] hover:text-black'}"
				>
				Certs
				</a>
			</div>
            {/if}

			{#if isMobile}
            <!-- Mobile Menu Button -->
			<div class="md:hidden flex items-center">
				<button
					type="button"
					class="text-[#333] hover:text-black focus:outline-none p-2"
					onclick={toggleMenu}
					aria-label="Toggle menu"
				>
					<!-- Hamburger Icon -->
					<svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
						{#if isOpen}
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
						{:else}
							<path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
						{/if}
					</svg>
				</button>
			</div>
            {/if}
		</div>
	</div>

	<!-- Mobile Menu Dropdown -->
	{#if isOpen}
		<div class="md:hidden bg-[#c1a882] border-t border-[#333]/10 absolute w-full left-0 top-16 shadow-lg">
			<div class="px-2 pt-2 pb-3 space-y-1 sm:px-3">
				<div class="hidden md:flex md:items-center md:space-x-8">
				<a
						href={resolve("/")}
						class="text-xl font-bold transition-colors duration-200
							   {page.url.pathname === "/" 
								? 'text-black underline decoration-2 underline-offset-4' 
								: 'text-[#333] hover:text-black'}"
						onclick={closeMenu}
					>
						Home
					</a>
			</div>

			<div class="hidden md:flex md:items-center md:space-x-8">
				<a
						href={resolve("/Projects")}
						class="text-xl font-bold transition-colors duration-200
							   {page.url.pathname === "/Projects/Personal" 
								? 'text-black underline decoration-2 underline-offset-4' 
								: 'text-[#333] hover:text-black'}"
						onclick={closeMenu}
					>
						Projects
					</a>
			</div>

			<div class="hidden md:flex md:items-center md:space-x-8">
				<a
						href={resolve("/About")}
						class="text-xl font-bold transition-colors duration-200
							   {page.url.pathname === "/About" 
								? 'text-black underline decoration-2 underline-offset-4' 
								: 'text-[#333] hover:text-black'}"
						onclick={closeMenu}
					>
						About
					</a>
			</div>

			<div class="hidden md:flex md:items-center md:space-x-8">
				<a
						href={resolve("/Certs")}
						class="text-xl font-bold transition-colors duration-200
							   {page.url.pathname === "/Certs" 
								? 'text-black underline decoration-2 underline-offset-4' 
								: 'text-[#333] hover:text-black'}"
						onclick={closeMenu}
					>
						Certs
					</a>
			</div>
			</div>
		</div>
	{/if}
</nav>


<style>
.item {
		position: relative;
		padding-bottom: 0.0rem;
	}

	.dropdown {
		position: absolute;
		top: 100%;
		left: 0;
		flex-direction: column;
		background: bg-color;
		border: 1px solid #333333;
		padding: 0.5rem;
	}

</style>