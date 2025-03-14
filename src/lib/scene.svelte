<script>
	import { T, useTask } from '@threlte/core';
	import { interactivity } from '@threlte/extras';
	import { Spring } from 'svelte/motion';

	interactivity();
	const scale = new Spring(1);

	let rotation = 0;
	useTask((delta) => {
		rotation += 0.5 * delta;
	});
</script>

<T.PerspectiveCamera
	makeDefault
	position={[10, 10, 10]}
	oncreate={(ref) => {
		ref.lookAt(0, 1, 0);
	}}
/>

<T.DirectionalLight position={[2, 6, 2]} castShadow />

<T.Mesh
	rotation.y={rotation}
	position.y={1}
	scale={scale.current}
	onpointerenter={() => {
		scale.target = 1.5;
	}}
	onpointerleave={() => {
		scale.target = 1;
	}}
	castShadow
>
	<T.BoxGeometry args={[6, 0.5, 6]} />
	<T.MeshStandardMaterial color="#f00" />
</T.Mesh>

<T.Mesh rotation.x={-Math.PI / 2} receiveShadow>
	<T.CircleGeometry args={[8, 80]} />
	<T.MeshStandardMaterial color="white" />
</T.Mesh>
