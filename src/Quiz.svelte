<script>
	import Question from './Question.svelte';

	let quiz = getQuiz();

	async function getQuiz() {
		const res = await fetch(
			'https://opentdb.com/api.php?amount=10&category=12&type=multiple'
		);
		const quiz = await res.json();
		return quiz;
	}

	const handleClick = () => {
		quiz = getQuiz();
	};
</script>

<div>
	<button on:click={handleClick}>Get questions</button>

	{#await quiz}
		....Loading
	{:then data}
		{#each data.results as question}
			<Question {question} />
		{/each}
	{/await}
</div>
