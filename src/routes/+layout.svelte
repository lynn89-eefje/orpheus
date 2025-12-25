<script>
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();

	import "$lib/styles.css";

	let title = $state("Orpheus <3")
</script>

<svelte:head> 
	<title>{title}</title>
	<link rel="icon" href={favicon} />
	<link rel="preconnect" href="https://fonts.googleapis.com">
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
	<link href="https://fonts.googleapis.com/css2?family=Geom:ital,wght@0,300..900;1,300..900&family=Montserrat:ital,wght@0,100..900;1,100..900&family=Playwrite+FR+Trad:wght@100..400&display=swap" rel="stylesheet">
	<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200&icon_names=arrow_circle_left,arrow_circle_right" />
</svelte:head>

{@render children()}
