<script>
	import { onMount } from 'svelte';
	import { getBands } from '$lib/api';

	let bands = [];
	let fridayBands = [];
	let saturdayBands = [];

	async function loadBands() {
		bands = await getBands();
		fridayBands = bands.filter((band) => band.dayOfWeek.toLowerCase() === 'friday');
		saturdayBands = bands.filter((band) => band.dayOfWeek.toLowerCase() === 'saturday');
	}

	onMount(loadBands);
</script>

<div class="container-fluid bg-dark text-white">
    <div class="container col-xxl-8 px-4 py-5">
        <div class="row flex-lg-row-reverse align-items-center g-5 py-5">
            <div class="col-12 col-sm-8 col-md-6 mt-2">
                <img
                    src="/tobakken.jpg"
                    alt="Tobakken"
                    class="d-block mx-lg-auto img-fluid"
                    width="700"
                    height="500"
                    loading="lazy"
                />
            </div>
            <div class="col-md-6">
                <h1>Esbjerg Fuzztival</h1>
                <p class="lead">
                    {#each bands as band, index}
                        <i class="bi bi-asterisk"></i>
                        <b style="font-size: calc(18px - {index}px);">
                            &nbsp;{band.name}&nbsp;
                        </b>
                    {/each}
                </p>
                <div class="d-grid gap-2 d-md-flex justify-content-md-start">
                    <a href="#program" type="button" class="btn btn-primary px-4 me-md-2">
                        Program<i class="bi bi-arrow-down"></i>
                    </a>
                    <a href="/bands" type="button" class="btn btn-outline-secondary px-4">
                        <i class="bi bi-music-note"></i>Bands
                    </a>
                </div>
            </div>
        </div>
    </div>
</div>

<div class="container-fluid py-3 px-5">
	<h2 id="program">Program</h2>
	<h4>Fredag</h4>
	<div class="row">
		<!-- Adding a row container here -->
		{#each fridayBands as band}
			<div class="col-sm-4">
				<!-- Changed from col-sm-4 col-lg-4 to just col-sm-4 -->
				<div class="card bg-primary">
					<img
						src={`/img/${band.name.toLowerCase()}.jpg`}
						alt={band.name}
						on:error={(e) => (e.target.style.display = 'none')}
					/>
					<div class="card-body">
						<a href="/bands"
							><b class="card-title text-white"
								>{band.name}<i class="bi-arrow-right float-end"></i></b
							></a
						>
					</div>
				</div>
			</div>
		{/each}
	</div>
</div>

<div class="container-fluid py-3 px-5">
	<h2 id="program">Program</h2>
	<h4>Fredag</h4>
	<div class="row">
		<!-- Adding a row container here -->
		{#each saturdayBands as band}
			<div class="col-sm-4">
				<!-- Changed from col-sm-4 col-lg-4 to just col-sm-4 -->
				<div class="card bg-primary">
					<img
						src={`/img/${band.name.toLowerCase()}.jpg`}
						alt={band.name}
						on:error={(e) => (e.target.style.display = 'none')}
					/>
					<div class="card-body">
						<a href="/bands"
							><b class="card-title text-white"
								>{band.name}<i class="bi-arrow-right float-end"></i></b
							></a
						>
					</div>
				</div>
			</div>
		{/each}
	</div>
</div>

<style>
</style>
