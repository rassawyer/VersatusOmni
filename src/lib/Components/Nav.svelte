<script lang="ts">
	import { onMount } from 'svelte';
    import { page } from '$app/state';
    import { resolve } from '$app/paths';

    // Define the allowed routes explicitly
	type Route = '/' | '/Projects' | '/Projects/Professional' | '/Projects/Personal' | '/Certs';

	interface NavLink {
		id: string;
        href: Route;
		label: string;
	}

	// Navigation Links
	const links: NavLink[] = [
		{ label: 'Home', href: '/', id: 'home' },
		{ label: 'Projects', href: '/Projects', id: 'projects' },
        { label: 'Professional', href: '/Projects/Professional', id: 'professional'},
		{ label: 'Personal', href: '/Projects/Personal', id: 'personal' },
		{ label: 'Certs', href: '/Certs', id: 'certs' }
	]as const;

	let isOpen = $state(false);
	let isMobile = $state(false);

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
</script>

<nav class="fixed top-0 w-full bg-[#c1a882]/95 backdrop-blur-md border-b border-[#333]/10 z-50 shadow-sm">
	<div class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8">
		<div class="flex items-center justify-between h-16">

			<!-- Desktop Menu -->
             {#if !isMobile}
			<div class="hidden md:flex md:items-center md:space-x-8">
				{#each links as link (link.id)}
					<a
						href={resolve(link.href)}
						class="text-sm font-medium transition-colors duration-200
							   {page.url.pathname === link.href 
								? 'text-black underline decoration-2 underline-offset-4' 
								: 'text-[#333] hover:text-black'}"
						onclick={closeMenu}
					>
						{link.label}
					</a>
				{/each}
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
				{#each links as link (link.id)}
					<a
						href={resolve(link.href)}
						class="block px-3 py-2 rounded-md text-base font-medium 
							   {page.url.pathname === link.href 
								? 'bg-[#333]/10 text-black font-bold' 
								: 'text-[#333] hover:bg-[#333]/5 hover:text-black'}"
						onclick={closeMenu}
					>
						{link.label}
					</a>
				{/each}
			</div>
		</div>
	{/if}
</nav>