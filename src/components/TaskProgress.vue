<template>
    <div class="progress">
        <div class="progress-bar" :style="{width: progress + '%'}">
                       
        </div>
        <div class="progress-value">
            <span>{{ progress }}%</span>
        </div>
    </div>
</template>

<script>
export default({
    props: {
        progress: { type: Number, default: 0}
    }    
})
</script>

<style>
	.progress {
        position: relative;
		width: 50%;
		height: 35px;
		border: 2px solid seagreen;
        border-radius: 5px;
		margin-top: 1rem;
        display: flex;
        flex-direction: column;
        align-items: center;
	}

	.progress-bar {
        position: absolute;
		background-color: seagreen;
		height: 100%;
		font-weight: 600;
        align-self: flex-start;
	}

    .progress-value {
        z-index: 1;
        height: 100%;
        display: flex;
        justify-content: center;        
        align-items: center;
    }

    @media screen and (max-width: 768px) {
        .progress {
            width: 75%;
        }
    }

    @media screen and (max-width: 550px) {
        .progress {
            width: 85%;
        }
    }
</style>