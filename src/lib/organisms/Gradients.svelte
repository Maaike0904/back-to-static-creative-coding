<script>
  import { onMount } from "svelte";

  onMount(() => {});
</script>

<main>
  <div class="card">
    <!-- Klimaatadaptatie card -->
    <div class="expertise__card">
      <img
        src="assets/Untitled4.png"
        alt="Illustratie klimaatadaptatie voor een groenere wereld"
        width="200px"
        height="200px"
      />
      <h3>Klimaatadaptatie</h3>
    </div>
  </div>
</main>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;500;600&family=Poppins:wght@400;500;600&display=swap");

  @property --rotate {
    syntax: "<angle>";
    initial-value: 132deg;
    inherits: false;
  }

  :root {
    --card-height: 65vh;
    --card-width: calc(var(--card-height) / 1.5);
  }

  main {
    display: flex;
    align-items: center;
    flex-direction: column;
    padding-top: 4em;
  }

  img {
    filter: blur(5px);
    filter: grayscale(100%);
  }

  img:hover {
    filter: none;
    filter: drop-shadow(0px 0px 30px var(--green));
  }
  /* body {
    min-height: 100vh;
    background: #212534;
    display: flex;
    align-items: center;
    flex-direction: column;
    padding-top: 2rem;
    padding-bottom: 2rem;
    box-sizing: border-box;
  } */

  .card {
    background: #191c29;
    width: var(--card-width);
    height: var(--card-height);
    padding: 3px;
    position: relative;
    border-radius: 6px;
    justify-content: center;
    align-items: center;
    text-align: center;
    display: flex;
    font-size: 1.5em;
    color: rgb(88 199 250 / 0%);
    cursor: pointer;
    font-family: cursive;
  }

  .card:hover {
    color: var(--spat);
    transition: color 1s;
    filter: none;
  }
  .card:hover:before,
  .card:hover:after {
    animation: none;
    opacity: 0;
  }

  .card::before {
    content: "";
    width: 104%;
    height: 102%;
    border-radius: 8px;
    background-image: linear-gradient(
      var(--rotate),
      var(--green),
      var(--spat) 43%,
      var(--darkblue)
    );
    position: absolute;
    z-index: -1;
    top: -1%;
    left: -2%;
    animation: spin 2.5s linear infinite;
  }

  .card::after {
    position: absolute;
    content: "";
    top: calc(var(--card-height) / 6);
    left: 0;
    right: 0;
    z-index: -1;
    height: 100%;
    width: 100%;
    margin: 0 auto;
    transform: scale(0.8);
    filter: blur(calc(var(--card-height) / 6));
    background-image: linear-gradient(
      var(--rotate),
      var(--green),
      var(--spat) 43%,
      var(--darkblue)
    );
    opacity: 1;
    transition: opacity 0.5s;
    animation: spin 2.5s linear infinite;
  }

  @keyframes spin {
    0% {
      --rotate: 0deg;
    }
    100% {
      --rotate: 360deg;
    }
  }

  a {
    color: #212534;
    text-decoration: none;
    font-family: sans-serif;
    font-weight: bold;
    margin-top: 2rem;
  }
  .expertise__card {
    height: 22em;
    width: 15em;
    border-radius: 4px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    /* box-shadow: 0 8px 10px rgba(174, 190, 205, 0.3); */
    /* background-color: var(--lg-bg); */
    /* color: var(--darkblue); */
    /* transition: transform 0.3s ease-in; */
    cursor: pointer;
  }
</style>
