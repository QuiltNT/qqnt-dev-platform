<script setup lang="ts">
import { ref } from 'vue';
import Versions from './components/Versions.vue';

const version = window.version;
const isMaximized = ref(false);

const close = () => window.api.close();
const maximize = () => {
	const max = isMaximized.value;
	max? window.api.unmaximize(): window.api.maximize();
	isMaximized.value = !max;
}
const minimize = () => window.api.minimize();

</script>

<template>
	<v-app>
		<v-layout>
			<v-system-bar window>
				<span class="title">QQNT Plugin Development Platform by QuiltNT - v{{ version }}</span>

				<v-spacer></v-spacer>

				<v-btn class="control-btn" icon="mdi-minus" variant="text" @click.prevent="minimize"></v-btn>
				<v-btn class="control-btn ms-2" :icon="isMaximized? 'mdi-checkbox-multiple-blank-outline': 'mdi-checkbox-blank-outline'" variant="text" @click.prevent="maximize"></v-btn>
				<v-btn class="control-btn ms-2" icon="mdi-close" variant="text" @click.prevent="close"></v-btn>
			</v-system-bar>
		</v-layout>
		<Versions />
	</v-app>
</template>

<style lang="scss" scoped>
.v-system-bar {
	display: flex;
	align-items: center;
	font-size: 1rem;
	padding: 1.2rem;
	user-select: none;
	-webkit-app-region: drag;
	>.control-btn {
		-webkit-app-region: no-drag;
	}
}
main {
	margin-top: 1.8rem;
	overflow: auto;
}
</style>
