<script lang="ts">
	interface FootballClub {
		id: string;
		title: string;
		logo: string;
		full_name: string;
		nicknames: string[];
		founded: number;
		ground: string;
		ground_capacity: number;
		league: string;
		links: {
			url: string;
			title: string;
		};
		colors: {
			hex: string;
			title: string;
		}[];
	}

	export let team: FootballClub;
</script>

{#if team}
	<a href={team.id}>
		<li class="bg-white border-[0.6px] border-neutral-300 p-[8px] flex-col rounded-[10px]">
			<p class="font-black text-neutral-900 text-[16px]">{team.title}</p>
			<div
				class="flex flex-row items-center h-[16px] w-full rounded-[4px] overflow-hidden mt-[12px] relative"
			>
				<div
					class="absolute top-[0.05px] left-[0.05px] rounded-[4px] border-[0.6px] border-neutral-300 w-[calc(100%-0.1px)] h-[calc(100%-0.1px)]"
				/>
				{#each team.colors as color}
					<div class="h-full w-full" style={`background-color: ${color.hex}`} />
				{/each}
			</div>
		</li>
	</a>
{/if}
