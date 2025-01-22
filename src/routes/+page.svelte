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

<div>
    {#if data.user}

        <p>Welcome back, {data.user.username}</p>

        <form action="/logout?/logout" method="POST">
            <button type="submit">Logout</button>
        </form>

        <form action="/logout?/deleteAccount" method="POST">
            <button type="submit">Delete</button>
        </form>

    {:else} 
        <p>
            You are logged in. 
        </p>
        <p>
            <a href="/login">Login</a>
            or
            <a href="/register">Register</a>
        </p>
    {/if}
</div>

<h1 class="events-title">My Event App</h1>

<p class="events-description">Here are the current events.</p>

<select name="" id="" bind:value={selectedCategory} onchange={filterEvents}>
	<option value="all">ALL</option>
	{#each data.categories as category}
		<option value="{category}">{category.name}</option>
	{/each}
</select>


<div class="events-container">
	{#each filteredEvents as event (event.id)}	
		<div animate:flip>
			<p class="event-details">
				<strong>ID:</strong>
				{event.id} 
				<strong>Title:</strong>
				{event.title} |
				<strong>Start Date:</strong>
				{event.start_date}
			</p>
		</div>
	{/each}
</div>

<style>
	.page {
        font-family: 'Roboto', Arial, sans-serif;
        padding: 20px;
        color: #2c3e50; 
        background: linear-gradient(135deg, #e8f8f5, #d6eaf8);
    }

    .title {
        font-size: 2.8em;
        text-align: center;
        color: #34495e; 
        margin-bottom: 15px;
        font-weight: bold;
    }

    .description {
        text-align: center;
        color: #566573; 
        margin-bottom: 30px;
        font-size: 1.2em;
    }

    .filter-section {
        display: flex;
        justify-content: center;
        margin-bottom: 30px;
        align-items: center;
        gap: 15px;
    }

    .filter-label {
        font-size: 1em;
        font-weight: 600;
        color: #2c3e50; 
    }

    select {
        padding: 10px;
        font-size: 1em;
        border-radius: 5px;
        border: 1px solid #aab7b8; 
        background-color: #ecf0f1;
        color: #2c3e50;
        transition: border-color 0.2s, box-shadow 0.2s;
    }
    select:focus {
        border-color: #5dade2; 
        box-shadow: 0 0 5px #5dade2;
        outline: none;
    }
    .events-container {
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
        gap: 20px;
        max-width: 1000px;
        margin: 0 auto;
    }

    .event-card {
        background: #ffffff; 
        padding: 20px;
        border-radius: 12px;
        box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
        transition: transform 0.2s, box-shadow 0.3s;
        border-left: 5px solid #5dade2; 
    }

    .event-card:hover {
        transform: translateY(-5px);
        box-shadow: 0 6px 15px rgba(0, 0, 0, 0.15);
        border-left: 5px solid #2ecc71;
    }

    .event-title {
        font-size: 1.4em;
        font-weight: 600;
        margin-bottom: 10px;
        color: #34495e;
    }

    .event-info {
        font-size: 1em;
        color: #7f8c8d;
    }

    .event-info strong {
        color: #2c3e50;
    }

    @media (max-width: 768px) {
        .title {
            font-size: 2.2em;
        }

        .description {
            font-size: 1em;
        }

        .filter-section {
            flex-direction: column;
            gap: 10px;
        }

        select {
            width: 100%;
        }
    }
    
</style>
