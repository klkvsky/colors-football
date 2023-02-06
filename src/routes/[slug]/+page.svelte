<script lang="ts">
	//
	import Info from '$lib/Info.json';
	import { page } from '$app/stores';
	//
	let item = Info.find((item) => item.id === $page.params.slug.toString());
	//
	function hexToRgbCmyk(hex: string) {
		let r, g, b;
		if (hex.length === 7) {
			r = parseInt(hex.substring(1, 3), 16);
			g = parseInt(hex.substring(3, 5), 16);
			b = parseInt(hex.substring(5, 7), 16);
		} else {
			r = parseInt(hex.substring(1, 2) + hex.substring(1, 2), 16);
			g = parseInt(hex.substring(2, 3) + hex.substring(2, 3), 16);
			b = parseInt(hex.substring(3, 4) + hex.substring(3, 4), 16);
		}
		let c = 1 - r / 255;
		let m = 1 - g / 255;
		let y = 1 - b / 255;
		let k = Math.min(c, m, y);
		if (k === 1) {
			c = 0;
			m = 0;
			y = 0;
		} else {
			c = (c - k) / (1 - k);
			m = (m - k) / (1 - k);
			y = (y - k) / (1 - k);
		}
		c = Math.round(c * 100);
		m = Math.round(m * 100);
		y = Math.round(y * 100);
		k = Math.round(k * 100);
		return {
			hex: hex,
			rgb: `${r}, ${g}, ${b}`,
			cmyk: `${c}, ${m}, ${y}, ${k}`
		};
	}
</script>

{#if item}
	<main class="pt-[32px] flex flex-col gap-[16px]">
		<div
			class="bg-neutral-100 w-full aspect-video border-[.6px] border-neutral-300 rounded-[10px] grid place-items-center lg:max-w-[840px] lg:mx-auto"
		>
			<img src={`./logos/${item.logo}`} alt="" class="w-1/3 h-auto" />
		</div>

		<div
			class="bg-white border-[0.6px] border-neutral-300 rounded-[10px] p-[12px] flex flex-col gap-[8px] w-full h-fit lg:max-w-[840px] lg:mx-auto lg:grid lg:grid-cols-2 relative"
		>
			<div class="hidden lg:block absolute w-[.6px] h-[63%] bg-neutral-300 top-0 left-[50%]" />
			<p class="font-bold text-[16px] text-neutral-600 lg:pr-[24px]">
				Full Name: <span class="text-neutral-900"> {item?.full_name} </span>
			</p>
			<p class="font-bold text-[16px] text-neutral-600 lg:pl-[24px]">
				Nickname(s): <span class="text-neutral-900">
					{#each item.nicknames as nickname, i}
						{#if i > 0}, {/if}
						{nickname}
					{/each}
				</span>
			</p>
			<p class="font-bold text-[16px] text-neutral-600 lg:pr-[24px]">
				Founded: <span class="text-neutral-900"> {item?.founded} </span>
			</p>
			<p class="font-bold text-[16px] text-neutral-600 lg:pl-[24px]">
				Ground: <span class="text-neutral-900"> {item?.ground} </span>
			</p>
			<p class="font-bold text-[16px] text-neutral-600 lg:pr-[24px]">
				Capacity: <span class="text-neutral-900"> {item?.ground_capacity.toLocaleString()} </span>
			</p>

			{#if item.links}
				<div
					class="flex flex-row items-center gap-[12px] border-t-[0.6px] border-neutral-300 pt-[12px] lg:col-span-2 w-full overflow-scroll no-scrollbar"
				>
					{#each item.links as link}
						<a
							href={link.url}
							target="_blank"
							rel="noreferrer"
							class="text-neutral-900 text-[14px] font-black px-[12px] py-[8px] rounded-full border-[0.6px] border-neutral-300 capitalize hover:bg-neutral-100 transition-all duration-300 ease-in-out"
						>
							{link.title}</a
						>
					{/each}
				</div>
			{/if}
		</div>
		<div
			class="flex flex-col gap-[16px] sm:grid sm:grid-cols-2 lg:grid-cols-3 lg:w-[840px] lg:mx-auto"
		>
			{#each item.colors as color}
				<div
					class="bg-white p-[8px] rounded-[10px] flex flex-col gap-[8px] border-[0.6px] border-neutral-300 w-full h-fit"
				>
					<div
						class="w-full h-[64px] rounded-[4px] border-[0.6px] border-neutral-300"
						style={`background-color: ${color.hex}`}
					/>
					<h2 class="font-black capitalize text-[16px] text-neutral-900 mt-[4px]">{color.title}</h2>
					<p class="text-neutral-600 text-[16px] font-bold uppercase">
						Hex: <span class="text-neutral-900"> {color.hex.slice(1)} </span>
					</p>
					<p class="text-neutral-600 text-[16px] font-bold">
						RGB: <span class="text-neutral-900"> {hexToRgbCmyk(color.hex.slice(1)).rgb} </span>
					</p>
					<p class="text-neutral-600 text-[16px] font-bold">
						CMYK: <span class="text-neutral-900"> {hexToRgbCmyk(color.hex.slice(1)).cmyk} </span>
					</p>
				</div>
			{/each}
		</div>
	</main>
{/if}
