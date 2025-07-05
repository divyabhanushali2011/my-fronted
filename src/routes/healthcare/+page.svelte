<script>
  import Navbar from '$lib/components/Navbar.svelte';

  let goal = '';
  let height = '';
  let weight = '';
  let diet = '';
  let tips = [];

  function calculateBMI() {
    const h = parseFloat(height) / 100;
    const w = parseFloat(weight);
    if (!h || !w || !goal || !diet) {
      tips = ["❗ Please fill in all fields properly."];
      return;
    }

    const bmi = (w / (h * h)).toFixed(1);
    generateTips(bmi);
  }

  function generateTips(bmi) {
    tips = [];
    let emoji = '';
    if (bmi < 18.5) emoji = '🤏 (Underweight)';
    else if (bmi < 25) emoji = '🧍‍♂️ (Normal)';
    else if (bmi < 30) emoji = '🙂 (Overweight)';
    else emoji = '🐷 (Obese)';

    tips.push(`Your BMI is ${bmi} ${emoji}`);

    if (goal === 'lose') {
      tips.push("🥗 Eat more vegetables, avoid sugary foods.");
      tips.push("🏃 Exercise daily: walk, run or do yoga for 30 mins.");
      tips.push("💧 Drink at least 3L of water every day.");
      if (diet === 'nonveg') tips.push("🍗 Eat grilled chicken/fish instead of fried items.");
    } else if (goal === 'gain') {
      tips.push("🍚 Eat calorie-dense food: rice, bananas, potatoes.");
      tips.push("💪 Do strength training 3-4 times a week.");
      tips.push("🧀 Add protein: paneer, cheese, eggs or meat.");
      if (diet === 'veg') tips.push("🌰 Include nuts, seeds and soy products in meals.");
    } else if (goal === 'healthy') {
      tips.push("🥦 Maintain a balanced diet with all nutrients.");
      tips.push("🚶‍♂️ Walk at least 5,000 steps a day.");
      tips.push("😴 Sleep for 7–8 hours consistently.");
      tips.push("🧘 Practice meditation or deep breathing.");
    }
  }
</script>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    font-family: 'Segoe UI', sans-serif;
    background: #eaf6ff;
  }

  main {
    display: flex;
    align-items: center;
    justify-content: center;
    min-height: calc(100vh - 60px); /* Adjust based on Navbar height */
    padding: 2rem;
    box-sizing: border-box;
  }

  .container {
    max-width: 600px;
    width: 100%;
    padding: 2rem;
    background: #f0f9ff;
    border-radius: 15px;
    box-shadow: 0 0 10px rgba(0,0,0,0.1);
  }

  h2 {
    text-align: center;
    margin-bottom: 1rem;
  }

  label {
    font-weight: bold;
    margin-top: 1rem;
    display: block;
  }

  select, input {
    margin-bottom: 1rem;
    width: 100%;
    padding: 10px;
    border-radius: 8px;
    border: 1px solid #ccc;
  }

  button {
    background: #00aaff;
    color: white;
    padding: 12px;
    border-radius: 10px;
    border: none;
    cursor: pointer;
    font-weight: bold;
    width: 100%;
    margin-top: 1rem;
  }

  ul {
    margin-top: 1.5rem;
    padding-left: 1.5rem;
  }

  li {
    margin-bottom: 0.6rem;
  }

  h3 {
    margin-top: 2rem;
    color: #0077aa;
  }
</style>

<Navbar />

<main>
  <div class="container">
    <h2>🩺 Personalized Health Tips</h2>

    <label>What do you want to do?</label>
    <select bind:value={goal}>
      <option value="" disabled selected>Choose your goal</option>
      <option value="lose">📉 Lose Weight</option>
      <option value="gain">📈 Gain Weight</option>
      <option value="healthy">🧘 Stay Healthy</option>
    </select>

    <label>Height (cm)</label>
    <input type="number" bind:value={height} min="50" max="250" />

    <label>Weight (kg)</label>
    <input type="number" bind:value={weight} min="10" max="250" />

    <label>Diet Preference</label>
    <select bind:value={diet}>
      <option value="" disabled selected>Choose diet</option>
      <option value="veg">🥦 Vegetarian</option>
      <option value="nonveg">🍗 Non-Vegetarian</option>
    </select>

    <button on:click={calculateBMI}>Get Tips ✅</button>

    {#if tips.length}
      <h3>💡 Tips for You:</h3>
      <ul>
        {#each tips as tip}
          <li>{tip}</li>
        {/each}
      </ul>
    {/if}
  </div>
</main>