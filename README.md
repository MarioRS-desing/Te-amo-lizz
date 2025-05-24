# Te-amo-lizz
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Lluvia + Salpicadura Te Amo</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      background: #fbeaff;
      overflow: hidden;
      height: 100vh;
      font-family: sans-serif;
      position: relative;
    }

    .corazon-contenedor {
      position: fixed;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      font-size: 150px;
      animation: latido 1s infinite;
      z-index: 10;
      pointer-events: none;
      user-select: none;
    }

    .frase {
      position: absolute;
      font-size: 24px;
      color: #ff1493;
      pointer-events: none;
      user-select: none;
      z-index: 5;
      white-space: nowrap;
      will-change: transform, opacity;
    }

    @keyframes latido {
      0%, 100% {
        transform: translate(-50%, -50%) scale(1);
      }
      50% {
        transform: translate(-50%, -50%) scale(1.3);
      }
    }
  </style>
</head>
<body>

  <div class="corazon-contenedor">🩵</div>

  <script>
    const corazonCentroX = window.innerWidth / 2;
    const corazonAncho = 150;
    const corazonMinX = corazonCentroX - corazonAncho / 2;
    const corazonMaxX = corazonCentroX + corazonAncho / 2;

    // Crea un "te amo" que cae desde arriba, evitando caer sobre el corazón
    function crearFraseLluvia() {
      const frase = document.createElement("div");
      frase.classList.add("frase");
      frase.innerText = "te amo";

      let x;
      do {
        x = Math.random() * window.innerWidth;
      } while (x > corazonMinX && x < corazonMaxX);

      frase.style.left = x + "px";
      frase.style.top = "-30px";

      frase.style.transition = "transform 4s linear, opacity 4s linear";
      document.body.appendChild(frase);

      requestAnimationFrame(() => {
        frase.style.transform = `translateY(110vh)`;
        frase.style.opacity = "0";
      });

      setTimeout(() => frase.remove(), 4000);
    }

    // Lluvia MUCHO más densa
    setInterval(crearFraseLluvia, 50); // más rápido, más frases

    // Salpicadura tipo agua en el punto tocado
    function salpicarTeAmo(event) {
      const x = event.clientX || event.touches[0].clientX;
      const y = event.clientY || event.touches[0].clientY;
      const cantidad = 40;

      for (let i = 0; i < cantidad; i++) {
        const frase = document.createElement("div");
        frase.classList.add("frase");
        frase.innerText = "te amo";
        frase.style.left = x + "px";
        frase.style.top = y + "px";

        const angle = Math.random() * 2 * Math.PI;
        const distance = 50 + Math.random() * 150;
        const duration = 1000 + Math.random() * 1000;

        frase.style.transition = `transform ${duration}ms ease-out, opacity ${duration}ms ease-out`;

        document.body.appendChild(frase);

        requestAnimationFrame(() => {
          frase.style.transform = `translate(${Math.cos(angle) * distance}px, ${Math.sin(angle) * distance}px)`;
          frase.style.opacity = "0";
        });

        setTimeout(() => {
          frase.remove();
        }, duration);
      }
    }

    document.addEventListener("click", salpicarTeAmo);
    document.addEventListener("touchstart", salpicarTeAmo);
  </script>

</body>
</html>
