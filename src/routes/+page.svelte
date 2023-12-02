<script>
	let gridArray;
	let currentplayer;
	let valueArray;
	let winner;
	let started;

	gridArray = [0,0,0,0,0,0,0,0,0];
	currentplayer = 1;
	valueArray = [];
	winner = ""; 
	started = false;

	let winningIndexes = [
		
		[0,1,2],
		[0,3,6],
		[0,4,8],
		[1,4,7],
		[2,4,6],
		[2,5,8],
		[3,4,5],
		[6,7,8]
		
	]

	let gameSteps = 0;

	let winningindexNumber = null;

	for(let i = 0; i < 9; i++){
		valueArray[i] = gridArray[i] == 0 ? "" : gridArray[i] == 1 ? "X" : "O";
	}

	function clickBox(index){
		if(gridArray[index] == 0){
			gridArray[index] = currentplayer;
			currentplayer = currentplayer == 1 ? 2 : 1;
			for(let i = 0; i < 9; i++){
				valueArray[i] = gridArray[i] == 0 ? "" : gridArray[i] == 1 ? "X" : "O";
			}

			gameSteps++;
		}

		if(gameSteps > 2){
			winnerCalc();

			if(gameSteps > 8){
				// alert("over")
				setTimeout(()=>{
					gameOver()
				},1500);
			}
		}

	


		
	}

	function winnerCalc(){
		let xInputIndexs = [];
		let oInputIndexs = [];
		winningindexNumber = null;

		for(let i=0;i<9;i++){
			if(valueArray[i] == "X"){
				xInputIndexs.push(i)
			}
			else if(valueArray[i] == "O"){
				oInputIndexs.push(i)
			}
		}

		console.log(xInputIndexs)
		console.log(oInputIndexs)

		if(findWinner(xInputIndexs) == true){
			disableEveryGridButton();
			onlyShowWinningSquares();

			setTimeout(()=>{
				gameOver("X")
			},1500)
		}else if(findWinner(oInputIndexs) == true){
			disableEveryGridButton();
			onlyShowWinningSquares();

			setTimeout(()=>{
				gameOver("O")
			},1500)
		}else {
			// gameOver(null)
		}
		
		
		
	}


	function findWinner(input_Array){

		let matchCount = 0;

		for(let i = 0;i<winningIndexes.length;i++){
			// console.log(winningIndexes[i]);
			matchCount = 0;
			for(let j = 0;j<winningIndexes[i].length;j++){


				for(let inp_i = 0;inp_i < input_Array.length;inp_i++){
					if(input_Array[inp_i] == winningIndexes[i][j]){
						matchCount++;
					}
				}
			}

			console.log(matchCount)
			if(matchCount >=3){
				winningindexNumber = i;
				return true;
			}

			if(i == winningIndexes.length -1){
				winningindexNumber = i;
				return false;
			}

		}
	}

	

	//UI functions
	function restartGame(){
		gridArray = [0,0,0,0,0,0,0,0,0];
		for(let i = 0; i < 9; i++){
			valueArray[i] = gridArray[i] == 0 ? "" : gridArray[i] == 1 ? "X" : "O";
		}
		winner = "";
		gameSteps = 0;

		enableEveryGridButton();
		showAllSquares();
	}

	function mainMenu(){
		restartGame();
		started = false;
	}

	function gameOver(winnerName){

		if(winnerName == null || winnerName == undefined){
			winner = "Its a Tie!"; 
		}else{
			winner = `${winnerName} Wins`;
		}
	}

	function twoPlayerMode(){
		started = true;
		restartGame();

	}

	function disableEveryGridButton(){
		let allGridButtons = document.querySelectorAll(".gridBtn");

		allGridButtons.forEach(el=>{
			el.disabled = true;
		})
	}

	function enableEveryGridButton(){
		let allGridButtons = document.querySelectorAll(".gridBtn");

		allGridButtons.forEach(el=>{
			el.disabled = false;
		})
	}

	function onlyShowWinningSquares(){
		let allGridButtons = document.querySelectorAll(".gridBtn");
		
		if(winningindexNumber != null){
			for(let i = 0;i<allGridButtons.length;i++){
				if(i != winningIndexes[winningindexNumber][0] && i != winningIndexes[winningindexNumber][1] && i != winningIndexes[winningindexNumber][2]){
					allGridButtons[i].classList.add("hideDivs")
				}
			}
		}
	}

	function showAllSquares(){
		let allGridButtons = document.querySelectorAll(".gridBtn");
		

		if(winningindexNumber != null){
			for(let i = 0;i<allGridButtons.length;i++){
				if(i != winningIndexes[winningindexNumber][0] && i != winningIndexes[winningindexNumber][1] && i != winningIndexes[winningindexNumber][2]){
					allGridButtons[i].classList.remove("hideDivs")
				}
			}
		}
	}




