<template>
	<Modal
		width="540px"
		:title="$locale.baseText('about.aboutN8n')"
		:eventBus="modalBus"
		:name="ABOUT_MODAL_KEY"
		:center="true"
	>
		<template #content>
			<div :class="$style.container">
				<el-row>
					<el-col :span="8" class="info-name">
						<n8n-text>{{ $locale.baseText('about.n8nVersion') }}</n8n-text>
					</el-col>
					<el-col :span="16">
						<n8n-text>{{ rootStore.versionCli }}</n8n-text>
					</el-col>
				</el-row>
				<el-row>
					<el-col :span="8" class="info-name">
						<n8n-text>{{ $locale.baseText('about.sourceCode') }}</n8n-text>
					</el-col>
					<el-col :span="16">
						<n8n-link to="https://github.com/n8n-io/n8n">https://github.com/n8n-io/n8n</n8n-link>
					</el-col>
				</el-row>
				<el-row>
					<el-col :span="8" class="info-name">
						<n8n-text>{{ $locale.baseText('about.license') }}</n8n-text>
					</el-col>
					<el-col :span="16">
						<n8n-link to="https://github.com/n8n-io/n8n/blob/master/packages/cli/LICENSE.md">
							{{ $locale.baseText('about.n8nLicense') }}
						</n8n-link>
					</el-col>
				</el-row>
				<el-row>
					<el-col :span="8" class="info-name">
						<n8n-text>{{ $locale.baseText('about.instanceID') }}</n8n-text>
					</el-col>
					<el-col :span="16">
						<n8n-text>{{ rootStore.instanceId }}</n8n-text>
					</el-col>
				</el-row>
			</div>
		</template>

		<template #footer>
			<div class="action-buttons">
				<n8n-button @click="closeDialog" float="right" :label="$locale.baseText('about.close')" />
			</div>
		</template>
	</Modal>
</template>

<script lang="ts">
import Vue from 'vue';
import Modal from './Modal.vue';
import { ABOUT_MODAL_KEY } from '../constants';
import { mapStores } from 'pinia';
import { useSettingsStore } from '@/stores/settings';
import { useRootStore } from '@/stores/n8nRootStore';
import { createEventBus } from '@/event-bus';

export default Vue.extend({
	name: 'About',
	components: {
		Modal,
	},
	data() {
		return {
			ABOUT_MODAL_KEY,
			modalBus: createEventBus(),
		};
	},
	computed: {
		...mapStores(useRootStore, useSettingsStore),
	},
	methods: {
		closeDialog() {
			this.modalBus.emit('close');
		},
	},
});
</script>

<style module lang="scss">
.container > * {
	margin-bottom: var(--spacing-s);
	overflow-wrap: break-word;
}
</style>
