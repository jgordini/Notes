	.game-container {
		position: relative;
		overflow: hidden;
		width: 100%;
		padding-top: 100%;
	}
	
	.responsive-iframe {
		position: absolute;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		border: 0;
	}

<style>
	@media screen and (max-width: 800px) {
		.game-container {
			position: relative;
			display: block;
			overflow: hidden;
			width: 100%;
			height: 0;
			padding-top: 157%;
		}
	}

	.game-container {
		position: relative;
		overflow: hidden;
		width: 100%;
		padding-top: 100%;
	}
		.responsive-iframe iframe {
			position: absolute;
			display: block;
			top: 0;
			width: 100%;
			height: 100%;
		}
	</style>
	<div class="game-container">
		<div class="responsive-iframe">
			<iframe src="https://uab-it.github.io/games/2021-phone-toss/" id="embededGame" allow="fullscreen"></iframe>
		</div>
	</div>