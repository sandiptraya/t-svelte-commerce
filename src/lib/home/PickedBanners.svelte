<script>
import LazyImg from '$lib/components/Image/LazyImg.svelte'

export let banners

$: pickedBanners = banners?.filter((b) => {
	return b._id?.type === 'picked' && b._id?.title !== 'DEAL ZONE'
})

$: pickedBannersForDeals = banners?.filter((b) => {
	return b._id?.type === 'picked' && b._id?.title === 'DEAL ZONE'
})
</script>

<div class="flex flex-col gap-5 sm:gap-10">
	{#if pickedBannersForDeals?.length}
		<div class="flex flex-col gap-5 sm:gap-10">
			{#each pickedBannersForDeals as b}
				<div class="flex flex-col gap-5 sm:gap-10">
					<h1
						class="p-3 py-5 text-center font-serif text-xl font-medium tracking-wider sm:px-10 sm:text-2xl md:py-10 md:text-3xl xl:text-4xl uppercase">
						{b._id?.title}
					</h1>

					{#if b.data?.length}
						<div class="flex flex-wrap items-center justify-center gap-5 sm:gap-10 xl:gap-20">
							{#each b.data as banner}
								{#if banner.imgCdn}
									<div
										role="banner"
										class="h-[40vw] w-[40vw] overflow-hidden rounded-full shadow-md sm:h-[30vw] sm:w-[30vw] lg:h-[20vw] lg:w-[20vw] xl:h-[15vw] xl:w-[15vw]">
										<a href="{banner.link}" data-sveltekit-prefetch>
											<LazyImg
												src="{banner.imgCdn}"
												alt=""
												width="375"
												class="h-full w-full object-cover object-center" />
										</a>
									</div>
								{/if}
							{/each}
						</div>
					{/if}
				</div>
			{/each}
		</div>
	{/if}

	{#if pickedBanners?.length}
		<div class="flex flex-col gap-5 sm:gap-10">
			{#each pickedBanners as b}
				<div>
					<h1
						class="p-3 py-5 text-center font-serif text-xl font-medium tracking-wider sm:px-10 sm:text-2xl md:py-10 md:text-3xl xl:text-4xl uppercase">
						{b._id?.title}
					</h1>

					{#if b.data?.length}
						<div class="max-w-screen overflow-x-auto scrollbar-none lg:hidden">
							<div role="banner" class="flex flex-row">
								{#each b.data as banner}
									{#if banner.imgCdn}
										<a href="{banner.link}" class="flex-shrink-0" data-sveltekit-prefetch>
											<LazyImg
												src="{banner.imgCdn}"
												alt=""
												width="375"
												class="w-[47vw] object-contain object-top sm:w-60" />
										</a>
									{/if}
								{/each}
							</div>
						</div>

						<div role="banner" class="hidden grid-cols-7 lg:grid">
							{#each b.data as banner}
								{#if banner.imgCdn}
									<a href="{banner.link}" class="col-span-1" data-sveltekit-prefetch>
										<LazyImg
											src="{banner.imgCdn}"
											alt=""
											width="375"
											class="h-full w-full object-contain object-top" />
									</a>
								{/if}
							{/each}
						</div>
					{/if}
				</div>
			{/each}
		</div>
	{/if}
</div>
