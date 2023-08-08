<script>
	let buttons = new Array(9).fill(null);
	let result = null;
	let turn = 'X';

	const winningCombinations = [
		[0,1,2],
		[3,4,5],
		[6,7,8],
		[0,3,6],
		[1,4,7],
		[2,5,8],
		[0,4,8],
		[2,4,6]
	]

	function setValue(i) {
		buttons[i] = turn;
		buttons = [...buttons];
		turn = turn === 'X' ? 'O' : 'X';

		if(!buttons.includes(null)) {
			result = "Match Draw";
		} else {
			checkWinner();
		}
	};

	function checkWinner() {
		for(let i=0; i<winningCombinations.length;i++) {
			if (buttons[winningCombinations[i][0]] !== null) {
				if (buttons[winningCombinations[i][0]] === buttons[winningCombinations[i][1]] 
					&& buttons[winningCombinations[i][1]] === buttons[winningCombinations[i][2]]) {
						result = "Winner : " + buttons[winningCombinations[i][0]];
						break;
				}
			}
		}
	}

	function restart() {
		buttons = new Array(9).fill(null);
		result = null;
		turn = 'X';
	}


</script>

<style>
	.container {
		width: 100%;
		height: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		background-color: antiquewhite;
	}
	.tictac {
		width: 600px;
		height: 600px;
		display: flex;
		flex-wrap: wrap;
	}

	.tictac button {
		width: 200px;
		height: 200px;
		margin: 0px;
	}
	p {
		font-size: 48px;
		font-weight: bold;
		margin: 2rem;
	}
</style>

{#if !result}
<div class="container">
	<div class="tictac">
		{#each buttons as button,i}
			<button on:click={() => setValue(i)}>
				{button? button : ""}
			</button>
		{/each}
	</div>
</div>
{:else}
	<div class="container">
	<p>
		{result}
	</p>

		<button on:click={restart}>
		Play Again
		</button>

	</div>
{/if}