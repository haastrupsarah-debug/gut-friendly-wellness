# gut-friendly-wellness
A modern health‑tech inspired web app designed to support people with food intolerances (including lactose intolerance), common food allergies, and acid reflux. 
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <title>Gut-Friendly Wellness</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />

  <style>
    :root {
      --bg-dark: linear-gradient(135deg, #020617, #0f172a, #064e3b);
      --bg-light: linear-gradient(135deg, #ecfdf5, #e0f2fe, #eef2ff);
      --card-dark: rgba(255,255,255,0.06);
      --card-light: rgba(255,255,255,0.9);
      --text-dark: #ffffff;
      --text-light: #0f172a;
      --accent: #34d399;
      --danger: #fb7185;
    }

    body {
      margin: 0;
      font-family: system-ui, sans-serif;
      min-height: 100vh;
      transition: all 0.3s ease;
    }

    body.dark {
      background: var(--bg-dark);
      color: var(--text-dark);
    }


    body.light {
      background: var(--bg-light);
      color: var(--text-light);
    }

    header {
      max-width: 1100px;
      margin: auto;
      padding: 1.5rem;
      display: flex;
      justify-content: space-between;
      align-items: center;
    }

    h1 {
      font-size: 2.2rem;
    }

    button {
      padding: 0.6rem 1rem;
      border-radius: 10px;
      border: 1px solid rgba(255,255,255,0.2);
      background: transparent;
      color: inherit;
      cursor: pointer;
    }

    nav {
      display: flex;
      justify-content: center;
      gap: 1rem;
      margin-bottom: 2rem;
    }

    .container {
      max-width: 1100px;
      margin: auto;
      padding: 1rem;
    }

    .grid {
      display: grid;
      gap: 1.5rem;
    }

    .two {
      grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    }

    .card {
      padding: 1.2rem;
      border-radius: 16px;
      backdrop-filter: blur(12px);
      transition: transform 0.2s ease;
    }

    body.dark .card {
      background: var(--card-dark);
    }

    body.light .card {
      background: var(--card-light);
    }

    .card:hover {
      transform: translateY(-4px);
    }

    .hidden {
      display: none;
    }

    input {
      width: 100%;
      padding: 0.7rem;
      border-radius: 10px;
      border: none;
      margin-top: 0.5rem;
    }

    .success {
      color: var(--accent);
      margin-top: 1rem;
      font-weight: bold;
    }

    .error {
      color: var(--danger);
      margin-top: 1rem;
      font-weight: bold;
    }

    footer {
      text-align: center;
      opacity: 0.7;
      margin: 3rem 0 1rem;
    }
  </style <.food-layer {
  position: fixed;
  inset: 0;
  overflow: hidden;
  pointer-events: none;
  z-index: 0;
}

.food {
  position: absolute;
  font-size: 2.2rem;
  opacity: 0.25;
  animation: float 18s linear infinite;
}

.food:nth-child(1) { left: 10%; animation-duration: 22s; }
.food:nth-child(2) { left: 25%; animation-duration: 18s; }
.food:nth-child(3) { left: 45%; animation-duration: 25s; }
.food:nth-child(4) { left: 65%; animation-duration: 20s; }
.food:nth-child(5) { left: 80%; animation-duration: 24s; }
.food:nth-child(6) { left: 90%; animation-duration: 19s; }

@keyframes float {
  from {
    transform: translateY(110vh) rotate(0deg);
  }
  to {
    transform: translateY(-20vh) rotate(360deg);
  }
}

/* Ensure content stays above animation */
header, nav, .container, footer {
  position: relative;
  z-index: 1;
}
> 
</head>

<body class="dark">

  <!-- Floating food animations -->
<div class="food-layer">
  <span class="food">🍓</span>
  <span class="food">🥑</span>
  <span class="food">🍌</span>
  <span class="food">🥦</span>
  <span class="food">🍎</span>
  <span class="food">🥕</span>
</div>


<header>
  <h1>Gut-Friendly Wellness</h1>
  <button onclick="toggleTheme()">🌗</button>
</header>

<nav>
  <button onclick="showTab('home')">Home</button>
  <button onclick="showTab('planner')">Planner</button>
  <button onclick="showTab('checker')">Checker</button>
</nav>

<div class="container">

  <!-- HOME -->
  <section id="home" class="grid two">
    <div class="card">
      <h3>Dietary Focus</h3>
      <ul>
        <li>Lactose-free</li>
        <li>Gluten-free</li>
        <li>Vegan & Halal options</li>
        <li>Low-FODMAP friendly</li>
      </ul>
    </div>

    <div class="card">
      <h3>Reflux Tips</h3>
      <ul>
        <li>Eat smaller meals</li>
        <li>Avoid lying down after eating</li>
        <li>Stay upright during exercise</li>
        <li>Track personal trigger foods</li>
      </ul>
    </div>
  </section>

  <!-- PLANNER -->
  <section id="planner" class="grid two hidden">
    <div class="card">
      <h3>Weekly Meal Plan</h3>
      <ul>
        <li>Oatmeal with banana & chia</li>
        <li>Grilled chicken & quinoa</li>
        <li>Baked salmon & sweet potato</li>
        <li>Tofu & rice stir fry</li>
      </ul>
    </div>

    <div class="card">
      <h3>Weekly Workout Plan</h3>
      <ul>
        <li>Mon – Low impact walking</li>
        <li>Wed – Upper body strength</li>
        <li>Fri – Reflux-safe yoga</li>
      </ul>
    </div>
  </section>

  <!-- CHECKER -->
  <section id="checker" class="hidden">
    <div class="card">
      <h3>Is this reflux-safe?</h3>
      <input id="foodInput" placeholder="e.g. tomato pasta" />
      <div id="result"></div>
    </div>
  </section>

</div>

<footer>
  Portfolio project · Modern health-tech UI
</footer>

<script>
  const triggers = ["tomato", "coffee", "chocolate", "spicy", "fried", "alcohol", "citrus"];

  function toggleTheme() {
    document.body.classList.toggle("dark");
    document.body.classList.toggle("light");
  }

  function showTab(tab) {
    ["home", "planner", "checker"].forEach(id =>
      document.getElementById(id).classList.add("hidden")
    );
    document.getElementById(tab).classList.remove("hidden");
  }

  document.getElementById("foodInput").addEventListener("input", (e) => {
    const value = e.target.value.toLowerCase();
    const result = document.getElementById("result");

    if (!value) {
      result.innerHTML = "";
      return;
    }

    const unsafe = triggers.some(t => value.includes(t));
    result.innerHTML = unsafe
      ? "<div class='error'>May trigger acid reflux</div>"
      : "<div class='success'>Likely reflux-safe</div>";
  });
</script>

</body>
</html>
