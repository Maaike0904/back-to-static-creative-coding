<script>
  import { onMount } from "svelte";

  onMount(() => {
    let cursor = document.querySelector(".cursor");
    document.addEventListener("mousemove", (e) => {
      cursor.style.left = e.pageX + "px";
      cursor.style.top = e.pageY + "px";
    });
  });
</script>

<nav>
  <img class="logo" src="/assets/logo_spatwater.png" alt="logo spatwater" />

  <div class="navbar-container">
    <!-- <input class="menu-button" type="checkbox" id="menu-button" /> -->
    <!-- <label class="menu-icon" for="menu-button"><span class="bars"></span></label
    > -->

    <ul class="menu">
      <li><a href="/over">Over</a></li>
      <li><a href="/expertise">Expertise</a></li>
      <li><a href="/#projecten">Projecten</a></li>
      <li><a href="/#kennisbank">Kennisbank</a></li>
      <li><a href="/team">Team</a></li>
      <li><a href="/contact"><span>Contact</span></a></li>
      <div class="cursor"></div>
    </ul>
  </div>
</nav>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;500;600&family=Poppins:wght@400;500;600&display=swap");

  :global(:has(.navbar-container)) {
    container-type: inline-size;
  }

  * {
    cursor: none;
  }

  /* Navigation */
  .navbar-container {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 70vh;
    font-family: "Open sans", sans-serif;
    cursor: pointer;
    color: #fafafa;
    font: 800 2rem;
    line-height: 4em;
    padding: 1em;
  }

  ul {
    position: relative;
    display: flex;
    flex-direction: column;
  }

  ul li {
    list-style: none;
  }

  ul li a {
    position: relative;
    display: inline-block;
    margin: 10px 0;
    font-size: 4em;
    text-decoration: none;
    color: var(--spat);
  }

  .logo {
    width: 11rem;
    height: auto;
    margin: 1rem 1rem;
    z-index: 1;
  }

  /* Hover animatie */
  li a:hover {
    color: rgb(#fafafa);
    text-shadow:
      0 0 5px #abd8ef,
      0 0 25px #abd8ef,
      0 0 50px #abd8ef,
      0 0 100px #abd8ef;
  }

  /* Mediaquery */
  @media (min-width: 900px) {
    /* Nav */
    nav li {
      line-height: 10px;
    }

    /* Bal animatie */
    ul li:hover ~ .cursor {
      /* Vergroting van het balletje */
      transform: translate(-50%, -50%) scale(3);
      background: var(--green);
      box-shadow: 0 0 0 100vh var(--spat);
      color: #fafafa;
    }

    nav li a {
      padding: 35px 0px;
      font-size: 5rem;
    }

    li a:hover {
      animation: none;
    }

    /* Balletje  */
    .cursor {
      position: fixed;
      width: 40px;
      height: 40px;
      background: #4ecd5d;
      border-radius: 50%;
      pointer-events: none;
      transform: translate(-50%, -50%);
      mix-blend-mode: multiply;
    }
  }
</style>
