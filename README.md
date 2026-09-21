<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Para Natalia</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Caveat:wght@500;600;700&family=Nunito:wght@400;600&display=swap" rel="stylesheet">
<style>
  :root {
    box-sizing: border-box;
    padding-top: env(safe-area-inset-top, 0px);
    padding-bottom: env(safe-area-inset-bottom, 0px);
    --sky-top-night: #0a0f2b;
    --sky-mid-night: #141b45;
    --sky-bottom-night: #232a52;
    --sky-top-day: #6fc3ea;
    --sky-mid-day: #9adcf0;
    --sky-bottom-day: #cdeffb;
    --moon: #f6ecc9;
    --moon-glow: rgba(246, 236, 201, 0.35);
    --sun: #ffc93c;
    --sun-glow: rgba(255, 201, 60, 0.45);
    --petal: #ffcf3f;
    --petal-shade: #f0b21e;
    --petal-core: #7a4a1e;
    --leaf: #356b3d;
    --leaf-dark: #234c2a;
    --ground-night: #101a30;
    --ground-day-top: #7ec25a;
    --ground-day-bottom: #4f9640;
    --ink: #3c2a14;
    --paper: #fffaf0;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  html, body {
    height: 100%;
    overflow: hidden;
    background: var(--sky-top-night);
  }

  body {
    font-family: 'Nunito', sans-serif;
    position: relative;
    cursor: pointer;
    -webkit-tap-highlight-color: transparent;
  }

  .sky {
    position: fixed;
    inset: 0;
    background: linear-gradient(to bottom, var(--sky-top-night) 0%, var(--sky-mid-night) 55%, var(--sky-bottom-night) 100%);
    transition: background 2.4s ease;
  }

  body.is-day .sky {
    background: linear-gradient(to bottom, var(--sky-top-day) 0%, var(--sky-mid-day) 55%, var(--sky-bottom-day) 100%);
  }

  .stars {
    position: fixed;
    inset: 0;
    transition: opacity 1.4s ease;
  }

  body.is-day .stars {
    opacity: 0;
  }

  .star {
    position: absolute;
    width: 2px;
    height: 2px;
    background: #fef6da;
    border-radius: 50%;
    animation: twinkle 3.4s ease-in-out infinite;
  }

  @keyframes twinkle {
    0%, 100% { opacity: 0.25; }
    50% { opacity: 1; }
  }

  .moon {
    position: fixed;
    top: 10%;
    right: 14%;
    width: 74px;
    height: 74px;
    border-radius: 50%;
    background: var(--moon);
    box-shadow: 0 0 50px 14px var(--moon-glow);
    transition: transform 2.2s cubic-bezier(.4,0,.2,1), opacity 1.8s ease;
  }

  .moon::before, .moon::after {
    content: '';
    position: absolute;
    border-radius: 50%;
    background: rgba(180, 160, 110, 0.28);
  }

  .moon::before {
    width: 16px;
    height: 16px;
    top: 14px;
    left: 12px;
  }

  .moon::after {
    width: 10px;
    height: 10px;
    top: 40px;
    left: 42px;
  }

  body.is-day .moon {
    transform: translateY(-140px);
    opacity: 0;
  }

  .sun {
    position: fixed;
    top: 12%;
    left: 16%;
    width: 84px;
    height: 84px;
    border-radius: 50%;
    background: var(--sun);
    box-shadow: 0 0 70px 20px var(--sun-glow);
    opacity: 0;
    transform: translateY(60px) scale(0.7);
    transition: opacity 2s ease 0.3s, transform 2s cubic-bezier(.2,.8,.3,1) 0.3s;
  }

  body.is-day .sun {
    opacity: 1;
    transform: translateY(0) scale(1);
  }

  .cloud {
    position: fixed;
    background: #ffffff;
    border-radius: 100px;
    opacity: 0;
    transition: opacity 1.8s ease 0.6s, transform 6s ease-in-out;
  }

  .cloud::before, .cloud::after {
    content: '';
    position: absolute;
    background: #ffffff;
    border-radius: 50%;
  }

  .cloud-a {
    top: 18%;
    left: -10%;
    width: 120px;
    height: 34px;
  }

  .cloud-a::before { width: 60px; height: 60px; top: -30px; left: 14px; }
  .cloud-a::after { width: 44px; height: 44px; top: -20px; left: 60px; }

  .cloud-b {
    top: 28%;
    right: -8%;
    width: 90px;
    height: 26px;
  }

  .cloud-b::before { width: 46px; height: 46px; top: -22px; left: 10px; }
  .cloud-b::after { width: 34px; height: 34px; top: -14px; left: 44px; }

  body.is-day .cloud-a {
    opacity: 0.92;
    transform: translateX(60px);
  }

  body.is-day .cloud-b {
    opacity: 0.85;
    transform: translateX(-40px);
  }

  .ground {
    position: fixed;
    left: 0;
    right: 0;
    bottom: 0;
    height: 30vh;
    background: var(--ground-night);
    transition: background 2s ease;
  }

  body.is-day .ground {
    background: linear-gradient(to bottom, var(--ground-day-top), var(--ground-day-bottom));
  }

  .field {
    position: fixed;
    left: 0;
    right: 0;
    bottom: 8vh;
    height: 28vh;
    display: flex;
    align-items: flex-end;
    justify-content: center;
    gap: clamp(6px, 3.5vw, 34px);
    pointer-events: none;
  }

  .flower {
    position: relative;
    width: 15vw;
    max-width: 84px;
    min-width: 46px;
  }

  .flower:nth-child(2) { transform: translateY(6%); }
  .flower:nth-child(4) { transform: translateY(4%); }
  .flower:nth-child(3) { transform: scale(1.16); }

  .stem {
    position: absolute;
    bottom: 0;
    left: 50%;
    width: 5px;
    height: 60%;
    background: var(--leaf-dark);
    transform: translateX(-50%);
    transform-origin: bottom center;
    border-radius: 3px;
    transition: background 1.6s ease;
  }

  body.is-day .stem {
    background: var(--leaf);
  }

  .leaf {
    position: absolute;
    width: 22px;
    height: 11px;
    background: var(--leaf-dark);
    border-radius: 0 100% 0 100%;
    bottom: 28%;
    transition: background 1.6s ease;
  }

  .leaf.left { left: -10px; transform: rotate(20deg); }
  .leaf.right { right: -10px; transform: rotate(-20deg) scaleX(-1); bottom: 20%; }

  body.is-day .leaf {
    background: var(--leaf);
  }

  .head {
    position: absolute;
    bottom: 56%;
    left: 50%;
    width: 40px;
    height: 40px;
    transform: translate(-50%, 50%);
  }

  .bud {
    position: absolute;
    inset: 0;
    background: var(--leaf-dark);
    border-radius: 50% 50% 50% 50% / 62% 62% 38% 38%;
    transform-origin: bottom center;
    transition: transform 1.1s cubic-bezier(.5,0,.3,1), opacity 0.6s ease 0.5s;
  }

  .bud::after {
    content: '';
    position: absolute;
    inset: 5px 5px 9px 5px;
    background: var(--petal-shade);
    border-radius: 50% 50% 50% 50% / 60% 60% 40% 40%;
  }

  body.is-day .bud {
    transform: scaleY(0.15) translateY(40%);
    opacity: 0;
  }

  .petals {
    position: absolute;
    inset: 0;
    opacity: 0;
    transform: scale(0.2) rotate(-30deg);
    transition: transform 1.3s cubic-bezier(.34,1.4,.4,1) 0.55s, opacity 0.8s ease 0.55s;
  }

  body.is-day .petals {
    opacity: 1;
    transform: scale(1) rotate(0deg);
  }

  .petal {
    position: absolute;
    top: 50%;
    left: 50%;
    width: 15px;
    height: 22px;
    background: var(--petal);
    border-radius: 50% 50% 50% 50% / 60% 60% 40% 40%;
    transform-origin: 50% 100%;
  }

  .petal:nth-child(1) { transform: translate(-50%, -100%) rotate(0deg); }
  .petal:nth-child(2) { transform: translate(-50%, -100%) rotate(45deg); }
  .petal:nth-child(3) { transform: translate(-50%, -100%) rotate(90deg); }
  .petal:nth-child(4) { transform: translate(-50%, -100%) rotate(135deg); }
  .petal:nth-child(5) { transform: translate(-50%, -100%) rotate(180deg); }
  .petal:nth-child(6) { transform: translate(-50%, -100%) rotate(225deg); }
  .petal:nth-child(7) { transform: translate(-50%, -100%) rotate(270deg); }
  .petal:nth-child(8) { transform: translate(-50%, -100%) rotate(315deg); }

  .core {
    position: absolute;
    top: 50%;
    left: 50%;
    width: 16px;
    height: 16px;
    background: var(--petal-core);
    border-radius: 50%;
    transform: translate(-50%, -50%);
    box-shadow: inset 0 -2px 3px rgba(0,0,0,0.25);
  }

  .hint {
    position: fixed;
    left: 0;
    right: 0;
    bottom: calc(5vh + env(safe-area-inset-bottom, 0px));
    text-align: center;
    color: #e9e3c9;
    font-size: 0.95rem;
    letter-spacing: 0.02em;
    opacity: 0.75;
    animation: float 2.6s ease-in-out infinite;
    transition: opacity 0.8s ease;
  }

  body.is-day .hint {
    opacity: 0;
  }

  @keyframes float {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-6px); }
  }

  .message {
    position: fixed;
    top: 40%;
    left: 50%;
    transform: translate(-50%, -40%) scale(0.85);
    font-family: 'Caveat', cursive;
    font-size: clamp(2.6rem, 9vw, 5rem);
    color: var(--ink);
    text-shadow: 0 2px 18px rgba(255,255,255,0.5);
    opacity: 0;
    text-align: center;
    pointer-events: none;
    transition: opacity 1.4s ease 1.3s, transform 1.4s cubic-bezier(.2,.9,.3,1.1) 1.3s;
    white-space: nowrap;
  }

  body.is-day .message {
    opacity: 1;
    transform: translate(-50%, -50%) scale(1);
  }

  @media (max-width: 420px) {
    .message {
      white-space: normal;
      width: 80%;
    }
  }

  @media (prefers-reduced-motion: reduce) {
    .star, .hint { animation: none; }
    * { transition-duration: 0.3s !important; }
  }
