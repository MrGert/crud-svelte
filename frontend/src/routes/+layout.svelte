<script>
	import { onMount } from 'svelte';

let w;
let path;
  onMount(() => {
    w = window.innerWidth;
    path = window.location.pathname;
  });
	let forside = 'act',
		bands = '',
		about = ''

  </script>

<nav class="navbar navbar-expand-md navbar-dark bg-dark ps-5 pe-5">
	<div class="container-fluid">
		<a class="navbar-brand" href="/"><img src="/logo.svg" alt="Logo" /></a>
		<button
    on:click={() => {
      let element = document.getElementById('thenav');
      element.classList.toggle('btn-group');
      element.classList.toggle('btn-group-vertical');
    }}
			class="navbar-toggler bg-primary"
			type="button"
			data-bs-toggle="collapse"
			data-bs-target="#navbarTogglerDemo02"
			aria-controls="navbarTogglerDemo02"
			aria-expanded="false"
			aria-label="Toggle navigation"
		>
			<span class="navbar-toggler-icon btn-group-vertical"></span>
		</button>

		<div class="collapse navbar-collapse" id="navbarTogglerDemo02">
			<div class="btn-group navbar-nav ms-auto mb-2 mb-lg-0" id="thenav" role="group">
				<a
					href="/"
					on:click={() => {
						(bands = ''), (forside = 'act'), (about = '');
					}}
					type="button"
					class="btn btn-primary text-start {forside}">Forside</a
				>
				<a
					href="/bands"
					on:click={() => {
						(bands = 'act'), (forside = ''), (about = '');
					}}
					type="button"
					class="btn btn-primary text-start {bands}">Bands</a
				>
				<a
					href="/about"
					on:click={() => {
						(bands = ''), (forside = ''), (about = 'act');
					}}
					type="button"
					class="btn btn-primary text-start {about}">Om festivalen</a
				>
				<a
					href="/admin"
					on:click={() => {
						(bands = ''), (forside = ''), (about = '');
					}}
					class="btn btn-primary text-white text-start"><i class="bi bi-lock-fill"></i></a
				>
			</div>
		</div>
	</div>
</nav>

<slot></slot>

<footer
	class="d-flex flex-wrap justify-content-between align-items-center py-3 my-4 border-top m-5 mt-5"
>
	<div class="col-md-6 d-flex align-items-center">
		<a href="/" class="mb-3 me-2 mb-md-0 text-body-secondary text-decoration-none lh-1">
			<img src="/logo-black.svg" alt="Logo" />
		</a>
		<span class="mb-3 mb-md-0 text-body-secondary"
			><small>&copy; 2024 Fuzztival Esjberg</small></span
		>
	</div>

	<ul class="nav col-md-4 justify-content-end list-unstyled d-flex">
		<a href="https://www.facebook.com/"><li class="ms-3"><i class="bi bi-facebook bbb"></i></li></a>
		<a href="https://www.instagram.com/"
			><li class="ms-3"><i class="bi bi-instagram bbb"></i></li></a
		>
	</ul>
</footer>

<style>
	.bbb {
		color: #000;
	}
	a {
		font-weight: bold;
		font-size: 16px;
		color: #aaa;
	}
	.act {
		color: #fff;
	}
</style>
