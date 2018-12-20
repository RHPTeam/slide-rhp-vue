<template>
	<div id="app"><app-slides /></div>
</template>

<script>
import AppSlides from "@/components/Slides";
export default {
	name: "App",
	components: {
		AppSlides
	}
};
</script>

<style>
#app {
	max-width: 900px;
	margin: 0 auto;
}
</style>
