<script>
    import axios from "axios"
    import {onMount} from "svelte"
    const getJokes = async() =>{
        const response = await axios.get("https://api.chucknorris.io/jokes/random")
        return response
    }
    let jokes = []
    onMount(async()=>{
        const joke = await getJokes()
        jokes = [joke.data]
        console.log(jokes);
    })

    $:jokes = []

onMount(async()=>{
    const joke = await getJokes()

    jokes=[joke.data]

    // console.log(jokes);
})

let refresh = setInterval(async()=>{
        const response = await getJokes()
        jokes = [...jokes,response.data]

        console.log(response)
},3500)
</script>
<body>
<div class="w-full h-[100vh] bg-gradient-to-r from-indigo-500 to-purple-500 flex justify-center items-center">
    <div class="flex flex-col shadow-md h-[20rem] w-[20rem] rounded-md bg-[#ffffff] p-4">
        <h1 class="text-indigo-700 text-center text-4xl font-bold">Chuck Norris</h1>
            <div class="flex flex-col gap-4 h-[18rem] overflow-auto">
                {#each jokes as joke}
                    <h1  class="text-indigo-800 pb-[6px] pt-[1rem] text-x2 font-medium flex w-[100%] h-[100%] border-[#d3cefc] border-b">{joke.value}</h1>
                {/each}
            </div>
    </div>
</div>

</body>