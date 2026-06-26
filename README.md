index.html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Para mi amiguita haru❤ ✨</title>
    <style>
        * { padding: 0; margin: 0; box-sizing: border-box; }
        body {
            background-color: #ffe6eb;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            flex-direction: column;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            overflow: hidden;
        }
        .container { position: relative; width: 280px; height: 180px; }
        .envelope {
            position: absolute; top: 0; left: 0;
            width: 280px; height: 180px;
            background-color: #f9c5c8;
            box-shadow: 0 4px 20px rgba(0,0,0,0.15);
            border-bottom-left-radius: 6px;
            border-bottom-right-radius: 6px;
            z-index: 1;
        }
        .envelope::before {
            content: ''; position: absolute; top: 0; left: 0; z-index: 4;
            border-left: 140px solid transparent; border-right: 140px solid transparent;
            border-bottom: 90px solid #f6b3b7; border-top: 90px solid transparent;
            border-bottom-left-radius: 6px; border-bottom-right-radius: 6px;
        }
        .envelope::after {
            content: ''; position: absolute; top: 0; left: 0; z-index: 5;
            border-left: 140px solid #f5a3a8; border-right: 140px solid transparent;
            border-bottom: 90px solid transparent; border-top: 90px solid transparent;
        }
        .flap {
            position: absolute; top: 0; left: 0; width: 0; height: 0;
            border-left: 140px solid transparent; border-right: 140px solid transparent;
            border-top: 90px solid #e08b90; border-bottom: 90px solid transparent;
            transform-origin: top; transition: transform 0.4s ease, z-index 0.2s;
            z-index: 6;
        }
        .letter {
            position: absolute; top: 20px; left: 20px;
            width: 240px; height: 140px;
            background-color: #fff; padding: 12px;
            border-radius: 4px; box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            text-align: center; display: flex; flex-direction: column; justify-content: center;
            opacity: 0; transform: translateY(40px);
            transition: transform 0.5s ease-in-out, opacity 0.3s ease-in-out;
            z-index: 2;
            pointer-events: none;
        }
        .letter p {
            font-size: 11px; color: #d1495b; font-weight: bold; line-height: 1.4;
            max-height: 120px; overflow-y: auto; padding-right: 5px;
        }
        .container.open .flap { transform: rotateX(180deg); z-index: 0; }
        .container.open .letter {
            opacity: 1; transform: translateY(-110px);
            z-index: 7; pointer-events: auto;
        }
        .buttons {
            margin-top: 60px; display: flex; gap: 15px;
            position: relative; z-index: 10;
        }
        button {
            padding: 10px 20px; border: none; background-color: #e08b90;
            color: white; font-size: 12px; font-weight: bold;
            letter-spacing: 1px; border-radius: 4px; cursor: pointer;
            box-shadow: 0 4px 6px rgba(0,0,0,0.1); transition: background 0.2s;
        }
        button:hover { background-color: #d1495b; }
        .heart {
            position: absolute; background-color: #d1495b;
            display: inline-block; height: 20px; width: 20px;
            transform: rotate(-45deg); opacity: 0; z-index: 8;
        }
        .heart::before, .heart::after {
            content: ""; background-color: #d1495b;
            border-radius: 50%; height: 20px; position: absolute; width: 20px;
        }
        .heart::before { top: -10px; left: 0; }
        .heart::after { left: 10px; top: 0; }
        @keyframes floatUp {
            0% { transform: translateY(0) rotate(-45deg) scale(0.5); opacity: 1; }
            100% { transform: translateY(-220px) rotate(-45deg) scale(1.2); opacity: 0; }
        }
    </style>
</head>
<body>

    <!-- REPRODUCTOR DE AUDIO OCULTO -->
    <audio id="backgroundMusic" src="cinderalla.mp3" loop></audio>

    <div class="container" id="envelopeContainer">
        <div class="flap"></div>
        <div class="envelope"></div>
        <div class="letter">
            <p>¡Haruuu! ✨<br>¡Feliz cumpleaños, Gianella! 🎂 Bienvenido sea al club de los 20. Quería escribirte para desearte un día increíble y decirte que, aunque llevamos poco tiempo de conocernos, te has convertido en alguien súper especial para mí. Tienes una luz increíble y da mucho gusto tenerte cerca. Pásala genial hoy con tu familia y amigos, ¡y que este año se venga lleno de puras cosas buenas amiguita te hice esto con mucho cariño aunque seas media loquita y me de ganas de darte un puñete JAJA! 🥳🎈 ❤️</p>
        </div>
    </div>
    <div class="buttons">
        <button onclick="openEnvelope()">OPEN</button>
        <button onclick="closeEnvelope()">RESET</button>
    </div>
    <script>
        const container = document.getElementById('envelopeContainer');
        const music = document.getElementById('backgroundMusic');

        function openEnvelope() {
            container.classList.add('open');
            
            // INTENTA REPRODUCIR LA MÚSICA AL ABRIR
            if(music) {
                music.play().catch(error => {
                    console.log("El navegador bloqueó el audio automático inicialmente:", error);
                });
            }

            for (let i = 0; i < 6; i++) { setTimeout(createHeart, i * 250); }
        }
        
        function closeEnvelope() { 
            container.classList.remove('open'); 
            
            // PAUSA LA MÚSICA SI CIERRA EL SOBRE (Opcional)
            if(music) {
                music.pause();
                music.currentTime = 0; // Reinicia la canción al segundo 0
            }
        }

        function createHeart() {
            if (!container.classList.contains('open')) return;
            const heart = document.createElement('div');
            heart.classList.add('heart');
            heart.style.left = Math.random() * 200 + 40 + 'px';
            heart.style.bottom = '40px';
            heart.style.animation = 'floatUp 1.5s linear forwards';
            container.appendChild(heart);
            setTimeout(() => heart.remove(), 1500);
        }
    </script>
</body>
</html>