</script>



<div class="container h-screen w-screen overflow-hidden">

	<!-- mainmenu screen -->
	<div class=" {started ? 'hidden' : ''}  fixed left-[50%] top-[50%] translate-y-[-50%] translate-x-[-50%] variant-filled-surface md:w-[42vw] md:h-[22vw] w-[90vw] h-[60vh] rounded-xl flex flex-col items-center">
		<div class="h-full flex justify-center items-center">
			<p class="text-8xl text-center h1">Tic Tac Toe</p>
		</div>
		<div class="h-3/4 flex justify-center items-center">
			<button on:click={()=>{twoPlayerMode()}} class="btn variant-filled-primary rounded-full mx-10">Two Player</button>
			<button on:click={()=>{alert("not available , Please use two player mode")}} class="btn variant-filled-primary rounded-full mx-10">VS Ai</button>
		</div>
	</div>


	<!-- gameOver screen -->
	<div class=" {winner != '' && started ? '' : 'hidden'} fixed left-[50%] top-[50%] translate-y-[-50%] translate-x-[-50%] variant-filled-surface md:w-[42vw] md:h-[22vw] w-[90vw] h-[60vh] rounded-xl flex flex-col items-center">
		<div class="h-full flex justify-center items-center">
			<p class="text-8xl text-center h1">{winner}</p>
		</div>
		<div class="h-3/4 flex justify-center items-center">
			<button on:click={()=>{restartGame()}} class="btn variant-filled-primary rounded-full mx-10">Restart</button>
			<button on:click={()=>{mainMenu()}} class="btn variant-filled-primary rounded-full mx-10">Main Menu</button>
		</div>
	</div>

	<!-- game screen -->
	<div class=" {winner === '' && started ? '' : 'hidden'}  fixed left-[50%] top-[50%] translate-y-[-50%] translate-x-[-50%] bg-orange-500 md:w-[42vw] md:h-[42vw] w-[90vw] h-[90vw] grid grid-cols-3">
		<button on:click={()=>{clickBox(0)}} class="border-8 flex justify-center items-center md:w-[14vw] md:h-[14vw] w-[30vw] h-[30vw] text-7xl gridBtn">{valueArray[0]}</button>
		<button on:click={()=>{clickBox(1)}} class="border-8 flex justify-center items-center md:w-[14vw] md:h-[14vw] w-[30vw] h-[30vw] text-7xl gridBtn">{valueArray[1]}</button>
		<button on:click={()=>{clickBox(2)}} class="border-8 flex justify-center items-center md:w-[14vw] md:h-[14vw] w-[30vw] h-[30vw] text-7xl gridBtn">{valueArray[2]}</button>
		<button on:click={()=>{clickBox(3)}} class="border-8 flex justify-center items-center md:w-[14vw] md:h-[14vw] w-[30vw] h-[30vw] text-7xl gridBtn">{valueArray[3]}</button>
		<button on:click={()=>{clickBox(4)}} class="border-8 flex justify-center items-center md:w-[14vw] md:h-[14vw] w-[30vw] h-[30vw] text-7xl gridBtn">{valueArray[4]}</button>
		<button on:click={()=>{clickBox(5)}} class="border-8 flex justify-center items-center md:w-[14vw] md:h-[14vw] w-[30vw] h-[30vw] text-7xl gridBtn">{valueArray[5]}</button>
		<button on:click={()=>{clickBox(6)}} class="border-8 flex justify-center items-center md:w-[14vw] md:h-[14vw] w-[30vw] h-[30vw] text-7xl gridBtn">{valueArray[6]}</button>
		<button on:click={()=>{clickBox(7)}} class="border-8 flex justify-center items-center md:w-[14vw] md:h-[14vw] w-[30vw] h-[30vw] text-7xl gridBtn">{valueArray[7]}</button>
		<button on:click={()=>{clickBox(8)}} class="border-8 flex justify-center items-center md:w-[14vw] md:h-[14vw] w-[30vw] h-[30vw] text-7xl gridBtn">{valueArray[8]}</button>
	</div>
</div>

<div class="hideDivs hidden" >

</div>
<style>

	.hideDivs{
		animation: hide 1500 ease forwards ;
	}

@keyframes hide {
  0% {
	opacity: 1;
  }
  90%{
	opacity: 0.1;
  }
  100% {
	opacity: 0;
  }
}
</style>