<script>

    import { onMount } from "svelte";

	import Card from "$lib/components/card.svelte"

	let buttons = [
		{
			name: "Train",
			image: "img/train.png",
			sound: "audio/train.wav",
            key: "a",
            isClicked: false
		},
		{
			name: "Golfer",
			image: "img/golf.png",
			sound: "audio/golf.wav",
            key: "s",
            isClicked: false
		},
		{
			name: "Bell",
			image: "img/bell.png",
			sound: "audio/bell.wav",
            key: "d",
            isClicked: false
		},
		{
			name: "Gun",
			image: "img/gun.png",
			sound: "audio/gun.wav",
            key: "f",
            isClicked: false
		},
		{
			name: "Toilet",
			image: "img/toilet.png",
			sound: "audio/toilet.wav",
            key: "g",
            isClicked: false
		}
	]

	onMount(() => {
		document.addEventListener('keydown', (event) => {
			playMyAudio(event.key)
		})
		document.addEventListener('keyup', (event) => {
			setTimeout(() =>{
				buttons = buttons.map(btn => {
					btn.isClicked = false;
					return btn;
				})
				stopMyAudio(event.key)
			}, 200)
		})
	})

	function playMyAudio(keyCode){
        const button = buttons.filter(btn => btn.key == keyCode).shift();
		if(button){
			let myAudio = new Audio(button.sound);
			myAudio.play();
		}
		buttons = buttons.map(btn => {
			if(btn.key === keyCode) btn.isClicked = true;
			return btn;
		})
    }

    function stopMyAudio(keyCode){
		const button = buttons.filter(btn => btn.key == keyCode).shift();
		if(button){
			let myAudio = new Audio(button.sound);
			myAudio.pause();
		}
	}

</script>

<section class="font-sans pt-5">

	<section class="mt-10 flex flex-wrap mx-auto w-3/4 gap-5 justify-center">
		{#each buttons as button}
			<Card button={button} />
		{/each}
	</section>
	
</section>