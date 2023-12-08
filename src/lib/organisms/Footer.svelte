<script>
  import { onMount } from "svelte";

  onMount(() => {
    console.log("Hello World");

    // Canvas id word aangesproken
    var canvas = document.getElementById("canvas");
    //  Hier wordt de 2D-context van het canvas verkregen en toegewezen aan de variabele c. Deze context wordt vaak gebruikt voor het tekenen van grafische elementen op het canvas.
    var c = canvas.getContext("2d");
    // Breedte van het canvcas geef je een variabele
    var tx = window.innerWidth;
    // Hoogte van het canvas geef je een variabele
    var ty = window.innerHeight;
    canvas.width = tx;
    canvas.height = ty;

    // Plek van de muis word gevolgd
    var mousex = 0;
    var mousey = 0;

    addEventListener("mousemove", function () {
      mousex = event.clientX;
      mousey = event.clientY;
    });

    // "zwaartekracht"
    var grav = 0.99;

    // Roze kleur word ingesteld
    function pinkColor() {
      return "rgba(255, 192, 203, 0.6)"; // Roze kleur met 60% transparantie (0.6)
    }

    // Er word een functie aangemaakt voor het ball element
    function Ball() {
      // De roze kleur word aangesproken die we eerder hebben ingesteld
      this.color = pinkColor();
      // De radius wordt ingesteld op een willekeurige waarde tussen 14 en 34 (20 + 14), waardoor de straal van de bal varieert.
      this.radius = Math.random() * 20 + 14;
      // Hier wordt startradius ingesteld op dezelfde waarde als radius op het moment dat hij word aangemaakt. Dit lijkt te worden gebruikt om de oorspronkelijke straal van de bal te onthouden.
      this.startradius = this.radius;
      //  De x-positie (this.x) wordt willekeurig ingesteld binnen het canvas, rekening houdend met de grootte van de bal.
      this.x = Math.random() * (tx - this.radius * 2) + this.radius;
      // Dit hetzelfde als voor de x-positie
      this.y = Math.random() * (ty - this.radius);
      // De dy (delta-y) eigenschap wordt ingesteld op een willekeurige waarde tussen 0 en 2, wat de verticale snelheid van de bal voorstelt.
      this.dy = Math.random() * 2;
      //  De dx (delta-x) eigenschap wordt ingesteld op een willekeurige waarde tussen -5 en 5, de horizontale snelheid van de bal.
      this.dx = Math.round((Math.random() - 0.5) * 10);
      // De vel (snelheid) eigenschap wordt ingesteld op een willekeurige waarde tussen 0 en 0.2. Dit is de snelheid van de bal.
      this.vel = Math.random() / 5;
      // Een methode genaamd update wordt gedefinieerd op het balobject. Deze methode wordt gebruikt om de weergave van de bal bij te werken op basis van zijn huidige eigenschappen.
      this.update = function () {
        // Bal word getekend met de waardes die we hierboven hebben ingesteld
        c.beginPath();
        c.arc(this.x, this.y, this.radius, 0, 2 * Math.PI);
        c.fillStyle = this.color;
        c.fill();
      };
    }

    // Hier wordt een lege array genaamd bal gedeclareerd. Deze array zal worden gebruikt om de balobjecten op te slaan.
    var bal = [];
    // Dit is een for-lus die 50 keer wordt doorlopen. De lus heeft een teller i die begint bij 0 en wordt verhoogd met 1 bij elke iteratie. De lus zal doorgaan zolang i kleiner is dan 50.
    for (var i = 0; i < 50; i++) {
      // Binnen de lus wordt een nieuwe instantie van het Ball object gemaakt met behulp van de constructorfunctie Ball(). Deze nieuwe instantie wordt vervolgens toegevoegd aan de array bal met behulp van de push-methode
      bal.push(new Ball());
    }

    // Deze functie word gebruikt om een animatie te maken op basis van de eerder gedefinieerde ballen en hun gedrag.
    function animate() {
      if (tx != window.innerWidth || ty != window.innerHeight) {
        tx = window.innerWidth;
        ty = window.innerHeight;
        canvas.width = tx;
        canvas.height = ty;
      }
      // Deze blok code controleert of de breedte (tx) of hoogte (ty) van het venster zijn gewijzigd sinds de laatste frame. Als dat het geval is, worden de variabelen tx en ty bijgewerkt met de actuele breedte en hoogte van het venster, en het canvas wordt opnieuw ingesteld op deze nieuwe grootte.

      // Dit vraagt de browser aan om de functie animate opnieuw aan te roepen voordat de volgende repaint plaatsvindt. Hiermee wordt een soepele animatieloop gemaakt.
      requestAnimationFrame(animate);
      // Dit zorgt ervoor dat het canvas aan het begin van elk frame wordt gewist om de oude posities van de ballen te verwijderen voordat de bijgewerkte posities worden getekend.
      c.clearRect(0, 0, tx, ty);
      // Deze for-lus itereert over alle ballen in de array bal en voert een reeks bewerkingen uit op elk balobject.
      for (var i = 0; i < bal.length; i++) {
        // Dit roept de update-methode aan voor het huidige balobject. Deze methode was eerder gedefinieerd in de Ball constructor en is verantwoordelijk voor het tekenen van de bal op het canvas.
        bal[i].update();
        // Hier worden de x- en y-posities van elk balobject bijgewerkt op basis van hun snelheid (dy en dx).
        bal[i].y += bal[i].dy;
        bal[i].x += bal[i].dx;
        // Dit deel controleert of de bal de onderkant van het canvas heeft bereikt. Als dat het geval is, wordt de verticale snelheid (dy) omgekeerd (vermenigvuldigd met -1) en vermenigvuldigd met de zwaartekrachtconstante (grav).
        if (bal[i].y + bal[i].radius >= ty) {
          bal[i].dy = -bal[i].dy * grav;
        }
        // Als de bal nog niet de onderkant heeft bereikt, wordt de verticale snelheid verhoogd met de snelheid (vel) van de bal.
        else {
          bal[i].dy += bal[i].vel;
        }
        // Hier wordt gecontroleerd of de bal de rechter- of linkergrens van het canvas heeft bereikt. Als dat het geval is, wordt de horizontale snelheid (dx) omgekeerd (vermenigvuldigd met -1).
        if (bal[i].x + bal[i].radius > tx || bal[i].x - bal[i].radius < 0) {
          bal[i].dx = -bal[i].dx;
        }
        // Hier wordt gecontroleerd of de muis zich binnen een bepaald gebied rondom een bal bevindt (mousex en mousey worden gebruikt om de muispositie bij te houden). Als dat het geval is en de straal van de bal is kleiner dan 70, wordt de straal van de bal met 5 verhoogd. Anders, als de straal groter is dan de oorspronkelijke straal, wordt de straal met 5 verminderd. Dit creëert een interactie waarbij ballen groter worden als de muis zich in de buurt bevindt, en kleiner als dat niet het geval is.
        if (
          mousex > bal[i].x - 20 &&
          mousex < bal[i].x + 20 &&
          mousey > bal[i].y - 50 &&
          mousey < bal[i].y + 50 &&
          bal[i].radius < 70
        ) {
          bal[i].radius += 5;
        } else {
          if (bal[i].radius > bal[i].startradius) {
            bal[i].radius += -5;
          }
        }
      }
    }

    animate();
    //  Deze intervalfunctie voegt elke 400 milliseconden een nieuwe bal toe aan de bal-array en verwijdert tegelijkertijd de oudste bal uit de array. Het resultaat is dat er elke 400 milliseconden een nieuwe bal wordt gecreëerd, en na verloop van tijd zal het aantal ballen in de array constant blijven, omdat er één wordt toegevoegd en één wordt verwijderd.
    setInterval(function () {
      // Voegt een nieuwe bal toe aan het einde van de bal-array door een nieuw Ball-object te maken met behulp van de constructorfunctie Ball() en het toe te voegen aan het einde van de array met push.
      bal.push(new Ball());
      // Verwijdert het eerste element uit de bal-array (index 0) met behulp van splice. Hierdoor blijft het aantal ballen in de array constant, wat een visueel effect creëert waarbij het lijkt alsof nieuwe ballen continu worden gegenereerd en de oudste ballen verdwijnen.
      bal.splice(0, 1);
    }, 400);
  });

  export let data;
  console.log(data);
