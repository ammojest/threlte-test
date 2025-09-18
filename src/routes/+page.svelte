<script>
	import { Canvas } from '@threlte/core';
	import Scene from '../lib/components/scene.svelte';
</script>

<div>
	<Canvas>
		<Scene marginTop={40} />
	</Canvas>
</div>

<style>
	div {
		height: 100%;
		padding-top: 40px;
	}
</style>
