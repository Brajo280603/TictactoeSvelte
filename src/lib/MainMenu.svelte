<script>
    export let started 
    export let twoPlayerMode
</script>

<div class=" {started ? 'hidden' : ''}  fixed left-[50%] top-[50%] translate-y-[-50%] translate-x-[-50%] variant-filled-surface md:w-[42vw] md:h-[22vw] w-[90vw] h-[60vh] rounded-xl flex flex-col items-center">
    <div class="h-full flex justify-center items-center">
        <p class="text-8xl text-center h1">Tic Tac Toe</p>
    </div>
    <div class="h-3/4 flex justify-center items-center">
        <button on:click={()=>{twoPlayerMode()}} class="btn variant-filled-primary rounded-full mx-10">Two Player</button>
        <button on:click={()=>{alert("not available , Please use two player mode")}} class="btn variant-filled-primary rounded-full mx-10">VS Ai</button>
    </div>
</div>