</script>

<canvas id="canvas"></canvas>
<section class="container">
  <article>
    <h2>SPATwater</h2>
    <h3>Een nieuwe generatie hydrologen</h3>
    <svg
      xmlns="http://www.w3.org/2000/svg"
      width="44"
      height="44"
      viewBox="0 0 44 44"
      fill="none"
    >
      <path
        d="M33.6163 33.6215H28.7296V25.964C28.7296 24.138 28.6926 21.7882 26.1831 21.7882C23.6353 21.7882 23.2461 23.7752 23.2461 25.8293V33.6215H18.3593V17.875H23.0536V20.0213H23.1168C23.7728 18.7838 25.3678 17.4776 27.7506 17.4776C32.7021 17.4776 33.6178 20.7365 33.6178 24.9783L33.6163 33.6215ZM12.8401 15.7204C11.2671 15.7204 10.0035 14.4471 10.0035 12.881C10.0035 11.3163 11.2685 10.0444 12.8401 10.0444C14.4076 10.0444 15.6781 11.3163 15.6781 12.881C15.6781 14.4471 14.4063 15.7204 12.8401 15.7204ZM15.2904 33.6215H10.3899V17.875H15.2904V33.6215ZM36.0611 5.5H7.93689C6.59077 5.5 5.50177 6.56425 5.50177 7.87738V36.1227C5.50177 37.437 6.59077 38.5 7.93689 38.5H36.0571C37.4018 38.5 38.5018 37.437 38.5018 36.1227V7.87738C38.5018 6.56425 37.4018 5.5 36.0571 5.5H36.0611Z"
        fill="white"
      />
    </svg>
  </article>

  <article>
    <h2>Over</h2>
    <ul>
      <li><a href="#over">Over ons</a></li>
      <li><a href="#klimaatadaptatie">Klimaatadaptatie</a></li>
      <li><a href="#waterkwaliteit">Waterkwaliteit</a></li>
      <li><a href="#brain">b-RAIN</a></li>
      <li><a href="#projecten">Projecten</a></li>
      <li><a href="#kennisbank">Kennisbank</a></li>
    </ul>
  </article>

  <article>
    <h2>Bedrijf</h2>
    <ul>
      <li><a href="#team">Team</a></li>
    </ul>
  </article>

  <article>
    <h2>Contact</h2>
    <ul>
      <li><a href="#contact">Neem contact op</a></li>
    </ul>
  </article>
