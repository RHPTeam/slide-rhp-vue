<template>
	<div class="slides">
		<div
			class="slides--inner"
			:style="{
				width: innerWidth + 'px',
				marginLeft: '-' + slideInnerMarginLeft + 'px'
			}"
		>
			<app-slide
				v-for="(slide, index) in slides"
				:style="{ width: singleWidth + 'px ' }"
				:slide="slide"
				:key="index"
			/>
		</div>
		<div class="actions">
			<span @click="prev">Prev</span>
			<span
				class="action--number"
				:class="[index === currentIndex ? 'active' : '']"
				v-for="(slide, index) in slides"
				:key="index"
				@click="goToSlide(index)"
				>{{ index + 1 }}</span
			>
			<span @click="next">Next</span>
		</div>
	</div>
</template>

<script>
import AppSlide from "@/components/Slide";
export default {
	props: {
		itemsPerSlide: {
			type: null,
			default: 1
		}
	},
	data() {
		return {
			slides: [
				{ src: "static/img/slide01.jpg" },
				{ src: "static/img/slide02.jpg" },
				{ src: "static/img/slide03.jpg" },
				{ src: "static/img/slide04.jpg" },
				{ src: "static/img/slide05.jpg" },
				{ src: "static/img/slide06.jpg" }
			],
			innerWidth: 0,
			singleWidth: 0,
			currentIndex: 0
		};
	},
	methods: {
		prev() {
			if (this.currentIndex === 0) return;
			this.currentIndex--;
		},
		next() {
			if (this.currentIndex === this.slides.length - 1) return;
			this.currentIndex++;
		},
		goToSlide(index) {
			this.currentIndex = index;
		}
	},
	computed: {
		slideInnerMarginLeft() {
			return this.currentIndex * this.singleWidth;
		}
	},
	components: {
		AppSlide
	},
	mounted() {
		this.$nextTick(() => {
			let singleWidth = this.$el.clientWidth / this.itemsPerSlide;
			this.$set(this.$data, "singleWidth", singleWidth);
			this.$set(this.$data, "innerWidth", singleWidth * this.slides.length);
		});
	}
};
</script>

<style scoped>
span {
	cursor: pointer;
}

.slides {
	overflow: hidden;
	text-align: center;
}

.slide--inner {
	transition: margin 0.6s ease-out;
}

.actions {
	margin: 10px 0 0 0;
}

.action--number {
	margin: 0 5px;
	background-color: #fff;
	padding: 0 5px;
	border: 1px solid #000;
	cursor: pointer;
}

.action--number.active {
	color: #fff;
	background: #000;
}
</style>
