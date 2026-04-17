<script lang="ts">
    import Nav from '$lib/Components/Nav.svelte';
    import { resolve } from '$app/paths';
    import Logo from '$lib/assets/images/logo.png';

</script>

<!-- Logo / Brand -->
<a href={resolve("/")} class="flex-shrink-0 flex group" aria-label="Logo">
	<span class="">
		<enhanced:img src={Logo}></enhanced:img>
	</span>
</a>
<Nav />