</style>
</head>
<body>

<div class="sky"></div>
<div class="stars" id="stars"></div>
<div class="moon"></div>
<div class="sun"></div>
<div class="cloud cloud-a"></div>
<div class="cloud cloud-b"></div>
<div class="ground"></div>

<div class="field">
  <div class="flower">
    <div class="stem"></div>
    <div class="leaf left"></div>
    <div class="head">
      <div class="bud"></div>
      <div class="petals">
        <div class="petal"></div><div class="petal"></div><div class="petal"></div><div class="petal"></div>
        <div class="petal"></div><div class="petal"></div><div class="petal"></div><div class="petal"></div>
        <div class="core"></div>
      </div>
    </div>
  </div>
  <div class="flower">
    <div class="stem"></div>
    <div class="leaf right"></div>
    <div class="head">
      <div class="bud"></div>
      <div class="petals">
        <div class="petal"></div><div class="petal"></div><div class="petal"></div><div class="petal"></div>
        <div class="petal"></div><div class="petal"></div><div class="petal"></div><div class="petal"></div>
        <div class="core"></div>
      </div>
    </div>
  </div>
  <div class="flower">
    <div class="stem"></div>
    <div class="leaf left"></div>
    <div class="leaf right"></div>
    <div class="head">
      <div class="bud"></div>
      <div class="petals">
        <div class="petal"></div><div class="petal"></div><div class="petal"></div><div class="petal"></div>
        <div class="petal"></div><div class="petal"></div><div class="petal"></div><div class="petal"></div>
        <div class="core"></div>
      </div>
    </div>
  </div>
  <div class="flower">
    <div class="stem"></div>
    <div class="leaf left"></div>
    <div class="head">
      <div class="bud"></div>
      <div class="petals">
        <div class="petal"></div><div class="petal"></div><div class="petal"></div><div class="petal"></div>
        <div class="petal"></div><div class="petal"></div><div class="petal"></div><div class="petal"></div>
        <div class="core"></div>
      </div>
    </div>
  </div>
  <div class="flower">
    <div class="stem"></div>
    <div class="leaf right"></div>
    <div class="head">
      <div class="bud"></div>
      <div class="petals">
        <div class="petal"></div><div class="petal"></div><div class="petal"></div><div class="petal"></div>
        <div class="petal"></div><div class="petal"></div><div class="petal"></div><div class="petal"></div>
        <div class="core"></div>
      </div>
    </div>
  </div>
</div>

<p class="hint">toca la pantalla</p>
<p class="message">Para mi amorcito</p>

<script>
var starsContainer = document.getElementById('stars');
var total = 90;
for (var i = 0; i < total; i++) {
  var star = document.createElement('div');
  star.className = 'star';
  star.style.left = (Math.random() * 100) + 'vw';
  star.style.top = (Math.random() * 62) + 'vh';
  star.style.animationDelay = (Math.random() * 3.4) + 's';
  var size = Math.random() < 0.15 ? 3 : 2;
  star.style.width = size + 'px';
  star.style.height = size + 'px';
  starsContainer.appendChild(star);
}

document.body.addEventListener('click', function () {
  document.body.classList.toggle('is-day');
});
</script>

</body>
</html>
