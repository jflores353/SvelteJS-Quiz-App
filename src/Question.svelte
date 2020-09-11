<script>
	export let question;
	let isCorrect;
	let isAnswered = false;
	let wrongAnswers = question.incorrect_answers.map((answer) => {
		return {
			answer,
			correct: false,
		};
	});

	let allAnswers = [
		...wrongAnswers,
		{
			answer: question.correct_answer,
			correct: true,
		},
	];

	function checkAnswer(correct) {
		isAnswered = true;
		isCorrect = correct;
	}

	function shuffle(arr) {
		arr.sort(() => Math.random() - 0.5);
	}

	shuffle(allAnswers);
</script>

<style>
	h4 {
		color: green;
	}
</style>

<h3>
	{@html question.question}
</h3>
{#if isAnswered}
	<h4>
		{#if isCorrect}Correct{:else}Wrong Answer{/if}
	</h4>
{/if}
{#each allAnswers as answer}
	<button on:click={() => checkAnswer(answer.correct)}>
		{@html answer.answer}
		<!-- {answer.correct} **** This displays true/false values for each answer **** -->
	</button>
{/each}
