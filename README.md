<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Warframe Eidolon Hunt Guide</title>
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background-color: #0b0c10;
      color: #c5c6c7;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 50px;
    }

    .container {
      background-color: #1f2833;
      border-radius: 12px;
      box-shadow: 0 0 20px rgba(0,0,0,0.5);
      padding: 30px;
      width: 500px;
    }

    h1 {
      color: #66fcf1;
      text-align: center;
    }

    .step {
      margin: 20px 0;
      font-size: 1.1em;
      line-height: 1.6;
    }

    .buttons {
      display: flex;
      justify-content: space-between;
    }

    button {
      padding: 10px 20px;
      font-size: 1em;
      background-color: #45a29e;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }

    button:disabled {
      background-color: #333;
      cursor: not-allowed;
    }

    .night-tracker {
      background-color: #0b0c10;
      border: 1px solid #45a29e;
      padding: 15px;
      border-radius: 8px;
      margin-bottom: 20px;
      text-align: center;
    }

    .night-tracker h2 {
      color: #66fcf1;
      margin-bottom: 10px;
    }
  </style>
</head>
<body>
  <div class="container">
    <h1>Eidolon Hunt Guide</h1>

    <div id="night-tracker" class="night-tracker">
      <h2>🌗 Plains of Eidolon Time</h2>
      <p id="cycle-status">Loading...</p>
      <p id="next-change"></p>
    </div>

    <div id="step-content" class="step">
      <!-- Tutorial step will go here -->
    </div>

    <div class="buttons">
      <button id="prevBtn" onclick="prevStep()">Previous</button>
      <button id="nextBtn" onclick="nextStep()">Next</button>
    </div>
  </div>

  <script>
    const steps = [
      "🎯 Welcome, Tenno! This tutorial will guide you through hunting Eidolons on the Plains of Eidolon. Click Next to begin.",
      "📌 Step 1: Prerequisites\nYou need to unlock Cetus and have access to the Plains of Eidolon at night. A good amp (like 2-2-3 or 7-7-7) and an Operator-focused build help a lot.",
      "⚔️ Step 2: Gear Up\nWarframe suggestions: Volt (for shields & speed), Trinity (for healing), Chroma (for damage). Bring Operator Arcanes (Virtuous Fury, Magus Elevate).",
      "🔦 Step 3: Eidolon Lures\nFind and charge Eidolon Lures by killing Vomvalysts. Bring 2-3 charged lures to capture Eidolons instead of killing them for more rewards.",
      "🕐 Step 4: The Teralyst\nThis is the first Eidolon. Use your amp to take down its shields, then destroy its limbs using your Warframe weapons. Repeat until it's captured or killed.",
      "🔥 Step 5: Gantulyst & Hydrolyst\nStronger Eidolons spawn after capturing the previous one. These fights require teamwork, coordination, and proper lure/lure positioning.",
      "🎁 Step 6: Rewards\nCapturing Eidolons gives you Eidolon Shards, Arcanes, and Sentient Cores. Trade these in Cetus for standing and Quill upgrades.",
      "✅ You're all done! Ready to face the Eidolons on your own now. Good luck out there, Tenno!"
    ];

    let currentStep = 0;

    function updateStep() {
      document.getElementById("step-content").innerText = steps[currentStep];
      document.getElementById("prevBtn").disabled = currentStep === 0;
      document.getElementById("nextBtn").disabled = currentStep === steps.length - 1;
    }

    function nextStep() {
      if (currentStep < steps.length - 1) {
        currentStep++;
        updateStep();
      }
    }

    function prevStep() {
      if (currentStep > 0) {
        currentStep--;
        updateStep();
      }
    }

    function updateEidolonCycle() {
      const cycleStartUTC = Date.UTC(2024, 0, 1, 0, 0, 0); // Jan 1, 2024 00:00 UTC
      const now = Date.now();
      const cycleLength = 150 * 60 * 1000; // 150 minutes in ms
      const timeSinceStart = (now - cycleStartUTC) % cycleLength;

      const isDay = timeSinceStart < 100 * 60 * 1000;
      const timeLeft = isDay
        ? 100 * 60 * 1000 - timeSinceStart
        : 150 * 60 * 1000 - timeSinceStart;

      const minutes = Math.floor(timeLeft / 60000);
      const seconds = Math.floor((timeLeft % 60000) / 1000);

      const statusText = isDay
        ? "☀️ It is currently DAY on the Plains of Eidolon."
        : "🌙 It is currently NIGHT on the Plains of Eidolon.";

      document.getElementById("cycle-status").innerText = statusText;
      document.getElementById("next-change").innerText =
        `Time until next cycle: ${minutes}m ${seconds}s`;
    }

    // Initialize everything
    window.onload = () => {
      updateStep();
      updateEidolonCycle();
      setInterval(updateEidolonCycle, 1000);
    };
  </script>
</body>
</html>
