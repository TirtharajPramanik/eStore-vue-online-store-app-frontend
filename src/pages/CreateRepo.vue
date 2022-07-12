<template>
	<Navbar navHeader="Create Reposit" />
	<div class="w-full max-w-lg px-2 py-12 m-auto sm:px-0 flex flex-col">
		<TabGroup>
			<TabList class="flex space-x-1 rounded-xl bg-blue-200/20 p-1">
				<Tab v-for="tab in tabs" as="template" :key="tab" v-slot="{ selected }">
					<button
						:class="[
							'transition ease-in-out duration-150',
							'w-full rounded-lg py-2.5 text-sm font-medium leading-5 text-slate-500',
							// 'ring-white ring-opacity-60 ring-offset-2 ring-offset-blue-400 focus:outline-none focus:ring-2',
							selected
								? 'bg-white shadow'
								: 'text-blue-50 hover:bg-white/[0.12] hover:text-white',
						]"
					>
						{{ tab }}
					</button>
				</Tab>
			</TabList>
			<TabPanels class="mt-2">
				<TabPanel
					:class="[
						'rounded-xl bg-white pt-4',
						// 'ring-white ring-opacity-60 ring-offset-2 ring-offset-blue-400 focus:outline-none focus:ring-2',
					]"
				>
					<AddRepoInfo />
				</TabPanel>
			</TabPanels>
		</TabGroup>
		<button type="button" class="rbtn bg-sky-50">Next</button>
	</div>
</template>

<script lang="ts">
import { TabGroup, TabList, Tab, TabPanels, TabPanel } from '@headlessui/vue';
import Navbar from '@/components/Navbar.vue';
import AddRepoInfo from '../components/AddRepoInfo.vue';

export default {
	components: {
		Navbar,
		TabGroup,
		TabList,
		Tab,
		TabPanels,
		TabPanel,
		AddRepoInfo,
	},
	data() {
		return {
			tabs: ['Reposit Info', 'Reposit Content'],
		};
	},
};
</script>

<style>
.rbtn {
	@apply text-center rounded-md text-xl w-max px-6 py-2 mx-auto mt-4 text-blue-400 shadow-sky-200 shadow-sm hover:bg-orange-200 hover:text-white hover:shadow-lg transition-all;
}
</style>