</section>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Montserrat:&display=swap");

  body {
    margin: 0px;
    overflow: hidden;
  }

  #canvas {
    margin-bottom: -30em;
    margin-top: -25em;
  }

  h2 {
    color: white;
    font-size: 1.3rem;
    padding-bottom: 1rem;
    font-family: "Montserrat", sans-serif;

    animation-duration: 1000ms;
    animation-timing-function: linear;
    animation-iteration-count: infinite;
    animation-direction: alternate;
    animation-name: font-animation;
  }

  @keyframes font-animation {
    0% {
      font-variation-settings:
        "wght" 100,
        "ROND" 1;
    }
    100% {
      font-variation-settings:
        "wght" 1000,
        "ROND" 100;
    }
  }

  /* @Keyframes font-animation {
0% {
font-variation-settings: "wght" 100;
}
100% {
font-variation-settings: "wght" 900;
}
} */

  h3 {
    color: white;
    font-size: 1rem;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
  }

  svg {
    width: 1.7rem;
    margin-top: 0.5rem;
    margin-left: -0.3em;
  }

  ul {
    list-style-type: none;
    text-decoration: none;
    cursor: pointer;
  }

  li,
  a {
    text-decoration: none;
    color: white;
    cursor: pointer;
    padding-bottom: 0.5rem;
    font-size: 0.9rem;
    font-family: Verdana, Geneva, Tahoma, sans-serif;
    z-index: 1;
  }

  section {
    height: 100vh;
    /* background-color: var(--darkblue); */
    background-image: url("./assets/curved-footer.png");
  }

  .container {
    padding: 2rem;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    padding-top: 6em;
    padding-bottom: 24em;
  }

  @media screen and (min-width: 720px) {
    h2 {
      margin-bottom: 1.5rem;
      margin-top: 2rem;
    }
    section {
      height: 50vh;
    }
    .container {
      flex-direction: row;
    }

    li {
      margin-bottom: 0.5rem;
    }
  }
</style>
