<main>

<div class="body">
	{#if !inProgress}
		{#if !progressCompleted}
			<button onclick={startCounting}>START COUNTING</button>
		{/if}
	{/if}

	{#if inProgress}
		<p>{timeleft} seconds left</p>
	{/if}

	{#if progressCompleted}
        <br>

		<p>How many beats have you counted?</p>
		<input min=1 max=70 type=number bind:value={beats}/>

		<br>

		{#if beats > 70 || beats < 0}
		<p>You should write a realistic amount of beats.</p>
		<p>If you really have <strong>{beats * 4} BPM</strong>, then it means you should rush to the hospital right away.</p>
    {:else if beats > 0}
		<p>You have {beats * 4} BPM.</p>
    {/if}

    <br>

    <div>
        <button onclick={restart}>ANOTHER TRY</button>
    </div>
	{/if}
</div>
</main>

<script>
    import '../app.css'

    let timeleft = $state(15);
    let beats = $state(0);

    let inProgress = $state(false);
    let progressCompleted = $state(false);

    async function startCounting() {
        inProgress = true;
        // Here I used a loop command
    for (let i = 0; i < 15; i++) {
        await new Promise(resolve => setTimeout(resolve, 1000));
        timeleft -= 1
        }
        inProgress = false;
        progressCompleted = true;
    }

    function restart() {
        progressCompleted = false;
        timeleft = 15;
        inProgress = true;

        startCounting();
    }

</script>

<style>
    .body {
        align-content: center;
        justify-items: center;
        text-align: center;
    }
</style>
