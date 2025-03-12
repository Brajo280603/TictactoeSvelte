<script>
    export let winner;
    export let started;
    export let clickBox;
    export let valueArray;
    
</script>

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