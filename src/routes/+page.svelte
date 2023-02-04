<script>
	import Card from '../lib/card.svelte';
	import Footer from '$lib/footer.svelte';

	let isLeaguePickerOpen = false;
	let isSearchOpen = false;
</script>

<div class="h-screen">
	<nav
		class="flex flex-col gap-[16px] mt-[32px] sm:flex-row items-center lg:max-w-[840px] lg:mx-auto"
	>
		<label
			class={`bg-white p-[8px] rounded-[10px] flex flex-row items-center gap-[12px] border-[0.6px] border-neutral-300 relative sm:w-full ${
				isSearchOpen ? 'rounded-b-none border-b-transparent' : ''
			}`}
			for="search"
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
				on:focus={() => {
					isSearchOpen = true;
				}}
				on:blur={() => {
					isSearchOpen = false;
				}}
			/>

			<div
				class={`absolute top-full left-0 w-[calc(100%+1.2px)] -translate-x-[.6px] h-fit bg-white border-[0.6px] border-[#360D3A29] border-t-transparent rounded-b-[10px] origin-top transition-all duration-500 ease-in-out px-[8px] flex flex-col gap-[12px] pb-[8px] text-left overflow-hidden text-[14px] font-black z-[100] shadow-md ${
					isSearchOpen
						? 'max-h-[calc(2ch+24px+8)] delay-200 opacity-100'
						: 'max-h-[0px]  pointer-events-none opacity-0'
				}`}
			>
				<div class="w-full h-[.6px] bg-neutral-300 mt-[8px]" />

				<div class="flex flex-row items-center gap-[12px]">
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

					<p class="font-black placeholder:text-neutral-600 text-[16px] outline-none">Arsenal</p>
				</div>
				<div class="flex flex-row items-center gap-[12px]">
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

					<p class="font-black placeholder:text-neutral-600 text-[16px] outline-none">Arsenal</p>
				</div>
			</div>
		</label>

		<button
			class={`bg-white p-[8px] ${
				isLeaguePickerOpen ? 'rounded-b-none border-b-transparent' : ''
			} rounded-[10px] flex flex-row items-center gap-[12px] relative border-[0.6px] border-neutral-300 transition-all duration-500 ease-out sm:min-w-[220px]`}
			on:click={() => {
				isLeaguePickerOpen = !isLeaguePickerOpen;
			}}
		>
			<div
				class="bg-[#360D3A14] rounded-full grid place-items-center border-[0.6px] border-[#360D3A29] w-[40px] aspect-square"
			>
				<svg
					width="20"
					height="24"
					viewBox="0 0 20 24"
					fill="none"
					xmlns="http://www.w3.org/2000/svg"
				>
					<g clip-path="url(#clip0_645_260)">
						<path
							d="M4.33092 1.98194C5.38132 2.47742 6.07645 3.08129 6.20002 3.17419C6.15368 2.89548 5.93742 1.57935 5.7984 0.774194C6.40084 1.19226 7.85287 2.19871 8.31628 2.52387C8.50165 1.93548 9.18132 0 9.18132 0C9.18132 0 10.3862 1.93548 10.5716 2.26065C10.8342 2.0129 12.2553 0.402581 12.626 0C12.7033 0.913548 12.7651 2.24516 12.796 2.43097C12.8732 2.33806 13.4293 1.56387 14.3407 0.836129C13.939 1.62581 13.7537 2.70968 13.661 3.59226C12.7496 3.32903 11.7919 3.18968 10.8187 3.18968C8.93417 3.18968 7.1423 3.68516 5.59758 4.56774C5.33498 3.71613 4.91791 2.66323 4.33092 1.98194ZM18.8203 18.6116L17.9862 17.6826C17.7545 20.1755 16.5187 22.3123 14.2789 23.7987L13.9236 22.4516C12.0082 23.8297 8.7488 24.7123 5.93742 23.1329C6.29271 21.3523 6.5862 19.5406 5.93742 17.3729C4.37726 19.7729 3.00246 20.7329 3.00246 20.7329C1.95206 18.9523 2.04474 15.4065 2.35368 14.3535L0.608154 14.8955C0.608154 13.7032 1.47319 11.1794 2.70897 9.75484L1.64311 9.58452C2.38458 8.0671 3.48132 6.76645 4.85612 5.76C4.43905 6.44129 4.43905 8.02065 5.62848 8.62452C5.11872 7.74194 5.07238 6.64258 5.58214 6.05419C6.12279 5.46581 7.00328 5.68258 7.55937 6.13161C7.38945 5.63613 6.8797 5.01677 6.16913 4.97032C7.55937 4.24258 9.18132 3.85548 10.8496 3.85548C11.174 3.85548 11.483 3.88645 11.7764 3.90194C12.2708 4.08774 12.9813 4.78452 13.3212 5.23355C13.3212 5.23355 13.3521 4.72258 13.0586 4.11871C14.8813 4.56774 15.7618 5.31097 16.1171 5.6671C16.1943 6.45677 16.426 6.92129 16.7504 7.68C16.1634 7.02968 14.6805 5.94581 13.9545 5.69806C13.9545 5.69806 13.8773 6.37935 13.6456 6.70452C12.2244 5.68258 11.5447 5.41935 11.5447 5.41935C9.96913 5.57419 8.99596 6.19355 8.43986 6.65806L8.90328 7.06065C7.97645 7.33935 7.35856 8.16 7.35856 8.16C7.35856 8.19097 8.19271 8.29935 8.19271 8.29935C8.19271 8.29935 8.10002 9.27484 9.3358 9.89419C10.3862 10.4052 11.8691 9.77032 13.2903 10.3432C12.3634 9.27484 11.7301 8.77936 11.7301 8.77936C11.7301 8.77936 11.3594 8.70194 11.0968 8.70194C10.7724 8.70194 10.2781 8.77936 9.76832 8.56258C9.50571 8.46968 9.21222 8.28387 8.99596 8.14452C8.99596 8.14452 9.64474 7.46323 10.6025 7.32387C10.6025 7.32387 11.4675 7.55613 12.1472 8.0671C12.5951 7.61806 13.074 7.64903 13.074 7.64903C13.074 7.64903 12.6106 8.09806 12.7496 8.60903C13.4293 9.2129 14.1708 10.08 14.1708 10.08C14.9122 9.66193 16.5496 9.75484 16.8895 10.1574C16.4724 9.6 15.839 9.15097 15.3756 8.76387C15.3293 8.5471 14.7886 7.83484 14.7269 7.75742C14.7269 7.75742 15.2212 7.92774 15.6537 8.29935C15.7773 8.11355 16.0244 7.92774 16.3334 7.85032C16.6577 8.12903 16.735 8.5471 16.7041 8.62452C16.5651 8.81032 16.3951 8.88774 16.3951 8.88774L17.183 9.75484L17.2602 9.12C19.0984 11.7368 20.1025 14.7871 18.8203 18.6116ZM15.3602 12.96V11.6129C15.3602 11.6129 14.7577 11.4271 14.109 10.9161C12.8114 11.1019 11.2512 12.4181 11.2512 12.4181C11.2512 12.4181 11.7919 13.4245 12.3634 14.5239C13.383 14.6323 14.8968 13.3626 15.3602 12.96ZM16.6577 15.4065C16.6577 15.4065 16.5651 14.849 16.1017 14.3381L15.0976 14.369C15.0976 14.369 13.7228 15.5303 12.9041 15.5613C12.9041 15.5613 13.3675 16.4284 13.5992 16.8619C14.0626 16.769 14.8504 16.3974 15.1903 16.0258C15.1903 16.0258 15.4065 16.7226 15.3602 17.5432C15.8236 17.249 16.4569 16.5368 16.6577 15.4065ZM17.0748 10.9471C16.5651 11.3652 16.148 11.6284 16.148 11.6284V12.9755C16.5187 13.3781 16.874 13.7187 17.1521 14.3226C17.6618 13.4245 17.5382 12.0774 17.0748 10.9471Z"
							fill="#360D3A"
						/>
					</g>
					<defs>
						<clipPath id="clip0_645_260">
							<rect width="19" height="24" fill="white" transform="translate(0.5)" />
						</clipPath>
					</defs>
				</svg>
			</div>

			<p class="text-neutral-600 font-black text-[16px]">Premier League</p>
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
				class={`absolute top-full left-0 w-[calc(100%+.5px)] -translate-x-[.35px] -translate-y-[2px] h-fit bg-white border-[0.6px] border-[#360D3A29] border-t-transparent rounded-b-[10px] origin-top transition-all duration-500 ease-in-out px-[8px] flex flex-col gap-[12px] pb-[8px] text-left overflow-clip text-[14px] font-black shadow-md rounded-t-none ${
					isLeaguePickerOpen
						? 'max-h-[calc(2ch+24px+8)]'
						: 'max-h-[0px] pointer-events-none opacity-0'
				}`}
			>
				<div class="w-full h-[.6px] bg-neutral-300" />

				<p class="text-neutral-900">All Leagues</p>
				<p class="text-neutral-600">Premier League</p>
			</div>
		</button>
	</nav>
	<main class="flex flex-col mt-[16px] lg:mt-[32px] lg:max-w-[840px] lg:mx-auto">
		<ul class="flex flex-col gap-[16px] sm:grid sm:grid-cols-2 lg:grid-cols-3">
			<Card />
			<Card />
			<Card />
			<Card />
			<Card />
			<Card />
			<Card />
			<Card />
			<Card />
			<Card />
			<Card />
			<Card />
			<Card />
			<Card />
		</ul>
	</main>

	<Footer />
</div>
