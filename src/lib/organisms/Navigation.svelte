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

<img class="logo" src="/assets/logo_spatwater.png" alt="logo spatwater" />

<nav>
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
  :global(:has(.navbar-container)) {
    container-type: inline-size;
  }

  * {
    color: none;
  }

  /* Navigation */
  nav {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 70vh;
    background-color: #fff;
    font-family: "Open sans", sans-serif;
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

  /* 
  .cursor {
    position: fixed;
    width: 40px;
    height: 40px;
    background: #4ecd5d;
    border-radius: 50%;
    pointer-events: none;
    transform: translate(-50%, -50%);
    mix-blend-mode: difference;
  } */

  /* & li a span {
    color: white;
    background-color: var(--green);
    padding: 0.5em 1em;
    border-radius: 5px;
  } */

  .logo {
    width: 11rem;
    height: auto;
    margin: 1rem 1rem;
  }

  /* & .menu {
    clear: both;
    height: 0;
    transition: height 0.2s ease-out;
  } */

  nav {
    cursor: pointer;
    color: #fafafa;
    font: 800 3rem;
    transition: 0.5s;
  }
  li a:hover {
    color: rgb(#fafafa);
    text-shadow:
      0 0 5px #abd8ef,
      0 0 25px #abd8ef,
      0 0 50px #abd8ef,
      0 0 100px #abd8ef;
  }

  /* 48em = 768px */
  @container (min-width: 900px) {
    nav li {
      float: left;
      line-height: 10px;
    }

    /* ul li:hover ~ .cursor {
      transform: translate(-50%, -50%) scale(3);
      background: #3ecd5d;
      box-shadow: 0 0 0 100vh #fff;
      /* color: #fff; */

    nav li a {
      padding: 35px 0px;
      font-size: 5rem;
    }

    /* 
    nav .menu {
      clear: none;
      float: right;
      height: auto; /* Adjusted to display the menu on desktop */

    /* nav .menu-icon {
      display: none;
    }

    .logo {
      width: 2rem;
      padding: 4em;
    }
    .cursor {
      position: fixed;
      width: 40px;
      height: 40px;
      background: #4ecd5d;
      border-radius: 50%;
      pointer-events: none;
      transform: translate(-50%, -50%);
      mix-blend-mode: difference;
    } */
  }
</style>
