<template>
	<div id="GameCanvas-wrapper">
		<canvas id="gameCanvas" width="300" height="500"></canvas>
	</div>
</template>

<script>
import axios from "axios";

export default {
	name: "GameCanvas",
	inject: ["newScoreObject"],
	mounted() {
		require("../../js/game.js");
		window.addEventListener(
			"game:over",
			async function(e) {
				let newScore = {
					score: e.detail.score,
				};
				this.$emit("newScore", newScore);
				await axios.post("/newScore", this.newScoreObject);
				this.$emit("postedNewScoreToServer");
			}.bind(this)
		);
	},
};
</script>

<style lang="scss" scoped>
#GameCanvas-wrapper {
	display: flex;
	justify-content: center;
}

#gameCanvas {
	border: 1px solid black;
}
</style>
