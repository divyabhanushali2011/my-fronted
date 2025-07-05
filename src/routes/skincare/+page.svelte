<script>
  import Navbar from '$lib/components/Navbar.svelte';
  let skinType = '';
  let issues = [];
  let tips = [];
  let error = '';

  const issueOptions = ['Dullness', 'Acne', 'Redness', 'Pigmentation', 'Dry Patches'];

  const tipsDatabase = {
    Dry: {
      Dullness: [
        "Use a rich hydrating moisturizer with Vitamin C.",
        "Massage your face with milk cream before bedtime.",
        "Apply a banana and honey face mask weekly."
      ],
      Acne: [
        "Avoid alcohol-based toners. Try aloe vera gel.",
        "Use turmeric and sandalwood paste on acne.",
        "Wash your face with neem water twice daily."
      ],
      Redness: [
        "Use fragrance-free calming creams.",
        "Apply cucumber juice to reduce inflammation.",
        "Use rose water as a gentle toner."
      ],
      Pigmentation: [
        "Apply gentle brightening serum at night.",
        "Use potato juice or tomato pulp on dark spots.",
        "Make a face pack with besan, turmeric, and lemon juice."
      ],
      "Dry Patches": [
        "Use heavy-duty moisturizer twice daily.",
        "Apply ghee or coconut oil before sleeping.",
        "Use curd and honey as a hydrating mask."
      ]
    },
    Oily: {
      Dullness: [
        "Use a gel-based exfoliant twice a week.",
        "Apply papaya pulp mixed with lemon juice.",
        "Use multani mitti face pack to brighten skin."
      ],
      Acne: [
        "Use a salicylic acid cleanser daily.",
        "Dab raw honey on pimples before sleeping.",
        "Apply paste of tulsi leaves and neem."
      ],
      Redness: [
        "Use lightweight calming gel with niacinamide.",
        "Splash face with cold green tea.",
        "Use aloe vera gel stored in the fridge."
      ],
      Pigmentation: [
        "Try a vitamin C serum in the morning.",
        "Use masoor dal (red lentil) face pack.",
        "Apply turmeric with curd on pigmented spots."
      ],
      "Dry Patches": [
        "Avoid harsh scrubs and over-washing.",
        "Apply almond oil at night.",
        "Use mashed avocado as a patch mask."
      ]
    },
    Combination: {
      Dullness: [
        "Use a balancing toner with glycolic acid.",
        "Apply honey with lemon on dull zones.",
        "Use a fruit-based face mask weekly."
      ],
      Acne: [
        "Use spot treatment for oily zones.",
        "Dab tea tree oil on breakouts.",
        "Make a paste of cinnamon and honey."
      ],
      Redness: [
        "Soothe with green tea extract products.",
        "Use chilled chamomile tea bags on face.",
        "Apply sandalwood paste with rosewater."
      ],
      Pigmentation: [
        "Use an even-tone serum at night.",
        "Use rice flour and milk paste weekly.",
        "Apply raw papaya on dark areas."
      ],
      "Dry Patches": [
        "Apply cream only on dry areas.",
        "Use aloe vera with a few drops of olive oil.",
        "Massage with warm coconut oil before bed."
      ]
    },
    Normal: {
      Dullness: [
        "Use mild exfoliator and brightening mask weekly.",
        "Use honey and lemon mask for natural glow.",
        "Apply orange peel powder with curd."
      ],
      Acne: [
        "Keep skin clean and moisturized.",
        "Use neem paste as a weekly mask.",
        "Dab mint juice to prevent breakouts."
      ],
      Redness: [
        "Use gentle skincare products only.",
        "Apply sandalwood paste and rosewater.",
        "Use fresh cucumber slices regularly."
      ],
      Pigmentation: [
        "Try natural brightening face packs.",
        "Apply mashed strawberries on dark spots.",
        "Use turmeric and honey regularly."
      ],
      "Dry Patches": [
        "Use a nourishing moisturizer regularly.",
        "Apply raw milk with cotton pad before sleep.",
        "Make an almond paste mask once a week."
      ]
    }
  };

  function getTips() {
    if (!skinType || issues.length === 0) {
      error = 'Please select your skin type and at least one issue.';
      tips = [];
      return;
    }

    tips = issues.flatMap(issue => {
      return tipsDatabase[skinType][issue] || [`General advice for ${issue}`];
    });
    error = '';
  }
