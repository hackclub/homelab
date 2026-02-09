<script lang="ts">
	import hackClubFlag from '$lib/assets/hack-club-flag.svg';
	import homelabLogo from '$lib/assets/homelab-logo.svg';
	import gridPattern from '$lib/assets/grid-pattern.png';

	const faqItems = [
		{
			question: 'When does it end?',
			answer: 'February 9th, 11:59 EST'
		},
		{
			question: 'What counts as a home server related project?',
			answer: `We are fairly open to this, however creating a random project that is "hosted on a home server" doesn't count. This means you can't build an unrelated website and just claim you can host it on a home server. Instead, ideas include a website that lets you automate tasks and processes on your network, a file explorer based on storage on a NAS, etc. You could also do a hardware project such as a 3d printed server rack.`
		},
		{
			question: 'Are there any requirements for participating?',
			answer: 'You must be YSWS eligible (18 years or under) and a participant of Hack Club.'
		},
		{
			question: 'Can I double dip?',
			answer: 'This program is not double dippable.'
		},
		{
			question: 'Can I use AI?',
			answer: `Using AI is okay, and AI assisted coding is acceptable only if disclosed. Most of the code should be written by you (<=30% can be AI). READMEs must be human written. AI generated slop is unacceptable.`
		}
	];

	const submissionRequirements = [
		'Video demo of your project',
		'Clear setup/install instructions',
		'Good commit history (or, alternatively, a well documented timeline/devlog)',
		'If AI was used, it should be disclosed. Also mention how it was used.'
	];

	const tabs = [
		{ id: 'faqs', label: 'FAQs', disabled: false },
		{ id: 'rewards', label: 'Rewards (TBD)', disabled: true },
		{ id: 'ship', label: 'Ship', link: 'https://submit.hackclub.com/homelab' }
	];

	let activeTab = $state('faqs');
</script>

<div class="relative flex min-h-screen items-center justify-center">
	<!-- Background -->
	<div class="pointer-events-none absolute inset-0">
		<div class="absolute inset-0 bg-linear-to-b from-[#1e1e1e] from-[66.7%] to-[#1f314d]"></div>
		<div
			class="absolute inset-0 bg-size-[960px_960px] bg-top-left opacity-[0.06]"
			style="background-image: url('{gridPattern}')"
		></div>
	</div>

	<!-- Body -->
	<div class="relative flex w-full max-w-[640px] flex-col gap-6 px-6 py-24">
		<!-- Logo Section -->
		<div class="flex flex-col gap-2">
			<img src={hackClubFlag} alt="Hack Club" class="h-[26px] w-[74px]" />
			<img src={homelabLogo} alt="Homelab" class="h-[40px] w-[239px]" />
			<p class="font-mono text-base text-white">Build projects that run on your homelab @ home</p>
		</div>

		<!-- Content -->
		<div class="flex flex-col gap-4">
			<!-- Nav -->
			<nav class="flex items-center gap-6">
				{#each tabs as tab}
					<button
						onclick={() => {
							if (tab.link) {
								window.location.href = tab.link;
							} else if (!tab.disabled) {
								activeTab = tab.id;
							}
						}}
						class="font-mono text-base font-semibold cursor-pointer {activeTab === tab.id
							? 'bg-white px-2 py-0.5 text-black'
							: tab.disabled
								? 'text-[#8B8B8B] underline'
								: 'text-white underline'}"
						disabled={tab.disabled}
					>
						{tab.label}
					</button>
				{/each}
			</nav>

			<!-- FAQ Body -->
			<div
				class="flex flex-col gap-4 border-4 border-white p-6 font-mono text-white"
			>
				{#each faqItems as { question, answer }, i}
					<div class="flex flex-col gap-1">
						<p class="text-base font-semibold">{question}</p>
						<p class="text-s">{answer}</p>
					</div>
					{#if i < faqItems.length - 1}
						<hr class="border-white/30" />
					{/if}
				{/each}

				<!-- Requirements -->
				<div class="flex flex-col gap-1">
					<p class="text-base font-semibold">Requirements for submitting</p>
					<ul class="list-disc pl-5 text-s">
						{#each submissionRequirements as requirement}
							<li>{requirement}</li>
						{/each}
					</ul>
				</div>
			</div>
		</div>
	</div>
</div>