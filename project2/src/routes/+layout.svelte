<script lang="ts">
	import '../app.css';
	let { children } = $props();
</script>

<main>
	<nav>
		<img src="/assets/logo.png" alt="logo" class="logo">
		<ul>
			<li><a href="/">home</a></li>
			<li><a href="/shop">shop</a></li>
			<li><a href="/contact">contact</a></li>
			<li><a href="/visit-us">visit us</a></li>
		</ul>
	</nav>
{@render children()}
</main>
