<script>
	import 'tailwindcss/tailwind.css';
	import { page } from '$app/stores';
	import { browser } from '$app/environment';
	import { sidebarOpen, closeSidebar } from './store';

	import TopBar from './TopBar.svelte';
	import Overlay from './Overlay.svelte';
	import Sidebar from './sidebar/Sidebar.svelte';
	const style = {
		open: 'lg:w-full',
		close: 'lg:pl-4 lg:w-[calc(100%-16rem)]',
		mainContainer: `flex flex-col w-full h-screen pl-0 lg:space-y-4`,
		container: `bg-gray-100 h-screen overflow-hidden relative`,
		main: `h-screen overflow-auto pb-36 pt-8 px-2 md:pb-8 md:pt-4 lg:pt-0`
	};

	if (browser) {
		page.subscribe(() => {
			if ($sidebarOpen && window.innerWidth < 1024) {
				closeSidebar();
			}
		});
	}
</script>

<div class={style.container}>
	<div class="flex items-start">
		<Overlay />
		<Sidebar mobileOrientation="end" />
		<div class={`${style.mainContainer} ${$sidebarOpen ? style.open : style.close}`}>
			<TopBar />
			<main class={style.main}>
				<slot />
			</main>
		</div>
	</div>
</div>
