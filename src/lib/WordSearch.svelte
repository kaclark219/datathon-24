<script>
	import { onMount } from 'svelte'
	import { Puzzle } from './utils.js'
	
	export let words = ["debit", "credit", "budget", "asset", "interest", "loan"]
	export let range = ["a", "z"]

	const { letters } = new Puzzle({ words, range })
	
	const dimensions = Math.floor(letters.length ** 0.5)
	const grid = letters.map((letter, i) => ({
		letter,
		c: i % dimensions,
		r: Math.floor(i / dimensions)
	}))

	let line = null
	let svg
	let w, h

	onMount(() => {
		handleSize()
	})

	const handleSize = () => {
		const { width, height } = svg.getBoundingClientRect()
		w = width
		h = height
	}

	let hasSelected = false

	const handleStart = () => {
		hasSelected = true
		line = null
	}

	const handleEnd = () => {
		hasSelected = false
		line = null
		match = null
	}

	const handleIng = (e) => {
		if (!hasSelected) return;

    const { offsetX: x, offsetY: y } = e;

    // Scale coordinates to the grid dimensions
    const c = Math.floor((x / w) * dimensions);
    const r = Math.floor((y / h) * dimensions);

    // Ensure c and r are within grid boundaries
    if (c < 0 || c >= dimensions || r < 0 || r >= dimensions) return;

    if (!line) {    
        line = { c1: c, r1: r, c2: c, r2: r };
    } else {
        const { c2, r2 } = line;
        if (c2 !== c) line.c2 = c;
        if (r2 !== r) line.r2 = r;
    }
	}

	let matches = []
	let lines = [];
	let match	
	$: if(line) {
		const { c1, r1, c2, r2} = line

		const rs = r2 - r1
		const cs = c2 - c1

		if (rs === 0 || cs === 0 || Math.abs(rs) === Math.abs(cs)) {
			const n = Math.max(Math.abs(rs), Math.abs(cs))

			let rd = 0;
			if (rs > 0) rd = 1;
			else if (rs < 0) rd = -1;

			let cd = 0;
			if (cs > 0) cd = 1;
			else if (cs < 0) cd = -1;

			match = Array(n + 1)
				.fill()
				.map((_, i) => grid[(r1 + i * rd) * dimensions + (c1 + i * cd)].letter)
				.reduce((acc, curr) => `${acc}${curr}`, "");

			if(!matches.includes(match) && words.includes(match)) {
				matches = [...matches, match]
				lines = [
					...lines,
					{
						c1,
						r1,
						c2,
						r2,
					},
				];
			}
		}
	}
</script>

<svelte:window on:resize={handleSize} />

<article>	
	<h2>
		<mark>{match || ''}</mark>
	</h2>

	<svg
    bind:this={svg}
    on:mousedown={handleStart} 
    on:mouseleave={handleEnd}
    on:mouseup={handleEnd}
    on:mousemove={handleIng}
    viewBox="-1 -1 {dimensions + 2} {dimensions + 2}">
  <g fill="none" stroke="#006D1F" stroke-width="1" stroke-linecap="round">
    <g opacity="0.4">
      {#each lines as { c1, r1, c2, r2 }}
      <path d="M {c1} {r1} {c2} {r2}" />
      {/each}
    </g>
    
    {#if line}
    <path d="M {line.c1} {line.r1} {line.c2} {line.r2}" />
    {/if}
  </g>

  <g style="pointer-events: none; user-select: none;" fill="currentColor" text-anchor="middle" dominant-baseline="middle" font-size="0.6" transform="translate(0 0.02)">
    {#each grid as {letter, c, r}}
    <g transform="translate({c} {r})">
      <text>{letter}</text>
    </g>
    {/each}
  </g>
</svg>

	<ul>
		{#each words as word}
		<li>
			{#if matches.includes(word)}
			<del>{word}</del>
			{:else}
			{word}
			{/if}
		</li>
		{/each}
	</ul>

</article>


<style>
    article {
      width: 90vw;
      height: 80vh;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding: 1rem;
    }
  
    mark {
      letter-spacing: 0.1rem;
      font-weight: 700;
      padding: 0.2rem 1.25rem;
      color: #D20000;
      background: white;
    }
  
    svg {
      display: block;
      width: 100%;
      height: 100%;
    }
  
    ul {
      padding: 1rem;
      align-self: stretch;
      background: #0320B4;
      display: flex;
      flex-wrap: wrap;
      justify-content: center;
      gap: 30px;
      color: white;
      font-family: "Open Sans", sans-serif;
      font-size: 24px;
    }
  
    li::marker {
      content: '';
    }
  </style>