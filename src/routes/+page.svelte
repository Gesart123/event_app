<script>
	let { data } = $props();
	import {flip} from 'svelte/animate';


	let filteredEvents = $state(data.events);
	let selectedCategory = $state('all');
	function filterEvents() {
		if(selectedCategory == 'all') {
			filteredEvents = data.events;
		} else {
			filteredEvents = data.events.filter(e => e.category_id === selectedCategory.id);
		}
	}
</script>

<div class="p-6 max-w-4xl mx-auto">
    {#if data.user}
        <div class="flex justify-between items-center bg-blue-200 p-4 rounded-lg shadow">
            <p class="text-lg font-semibold text-blue-800">Welcome back, {data.user.username}!</p>
            <div class="flex gap-2">
                <form action="/logout?/logout" method="POST">
                    <button type="submit" class="bg-red-500 text-white px-4 py-2 rounded hover:bg-red-600">Logout</button>
                </form>
                <form action="/logout?/deleteAccount" method="POST">
                    <button type="submit" class="bg-gray-500 text-white px-4 py-2 rounded hover:bg-gray-600">Delete</button>
                </form>
            </div>
        </div>
    {:else}
        <div class="text-center p-4 bg-blue-100 rounded-lg shadow">
            <p class="text-lg font-medium text-blue-800">You are not logged in.</p>
            <p class="mt-2">
                <a href="/login" class="text-blue-600 hover:underline">Login</a>
                or
                <a href="/register" class="text-blue-600 hover:underline">Register</a>
            </p>
        </div>
    {/if}
</div>

<h1 class="text-3xl font-bold text-center mt-6 text-blue-700">My Event App</h1>
<p class="text-center text-blue-500 mt-2">Here are the current events.</p>

<div class="flex justify-center mt-4">
    <select class="border rounded px-4 py-2 shadow bg-white text-blue-700 border-blue-400" bind:value={selectedCategory} onchange={filterEvents}>
        <option value="all">ALL</option>
        {#each data.categories as category}
            <option value="{category}" class="text-blue-700">{category.name}</option>
        {/each}
    </select>
</div>

<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6 mt-6 p-6">
    {#each filteredEvents as event (event.id)}
        <div class="bg-blue-50 p-4 rounded-lg shadow hover:shadow-lg transition border border-blue-300" animate:flip>
            <p>{event.title}</p>
            <p>ID: {event.id}</p>
            <p>Start Date: <span>{event.start_date}</span></p>
        </div>
    {/each}
</div>

