<script lang="ts">
    import Nav from '$lib/Components/Nav.svelte';
    import { resolve } from '$app/paths';
    import Logo from '$lib/assets/images/logo.png';

</script>

<div>
<div class="justify-center">
<!-- Logo / Brand -->
<a href={resolve("/")} class="shrink-0 flex justify-center group" aria-label="Logo">
	<span class="">
		<enhanced:img src={Logo} class="h-[10em]"></enhanced:img>
	</span>
</a>
</div>

<div class="flex justify-center">
<Nav />
</div>
</div>