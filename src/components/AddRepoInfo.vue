<template>
	<form class="rinp-card">
		<input
			type="text"
			name="rname"
			placeholder="Reposit Name"
			class="rinp-txt"
			autofocus
			v-model="rname"
		/>
		<input
			type="text"
			name="rdate"
			placeholder="Reposit Date"
			class="rinp-txt"
			onfocus="(this.type='date')"
			onfocusout="(this.type='text')"
			v-model="rdate"
		/>
		<input
			type="text"
			name="rtype"
			placeholder="Reposit Type"
			class="rinp-txt"
			@focus="vrtype = true"
			v-if="!vrtype"
		/>
		<div class="w-full text-xl" v-if="vrtype">
			<Listbox v-model="rtype">
				<div class="relative mt-1">
					<ListboxButton
						class="relative w-full cursor-default rounded-lg bg-white py-2 pl-3 pr-10 text-left shadow-md focus:outline-none focus-visible:border-indigo-500 focus-visible:ring-2 focus-visible:ring-white focus-visible:ring-opacity-75 focus-visible:ring-offset-2 focus-visible:ring-offset-orange-300"
					>
						<span class="block truncate">{{ rtype }}</span>
						<span
							class="pointer-events-none absolute inset-y-0 right-0 flex items-center pr-2"
						>
							<SelectorIcon class="h-5 w-5 text-gray-400" aria-hidden="true" />
						</span>
					</ListboxButton>

					<transition
						leave-active-class="transition duration-100 ease-in"
						leave-from-class="opacity-100"
						leave-to-class="opacity-0"
					>
						<ListboxOptions
							class="absolute mt-1 max-h-60 w-full overflow-auto rounded-md bg-white py-1 text-base shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none"
						>
							<ListboxOption value="Reposit Type" disabled>
								<span class="block truncate ml-4 my-4 font-light"
									>Reposit Type</span
								>
							</ListboxOption>
							<ListboxOption
								v-slot="{ active, selected }"
								v-for="repoType in repoTypes"
								:key="repoType"
								:value="repoType"
								as="template"
							>
								<li
									:class="[
										active ? 'bg-amber-100 text-amber-900' : 'text-gray-900',
										'relative cursor-default select-none py-2 pl-10 pr-4',
									]"
								>
									<span
										:class="[
											selected ? 'font-medium' : 'font-normal',
											'block truncate',
										]"
										>{{ repoType }}</span
									>
									<span
										v-if="selected"
										class="absolute inset-y-0 left-0 flex items-center pl-3 text-amber-600"
									>
										<CheckIcon class="h-5 w-5" aria-hidden="true" />
									</span>
								</li>
							</ListboxOption>
						</ListboxOptions>
					</transition>
				</div>
			</Listbox>
		</div>
		<textarea
			name="rsubj"
			class="rinp-txt resize-y h-auto"
			@input="rsubjAutoGrow"
			@focusout="rsubjResetGrow"
			@focus="rsubjAutoGrow"
			placeholder="Reposit Subject"
			v-model="rsubj"
		></textarea>
	</form>
</template>

<script lang="ts">
import {
	Listbox,
	ListboxButton,
	ListboxOptions,
	ListboxOption,
} from '@headlessui/vue';
import { SelectorIcon, CheckIcon } from '@heroicons/vue/outline';
export default {
	name: 'AddRepoInfo',
	components: {
		Listbox,
		ListboxButton,
		ListboxOptions,
		ListboxOption,
		SelectorIcon,
		CheckIcon,
	},
	data() {
		return {
			repoTypes: ['a', 'b', 'c'],
			rtype: 'a',
			rname: '',
			rdate: '',
			rsubj: '',
			vrtype: false,
		};
	},
	methods: {
		rsubjAutoGrow(e: any) {
			this.rsubjResetGrow(e);
			e.target.style.cssText = 'height:' + e.target.scrollHeight + 'px';
		},
		rsubjResetGrow(e: any) {
			e.target.style.cssText = 'height:auto; padding:0; padding-block:8px;';
		},
	},
};
</script>

<style scoped>
.rinp-txt {
	@apply text-center rounded-md text-2xl py-2 w-full shadow-md;
}
.rinp-card {
	@apply bg-slate-100 flex flex-col space-y-10 px-5 py-10 mx-2 my-8 rounded-2xl sm:mx-5 shadow-sm;
}
/* .rinp-card,
.rinp-txt {
	@apply focus:outline-none focus-visible:border-indigo-500 focus-visible:ring-2 focus-visible:ring-white focus-visible:ring-opacity-75 focus-visible:ring-offset-2 focus-visible:ring-offset-orange-300;
} */
</style>
