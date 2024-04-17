<script>
    import { onMount } from 'svelte';
    import { getBands, createBand, updateBand, deleteBand } from '$lib/api';

    let bands = [];
    let newBand = {
        name: '',
        country: '',
        website: 'https://www.example.com/',
        facebook: 'https://www.example.com/',
        instagram: 'https://www.example.com/',
        dayOfWeek: 'Friday',
        year: 2024
    };
    let selectedBand = null;

    async function loadBands() {
        bands = await getBands();
    }

    async function saveBand() {
        if (selectedBand) {
            await updateBand(selectedBand._id, newBand);
        } else {
            await createBand(newBand);
        }
        await loadBands();
        resetForm();
    }

    function editBand(band) {
        selectedBand = band;
        newBand = {...band};
    }

    async function removeBand(id) {
        await deleteBand(id);
        await loadBands();
    }

    function resetForm() {
        selectedBand = null;
        newBand = {
            name: '',
            country: '',
            website: 'https://www.example.com/',
            facebook: 'https://www.example.com/',
            instagram: 'https://www.example.com/',
            dayOfWeek: 'Friday',
            year: 2024
        };
    }

    onMount(loadBands);
</script>
<h2 class="ms-5 mt-4">Admin Panel</h2>
<div class="m-5 mt-3">
<form on:submit|preventDefault={saveBand} class="mb-4">
    <div class="form-group">
        <input class="form-control" placeholder="Name" bind:value={newBand.name} />
    </div>
    <div class="form-group">
        <input class="form-control" placeholder="Country" bind:value={newBand.country} />
    </div>
    <div class="form-group">
        <input class="form-control" placeholder="Website" bind:value={newBand.website} />
    </div>
    <div class="form-group">
        <input class="form-control" placeholder="Facebook" bind:value={newBand.facebook} />
    </div>
    <div class="form-group">
        <input class="form-control" placeholder="Instagram" bind:value={newBand.instagram} />
    </div>
    <div class="form-group">
        <select class="form-control" bind:value={newBand.dayOfWeek}>
            <option>Friday</option>
            <option>Saturday</option>
        </select>
    </div>
    <div class="form-group">
        <input class="form-control" type="number" placeholder="Year" bind:value={newBand.year} />
    </div>
    <div class="form-group">
        <button type="submit" class="btn btn-primary">{selectedBand ? 'Update' : 'Create'}</button>
        <button type="button" class="btn btn-secondary" on:click={resetForm}>Cancel</button>
    </div>
</form>

<h2>Bands</h2>
<ul class="list-group">
    {#each bands as band}
        <li class="list-group-item d-flex justify-content-between align-items-center">
            {band.name} - {band.country}
            <div>
                <button class="btn btn-info btn-sm mr-2" on:click={() => editBand(band)}>Edit</button>
                <button class="btn btn-danger btn-sm" on:click={() => removeBand(band._id)}>Delete</button>
            </div>
        </li>
    {/each}
</ul>
</div>

<style>
    button, input {
        margin-top: 10px;
    }
    .list-group-item {
        cursor: pointer;
    }
    .list-group-item:hover, input:hover {
        background-color: #f0f0f0;
    }
</style>