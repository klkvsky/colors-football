<script>
	import Card from '../lib/card.svelte';
	import Info from '../lib/Info.json';
	import { clickOutside } from '../lib/clickOutside.js';

	let newInfo = Info;
	let isLeaguePickerOpen = false;
	let isSearchOpen = false;
	let serachResult = [];
	// parse info json to find all leagues and make them unique and assign them to a variable
	const leagues = [...new Set(Info.map((item) => item.league))];
	// make a function that parses the info json and returns the teams that match the league
	function getTeams(league) {
		return Info.filter((item) => item.league === league);
	}

	let isColorSpeicif = false;
	// make a function that parses the info json and returns the teams that match the search query by team title or by color title inside team color array and array and by league title and if search query is color specific it will return color name in search query
	function searchTeams(query) {
		return Info.filter((item) => {
			if (item.title.toLowerCase().includes(query)) {
				isColorSpeicif = false;
				return item;
			} else if (item.colors.some((color) => color.title.toLowerCase().includes(query))) {
				isColorSpeicif = true;
				return item;
			} else if (item.league.toLowerCase().includes(query)) {
				isColorSpeicif = false;
				return item;
			} else if (item.colors.some((color) => color.hex.toLowerCase().includes(query))) {
				isColorSpeicif = true;
				return item;
			}
		});
	}

	let searchQuery = '';
	let selectedLeague = 'All';

	let leaguesColors = [
		{
			league: 'All',
			color: '#000000'
		},
		{
			league: 'Premier',
			color: '#360D3A'
		}
	];
</script>

