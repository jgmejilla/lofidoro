<script>
    import { onMount, onDestroy } from 'svelte';
  
    let player;
    let playing = false;
  
    onMount(() => {
      document.title = "LofiDoro"
      // Load the YouTube IFrame API script
      const tag = document.createElement('script');
      tag.src = "https://www.youtube.com/iframe_api";
      const firstScriptTag = document.getElementsByTagName('script')[0];
      firstScriptTag.parentNode.insertBefore(tag, firstScriptTag);
  
      // Create a new YouTube player when the API is ready
      window.onYouTubeIframeAPIReady = () => {
        player = new YT.Player('player', {
          height: '390',
          width: '640',
          videoId: 'jfKfPfyJRdk',
          events: {
            'onReady': onPlayerReady,
            'onStateChange': onPlayerStateChange
          }
        });
      };
  
      return () => {
        // Clean up the player when the component is destroyed
        if (player) {
          player.destroy();
        }
      };
    });
  
    function onPlayerReady(event) {
      event.target.playVideo();
    }
  
    function onPlayerStateChange(event) {
      // Handle player state changes if needed
    }

    function playVideo() {
        if (player) {
        player.playVideo();
        }
    }

    function pauseVideo() {
        if (player) {
            player.pauseVideo();
        }
    }

    function toggleMusic() {
        if (playing) {
            pauseVideo()
        } else {
            playVideo()
        }
        playing = !playing
    }
</script>
  
<style>
    #player {
        display: none;
    }
    .music-player {
    
        display: flex;
        flex-direction: column;
        align-items: center;
        margin: 10px;
    }

</style>
  
<div id="player"></div>

<div class="music-player">
<div class="controls">
    
    <button on:click={toggleMusic}>
    {#if playing}
        ||
    {:else}
        ▷
    {/if}
    </button>
</div>
</div>

