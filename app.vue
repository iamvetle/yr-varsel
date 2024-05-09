<template>
	<div>
		<div v-if="apiSvgUrl" id="divGuy">
			<!-- {{ apiSvgUrl }} -->
			<img :src="apiSvgUrl" id="theImg"/>

		</div>
		<div v-else>
			<p>No data yet</p>
		</div>
	</div>
</template>

<script setup lang="ts">
	const apiSvgUrl = ref<any>(null);

    const url = "https://www.yr.no/en/content/1-2715300/meteogram.svg";
	const delay = 5000;

	const intervalID = ref<any>(null);

	const fetchData = () => {
		console.debug("fetchData called from setInterval")

		apiSvgUrl.value = null
		apiSvgUrl.value = url
	};

	onMounted(async () => {
		fetchData()
    console.debug("on mounted run")
		intervalID.value = setInterval(fetchData, delay);
	});

	onUnmounted(() => {
		if (intervalID.value) {
			clearInterval(intervalID.value);
		}
	});
</script>


<style scoped>

#theImg {
	width: 80%;
}

#divGuy {
	display: flex;
	justify-content:center;
}

</style>