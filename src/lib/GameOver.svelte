<script>
    export let winner;
    export let started;
    export let restartGame;
    export let mainMenu; 
</script>

<div class=" {winner != '' && started ? '' : 'hidden'} fixed left-[50%] top-[50%] translate-y-[-50%] translate-x-[-50%] variant-filled-surface md:w-[42vw] md:h-[22vw] w-[90vw] h-[60vh] rounded-xl flex flex-col items-center">
    <div class="h-full flex justify-center items-center">
        <p class="text-8xl text-center h1">{winner}</p>
    </div>
    <div class="h-3/4 flex justify-center items-center">
        <button on:click={()=>{restartGame()}} class="btn variant-filled-primary rounded-full mx-10">Restart</button>
        <button on:click={()=>{mainMenu()}} class="btn variant-filled-primary rounded-full mx-10">Main Menu</button>
    </div>
</div>