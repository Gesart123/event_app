<script>
    import { enhance } from '$app/forms';
    import { slide } from 'svelte/transition';

    let { data } = $props();
</script>

<div class="max-w-5xl mx-auto p-6">
    <h1 class="text-3xl font-bold text-center text-blue-600 mb-6">Admin Dashboard</h1>

    <div class="flex justify-center mb-4">
        <a href="/admin/events/new" class="bg-green-500 text-white px-4 py-2 rounded shadow hover:bg-green-600 transition">Create a New Event</a>
    </div>

    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
        {#each data.events as event (event.id)}
            <div class="bg-white p-4 rounded-lg shadow hover:shadow-lg transition border border-gray-200" transition:slide>
                <p class="text-lg font-semibold text-gray-700">
                    <strong class="text-gray-500">ID:</strong> {event.id} <br>
                    <strong class="text-gray-500">Title:</strong> {event.title} <br>
                    <strong class="text-gray-500">URL:</strong> <a href="{event.url}" class="text-blue-500 hover:underline">{event.url}</a> <br>
                    <strong class="text-gray-500">Start Date:</strong> {event.start_date} <br>
                    <strong class="text-gray-500">End Date:</strong> {event.end_date} <br>
                    <strong class="text-gray-500">Start Time:</strong> {event.start_time} <br>
                    <strong class="text-gray-500">Location:</strong> {event.locationName} <br>
                    <strong class="text-gray-500">Category:</strong> {event.categoryName}
                </p>
                <form action="?/deleteEvent" method="POST" use:enhance class="mt-2">
                    <input type="hidden" name="id" value={event.id} />
                    <button type="submit" class="bg-red-500 text-white px-4 py-2 rounded hover:bg-red-600 transition">Delete</button>
                </form>
            </div>
        {/each}
    </div>
</div>