<div class="w-full">
	<nav
		class="flex flex-col gap-[16px] mt-[32px] sm:flex-row items-center lg:max-w-[840px] lg:mx-auto"
	>
		<label
			class="bg-white p-[8px] rounded-[10px] flex flex-row items-center gap-[12px] border-[0.6px] border-neutral-300 relative w-full cursor-text"
			for="search"
			use:clickOutside
			on:click_outside={() => {
				isSearchOpen = false;
			}}
		>
			<div
				class="bg-[#F5F5F5] rounded-full grid place-items-center border-[0.6px] border-neutral-300 w-[40px] aspect-square"
			>
				<svg
					width="20"
					height="20"
					viewBox="0 0 20 20"
					fill="none"
					xmlns="http://www.w3.org/2000/svg"
				>
					<path
						d="M9.16667 15.8333C12.8486 15.8333 15.8333 12.8486 15.8333 9.16667C15.8333 5.48477 12.8486 2.5 9.16667 2.5C5.48477 2.5 2.5 5.48477 2.5 9.16667C2.5 12.8486 5.48477 15.8333 9.16667 15.8333Z"
						stroke="#171717"
						stroke-width="1.66667"
						stroke-linecap="round"
						stroke-linejoin="round"
					/>
					<path
						d="M17.5 17.5L13.875 13.875"
						stroke="#171717"
						stroke-width="1.66667"
						stroke-linecap="round"
						stroke-linejoin="round"
					/>
				</svg>
			</div>

			<input
				type="text"
				placeholder="Try Red"
				id="search"
				class="font-black placeholder:text-neutral-600 text-[16px] outline-none"
				autocomplete="off"
				bind:value={searchQuery}
				on:focus={() => {
					isSearchOpen = true;
				}}
				on:input={(e) => {
					isSearchOpen = true;
					serachResult = searchTeams(e.target.value.toLowerCase());
				}}
			/>

			{#if serachResult.length > 0 && searchQuery.length > 0}
				<div
					class={`absolute top-[85%] left-0 w-[calc(100%+1.2px)] -translate-x-[.6px] h-fit bg-white border-[0.6px] border-[#360D3A29] border-t-transparent rounded-b-[10px] origin-top px-[8px] flex flex-col text-left overflow-hidden text-[14px] font-black z-[100] shadow-md  ${
						isSearchOpen
							? 'max-h-[calc(2ch+24px+8)] delay-200 opacity-100'
							: 'max-h-[0px]  pointer-events-none opacity-0'
					}`}
				>
					<div class="w-full h-[0.6px] bg-neutral-300 mt-[8px] opacity-0" />
					{#each serachResult as result, index}
						<div class="ml-[50px] w-[calc(100%-100px)] h-[0.6px] bg-neutral-300" />
						<a href={result.id} class="flex flex-row items-center gap-[12px] py-[6px]">
							<div class=" rounded-full grid place-items-center w-[40px] aspect-square">
								<img
									src={`./logos/${result.logo}`}
									alt={result.title}
									class="w-[30px] h-[30px] object-contain"
								/>
							</div>

							<p class="font-black placeholder:text-neutral-600 text-[16px] outline-none">
								{#key isColorSpeicif}
									{#if isColorSpeicif && searchQuery.length > 2}
										<span class="text-[#360D3A]">{result.title}</span>
										<span class="text-[#360D3A] capitalize">
											{result.colors.find((color) => color.title.includes(searchQuery)) &&
												result.colors.find((color) => color.title.includes(searchQuery)).title}
											<span class="hidden"> yo </span>
										</span>
									{:else}
										{result.title}
									{/if}
								{/key}
							</p>
						</a>
					{/each}
				</div>
			{/if}
		</label>

		<div
			class={`bg-white p-[8px] rounded-[10px] flex flex-row items-center gap-[12px] relative border-[0.6px] border-neutral-300 w-full sm:max-w-[220px] sm:min-w-[320px] cursor-pointer ${
				isLeaguePickerOpen ? 'rounded-b-none' : ''
			}`}
			on:click={() => {
				isLeaguePickerOpen = !isLeaguePickerOpen;
			}}
			on:keydown={() => {}}
			use:clickOutside
			on:click_outside={() => {
				isLeaguePickerOpen = false;
			}}
		>
			<div
				class="rounded-full grid place-items-center border-[0.6px] w-[40px] aspect-square"
				style={`background-color: ${
					selectedLeague != 'All'
						? `${
								leaguesColors.find((league) => league.league == selectedLeague.split(' ')[0]).color
						  }14`
						: '#F5F5F5'
				}; border-color: ${
					selectedLeague != 'All'
						? `${
								leaguesColors.find((league) => league.league == selectedLeague.split(' ')[0]).color
						  }29`
						: '#360D3A29'
				} `}
			>
				<!-- All images are without work League in names -->
				<img
					src={`./leagues/${selectedLeague != 'All' ? selectedLeague.split(' ')[0] : 'All'}.svg`}
					alt={selectedLeague}
					class="w-[25px] h-[25px] object-contain"
				/>
			</div>

			<p class="text-neutral-600 font-black text-[16px]">
				{selectedLeague != 'All' ? selectedLeague : 'All Leagues'}
			</p>
			<svg
				width="12"
				height="12"
				viewBox="0 0 12 12"
				fill="none"
				xmlns="http://www.w3.org/2000/svg"
				class="-ml-[8px]"
			>
				<rect width="12" height="12" fill="white" />
				<path
					d="M9.58579 4H2.41421C1.52331 4 1.07714 5.07714 1.70711 5.70711L5.29289 9.29289C5.68342 9.68342 6.31658 9.68342 6.70711 9.29289L10.2929 5.70711C10.9229 5.07714 10.4767 4 9.58579 4Z"
					fill="#525252"
				/>
			</svg>

			<div
				class={`absolute top-[103%] left-0 w-[calc(100%+1.2px)] -translate-x-[.6px] -translate-y-[2px] h-fit bg-white border-[0.6px] border-[#360D3A29] border-t-transparent rounded-b-[10px] origin-top transition-all duration-300 ease-in-out px-[8px] flex flex-col gap-[12px] pb-[8px] text-left overflow-clip text-[14px] font-black shadow-md rounded-t-none ${
					isLeaguePickerOpen ? 'opacity-100' : 'hidden pointer-events-none opacity-0'
				}`}
			>
				<div class="w-full h-[.6px] bg-neutral-300" />

				<button
					on:click={() => {
						newInfo = Info;
						isLeaguePickerOpen = false;
						selectedLeague = 'All';
					}}
					class={`text-neutral-900 text-left ${
						selectedLeague == 'All' ? 'text-neutral-900' : 'text-neutral-600'
					}`}>All Leagues</button
				>
				{#each leagues as league}
					<button
						on:click={() => {
							newInfo = getTeams(league);
							selectedLeague = league;
							isLeaguePickerOpen = false;
						}}
						class={`relative z-50 text-left ${
							selectedLeague == league ? 'text-neutral-900' : 'text-neutral-600'
						}`}>{league}</button
					>
				{/each}
			</div>
		</div>
	</nav>
	<main class="flex flex-col mt-[16px] lg:mt-[32px] lg:max-w-[840px] lg:mx-auto">
		<ul class="flex flex-col gap-[16px] sm:grid sm:grid-cols-2 lg:grid-cols-3">
			{#each newInfo as team}
				<Card {team} />
			{/each}
		</ul>
	</main>
</div>
