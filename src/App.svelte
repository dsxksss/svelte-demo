<script>
  import { onMount } from "svelte";

  let characters = ["💕", "❤️", "✨", "雷"];

  let confetti = new Array(100)
    .fill()
    .map((_, i) => {
      return {
        character: characters[i % characters.length],
        x: Math.random() * 100,
        y: -20 - Math.random() * 100,
        r: 0.1 + Math.random() * 1,
      };
    })
    .sort((a, b) => a.r - b.r);

  onMount(() => {
    let frame;

    function loop() {
      frame = requestAnimationFrame(loop);

      confetti = confetti.map((emoji) => {
        emoji.y += 0.7 * emoji.r;
        if (emoji.y > 120) emoji.y = -20;
        return emoji;
      });
    }

    loop();

    return () => cancelAnimationFrame(frame);
  });
</script>

{#each confetti as c}
  <span style="left: {c.x}%; top: {c.y}%; transform: scale({c.r})"
    >{c.character}</span
  >
{/each}
<div class="center">
  <spen class="context">给 我 唱 歌</spen>
</div>

<style>
  :global(body) {
    overflow: hidden;
    color: lightcoral;
  }

  span {
    position: absolute;
    font-size: 5vw;
    user-select: none;
  }

  .center {
    display: flex;
    height: 100vh;
    justify-content: center;
    align-items: center;
  }

  .context {
    font-size: 18rem;
  }
</style>
