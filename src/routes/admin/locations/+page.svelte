<script>
    import { enhance } from '$app/forms';
    import { slide } from 'svelte/transition';
    import Warning from '$lib/components/Warning.svelte';

    let { data, form } = $props();
</script>

<div class="max-w-4xl mx-auto p-6">
    <h1 class="text-3xl font-bold text-center text-blue-600 mb-6">Admin Dashboard</h1>

    <div class="flex justify-center mb-4">
        <a href="/admin/locations/new" class="bg-green-500 text-white px-4 py-2 rounded shadow hover:bg-green-600 transition">Add a New Location</a>
    </div>

    {#if form && !form.success}
        <Warning message={form.message} class="mb-4"/>
    {/if}

    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
        {#each data.locations as location (location.id)}
            <div class="bg-white p-4 rounded-lg shadow hover:shadow-lg transition border border-gray-200" transition:slide>
                <p class="text-lg font-semibold text-gray-700">
                    <strong class="text-gray-500">ID:</strong> {location.id} <br>
                    <strong class="text-gray-500">Name:</strong> {location.name} <br>
                    <strong class="text-gray-500">Street:</strong> {location.street}
                </p>
                <form action="?/deleteLocation" method="POST" use:enhance class="mt-2">
                    <input type="hidden" name="id" value={location.id} />
                    <button type="submit" class="bg-red-500 text-white px-4 py-2 rounded hover:bg-red-600 transition">Delete</button>
                </form>
            </div>
        {/each}
    </div>
</div>
