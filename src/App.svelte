<script lang="ts">
  import Slide from "./components/Slide.svelte";
  import SlideButton from "./components/SlideButton.svelte";

  let slides: string[][] = [
    // ["# TKC", "\nTesting", "\n\nTesting", "\n> 123"],
    // ["# TKC2", "\nTesting", "\n\nTesting", "\n> 123"],
    [
      "# Svelte",
      "\n\n>Cybernetically enhanced web apps",
      `
\`\`\`

       WTF?
       /
  ¯\\_(ツ)_/¯
\`\`\``,
    ],
    ["# Why?"],
    [
      ">The virtual DOM === 🐌",
      "\n\nIt is pretty cool though...",
      "\n\n>Do the pro's still outweigh the cons?",
    ],
    [
      ">The virtual DOM turns 🔋",
      " into 💀",
      "\n\n<image src='https://c.tenor.com/8iSobq9-6UsAAAAM/dave-tyrone-dave.gif'/>\n\nY'all got any more of them mAh?",
    ],
    [
      "\n\n>React === 🧐",
      "🤯",
      "🥔",
      "\n\n2013 called, they want their framework back",
      "\n\n<image src='https://resources.stuff.co.nz/content/dam/images/1/k/c/e/s/v/image.related.StuffLandscapeSixteenByNine.1240x700.1keazd.png/1499990640977.jpg?format=pjpg&optimize=medium'/>",
    ],
    [
      "# Vue",
      "\n\n> Client side CPU cycles = 💀🔋",
      "\n\nSo? its still better than React right? Smart diffing FTW!",
      "> Bundle sizes = ",
    ],
    [
      "# Enter Svelte\n\n<image src='https://e7.pngegg.com/pngimages/553/714/png-clipart-t-shirt-sunglasses-t-shirt-angle-lens-thumbnail.png' />",
    ],
    ["FIN"],
  ];

  function clampedIncrement(i: number, array: any[]) {
    return Math.min(i + 1, array.length - 1);
  }

  function clampedDecrement(i: number, array: any[]) {
    return Math.max(i - 1, 0);
  }

  let slideIndex: number = 0;
  let currentSlide: string[] = slides[slideIndex];

  let contentIndex: number = 0;
  let currentContent: string = currentSlide[contentIndex];

  function buildMarkdown(i: number) {
    // whaddup, we is teh functional programmer now ¯\_(ツ)_/¯
    return currentSlide.reduce(
      (previousValue: string, currentValue: string, currentIndex: number) => {
        return currentIndex <= contentIndex
          ? previousValue.concat(currentValue)
          : previousValue;
      }
    );
  }

  function resetSlideStatus() {
    currentSlide = slides[slideIndex];
    contentIndex = 0;
    currentContent = buildMarkdown(contentIndex);
  }

  function slideButtonNotify(event) {
    if (event.detail === "forward") {
      slideIndex = clampedIncrement(slideIndex, slides);
    } else if (event.detail === "backward") {
      slideIndex = clampedDecrement(slideIndex, slides);
    }
    resetSlideStatus();
  }

  function handleClick(event: MouseEvent) {
    event.preventDefault();
    if (event.button === 0) {
      contentIndex = clampedIncrement(contentIndex, currentSlide);
    } else if (event.button === 2) {
      contentIndex = clampedDecrement(contentIndex, currentSlide);
    }
    currentContent = buildMarkdown(contentIndex);
  }

  function handleScroll(event: WheelEvent) {
    event.preventDefault();
    if (event.deltaY < 0) {
      slideIndex = clampedIncrement(slideIndex, slides);
    } else if (event.deltaY > 0) {
      slideIndex = clampedDecrement(slideIndex, slides);
    }
    resetSlideStatus();
  }
</script>

<main
  on:click={handleClick}
  on:contextmenu={handleClick}
  on:wheel={handleScroll}
>
  <SlideButton
    on:slideButtonNotify={slideButtonNotify}
    buttonDirection="backward"
  />
  <Slide markdown={currentContent} />
  <SlideButton
    on:slideButtonNotify={slideButtonNotify}
    buttonDirection="forward"
  />
</main>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Montserrat&family=Raleway&display=swap");

  :global(:root) {
    --pal-primary: #fe7f2d;
    --pal-secondary: #619b8a;
    --pal-highlight: #fcca46;
    --pal-bg-dark: #233d4d;
    --pal-bg-light: #a1c181;
  }

  main {
    height: 100%;
    width: 100%;
    background-color: var(--pal-bg-dark);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: var(--pal-secondary);
    transition: all 300ms;
    overflow: hidden;
    cursor: pointer;
  }

  :global(h1, h2, h3, h4, h5, h6, p, code) {
    -webkit-touch-callout: none;
    -webkit-user-select: none;
    -khtml-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
  }

  :global(h1, h2, h3, h4, h5, h6) {
    font-family: "Montserrat", sans-serif;
    color: var(--pal-primary);
  }

  :global(h1) {
    font-size: 6rem;
  }
  :global(h2) {
    font-size: 5rem;
  }
  :global(h3) {
    font-size: 4rem;
  }
  :global(h4) {
    font-size: 3rem;
  }
  :global(h5) {
    font-size: 2rem;
  }
  :global(h6) {
    font-size: 1rem;
  }
  :global(img) {
    max-height: 50%;
    max-width: 50%;
    border-radius: 1em;
  }

  :global(p) {
    font-family: "Raleway", sans-serif;
    color: inherit;
    font-size: 2rem;
  }

  :global(code) {
    font-size: 2rem;
  }

  :global(blockquote) {
    color: var(--pal-highlight);
  }
  :global(blockquote > p) {
    font-size: 3rem;
  }
</style>
