<script lang="ts">
	import { spring } from 'svelte/motion';
	import styles from './Counter.module.scss';
	let count = 0;

	const displayed_count = spring();
	$: displayed_count.set(count);
	$: offset = modulo($displayed_count, 1);

	function modulo(n: number, m: number) {
		// handle negative numbers
		return ((n % m) + m) % m;
	}
</script>

<div class={styles.counter}>
	<button class={styles.counter__btn} on:click={() => (count -= 1)} aria-label="Decrease the counter by one">
		<svg class={styles.svg} aria-hidden="true" viewBox="0 0 1 1">
			<path class={styles.path} d="M0,0.5 L1,0.5" />
		</svg>
	</button>

	<div class={styles.counter__viewport}>
		<div class={styles.counter__digits} style="transform: translate(0, {100 * offset}%)">
			<strong class={styles.hidden} aria-hidden="true">{Math.floor($displayed_count + 1)}</strong>
			<strong>{Math.floor($displayed_count)}</strong>
		</div>
	</div>

	<button class={styles.counter__btn} on:click={() => (count += 1)} aria-label="Increase the counter by one">
		<svg class={styles.svg} aria-hidden="true" viewBox="0 0 1 1">
			<path class={styles.path} d="M0,0.5 L1,0.5 M0.5,0 L0.5,1" />
		</svg>
	</button>
</div>