<script>
	import { T, useTask } from '@threlte/core';
	import { interactivity } from '@threlte/extras';
	import { Spring } from 'svelte/motion';

	interactivity();
	const scale = new Spring(1);

	let rotation = 0;
	let orbitRotation = 0;
	const orbitRadius = 0.7;

	useTask((delta) => {
		rotation += delta * 0.5; // local spin
		orbitRotation += delta * 0.9; // orbit speed
	});
</script>

<T.DirectionalLight position={[0, 10, 10]} intensity={2} />
<T.AmbientLight intensity={1} />
<T.PointLight position={[0, 5, 5]} intensity={1.5} />
<!-- Left group (orbits right) -->
<T.Group
	position={[Math.cos(orbitRotation) * orbitRadius, -2, Math.sin(orbitRotation) * orbitRadius]}
	scale={scale.current}
	onpointerenter={() => scale.set(1.5)}
	onpointerleave={() => scale.set(1)}
>
	<T.Mesh position={[0, 1, 0]} rotation.y={rotation}>
		<T.CylinderGeometry args={[0.3, 0.3, 1.2, 32]} />
		<T.MeshStandardMaterial color="#ff6401" />
	</T.Mesh>
	<T.Mesh position={[0, 2.2, 0]}>
		<T.SphereGeometry args={[0.35, 32, 32]} />
		<T.MeshStandardMaterial color="#ff6401" />
	</T.Mesh>
</T.Group>

<!-- Right group (opposite side of orbit) -->
<T.Group
	position={[
		Math.cos(orbitRotation + Math.PI) * orbitRadius,
		-2,
		Math.sin(orbitRotation + Math.PI) * orbitRadius
	]}
	scale={scale.current}
	onpointerenter={() => scale.set(1.5)}
	onpointerleave={() => scale.set(1)}
>
	<T.Mesh position={[0, 1.3, 0]} rotation.y={rotation}>
		<T.CylinderGeometry args={[0.3, 0.3, 1.8, 32]} />
		<T.MeshStandardMaterial color="#ff6401" />
	</T.Mesh>
	<T.Mesh position={[0, 2.8, 0]}>
		<T.SphereGeometry args={[0.35, 32, 32]} />
		<T.MeshStandardMaterial color="#ff6401" />
	</T.Mesh>
</T.Group>
