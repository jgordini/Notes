	OLD 
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

New 


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
	
		@media screen and (min-width: 801px) {
			.game-container {
				position: relative;
				overflow: hidden;
				width: 100%;
				padding-top: 90%;
			}
		}
		.responsive-iframe iframe {
			position: absolute;
			display: block;
			top: 0;
			width: 100%;
			height: 100%;
		}
	</style>