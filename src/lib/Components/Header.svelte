<script lang="ts">
    import Nav from '$lib/Components/Nav.svelte';
    import { resolve } from '$app/paths';

</script>

<div>
<div class="justify-center">
<!-- Logo / Brand -->
<a href={resolve("/")} class="shrink-0 flex justify-center group" aria-label="Logo">
	<span class="">
		<enhanced:img src='/src/lib/assets/images/logo.png' class="h-[10em] w-auto" alt="logo"/>
	</span>
</a>
</div>

<div class="flex justify-center">
<Nav />
</div>
</div>