</script>

<style>
  body {
    background-color: #f9f9f9;
    font-family: 'Arial', sans-serif;
    margin: 0;
    padding: 0;
  }

  .header {
    background-color: #007bff59;
    color: white;
    padding: 20px;
    text-align: center;
  }

  .container {
    max-width: 1200px;
    margin: auto;
    padding: 20px;
  }

  h2 {
    margin-bottom: 20px;
  }

  .card {
    border-radius: 10px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
    transition: transform 0.2s ease, box-shadow 0.2s ease;
    background-color: #ffffff;
    margin-bottom: 20px;
    padding: 15px;
  }

  .card:hover {
    transform: scale(1.02);
    box-shadow: 0 6px 30px rgba(0, 0, 0, 0.15);
  }

  .btn {
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 5px;
    padding: 10px 20px;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }

  .btn:hover {
    background-color: #0056b3;
  }

  .alert {
    background-color: #f8d7da;
    color: #721c24;
    border: 1px solid #f5c6cb;
    border-radius: 5px;
    padding: 10px;
    margin-bottom: 20px;
  }

  .form-check {
    margin: 10px 0;
  }

  .skin-type-option {
    display: flex;
    align-items: center;
    margin: 10px 0;
  }

  .skin-type-option input {
    margin-right: 10px;
  }

  .skin-type-option img {
    width: 50px;
    height: 50px;
    margin-right: 10px;
    border-radius: 50%;
    object-fit: cover;
  }

  ul {
    list-style: disc;
    padding-left: 20px;
  }

  @media (max-width: 576px) {
    h5, label, select, .btn, li {
      font-size: 14px;
    }

    .skin-type-option img {
      width: 40px;
      height: 40px;
    }
  }
</style>
<Navbar/>
<div class="header"m-6>
  
  <h1>Skincare Tips</h1>
  <p>Your personalized skincare routine starts here!</p>
</div>

<div class="container">
  <h2>Get Your Personalized Skincare Tips</h2>

  {#if error}
    <div class="alert">{error}</div>
  {/if}

  <!-- Skin Type -->
  <!-- Skin Type with Smile Emojis -->
<div class="card p-3">
  <h5>1. What's your skin type?</h5>
  
  <div class="skin-type-option">
    <input type="radio" name="skinType" value="Dry" id="dry" bind:group={skinType} />
    <label for="dry">
      <span class="emoji">😬</span> Dry
    </label>
  </div>

  <div class="skin-type-option">
    <input type="radio" name="skinType" value="Oily" id="oily" bind:group={skinType} />
    <label for="oily">
      <span class="emoji">😅</span> Oily
    </label>
  </div>

  <div class="skin-type-option">
    <input type="radio" name="skinType" value="Combination" id="combination" bind:group={skinType} />
    <label for="combination">
      <span class="emoji">🤔</span> Combination
    </label>
  </div>

  <div class="skin-type-option">
    <input type="radio" name="skinType" value="Normal" id="normal" bind:group={skinType} />
    <label for="normal">
      <span class="emoji">😊</span> Normal
    </label>
  </div>
</div>

  <!-- Issues -->
  <div class="card p-3">
    <h5>2. Select your skin concerns:</h5>
    {#each issueOptions as issue}
      <div class="form-check">
        <input class="form-check-input" type="checkbox" bind:group={issues} value={issue} id={issue} />
        <label for={issue}>{issue}</label>
      </div>
    {/each}
  </div>

  <!-- Submit Button -->
  <div class="text-center mb-4">
    <button class="btn" on:click={getTips}>Get Tips</button>
  </div>

  <!-- Display Tips -->
  {#if tips.length > 0}
    <div class="card p-3">
      <h5>Your Personalized Tips:</h5>
      <ul>
        {#each tips as tip}
          <li>{tip}</li>
        {/each}
      </ul>
    </div>
  {/if}
</div>
