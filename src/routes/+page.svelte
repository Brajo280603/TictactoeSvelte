<script>
	import MainMenu from "$lib/MainMenu.svelte";
    import GameOver from "$lib/GameOver.svelte";
    import Game from "$lib/Game.svelte";

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

	<MainMenu started={started} twoPlayerMode={twoPlayerMode}/>

	<!-- gameOver screen -->
	<GameOver winner={winner} started={started} restartGame={restartGame} mainMenu={mainMenu}/>

	<!-- game screen -->
	<Game winner={winner} started={started} clickBox={clickBox} valueArray={valueArray}/>
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