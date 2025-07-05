<script>
  import { fade, slide } from 'svelte/transition';
  import Navbar from '$lib/components/Navbar.svelte';
</script>

<section class="min-h-screen bg-[#fdfcfa] text-[#1e1e1e] p-6">
  <Navbar />
  <h1 class="text-4xl font-bold text-center mb-10" in:fade>About Our Gym</h1>

  <div class="max-w-3xl mx-auto text-lg space-y-6 mb-12">
    <p in:fade={{ delay: 100 }}>
      Welcome to <strong>GYM FORCE</strong> — more than a gym, it's a lifestyle. We focus on physical training, health care, and skin care tips so you glow inside and out.
    </p>
    <p in:fade={{ delay: 200 }}>
      We offer personalized plans, modern equipment, and a friendly environment for all fitness levels. Our experts guide you in workout routines, nutrition, and skin health to ensure holistic well-being.
    </p>
  </div>

  <div class="grid gap-8 md:grid-cols-3 max-w-6xl mx-auto">
    <div class="card" in:slide={{ delay: 100 }}>
      <h2 class="text-xl font-bold mb-2">🎉 2-Day Free Workout</h2>
      <p class="mb-2">Experience our gym absolutely free for 2 days. Try group classes, equipment, and get health + skin care tips from our trainers.</p>
      <p class="mb-4 text-sm italic">Leave a review after your trial. If you love it — join us!</p>
      <a href="/register" class="btn">Join Now</a>
    </div>

    <div class="card" in:slide={{ delay: 200 }}>
      <h2 class="text-xl font-bold mb-2">💪 6-Month Training Plan</h2>
      <p class="mb-2">Get a structured 6-month workout plan with weekly progress tracking, dietary plans, and daily fitness tasks.</p>
      <p class="mb-2 text-sm italic">Includes health & skin care consultations.</p>
      <p class="font-bold text-lg mb-4">₹4,999 Only</p>
      <a href="/register" class="btn">Buy Now</a>
    </div>

    <div class="card" in:slide={{ delay: 300 }}>
      <h2 class="text-xl font-bold mb-2">🏆 1-Year Pro Plan</h2>
      <p class="mb-2">Transform your body with our 12-month elite plan. Full-body transformation coaching + health & skin care guides.</p>
      <p class="mb-2 text-sm italic">Daily motivation, trainer access, and exclusive wellness workshops.</p>
      <p class="font-bold text-lg mb-4">₹9,499 Only</p>
      <a href="/register" class="btn">Buy Now</a>
    </div>
  </div>
</section>

<style>
  header {
    background: #f8f9fa;
    padding: 1.2rem 3rem;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    position: sticky;
    top: 0;
    z-index: 10;
  }

    .login-btn {
    background: #ff6a3d;
    color: white;
    padding: 0.5rem 1rem;
    border-radius: 6px;
    transition: background 0.3s, transform 0.3s;
  }

  .login-btn:hover {
    background: #e55a2b;
    transform: scale(1.05);
  }

  .hero {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
    padding: 3rem;
    min-height: 80vh;
    background-color: #fefaf6;
  }

  .text {
    flex: 1;
    max-width: 500px;
  }

  h1 {
    font-size: 3rem;
    color: #1a1a1a;
  }

  p {
    margin-top: 1rem;
    color: #555;
    line-height: 1.6;
  }

  .btn {
    display: inline-block;
    margin-top: 1.5rem;
    padding: 0.75rem 1.5rem;
    background: #1d3557;
    color: white;
    border-radius: 8px;
    text-decoration: none;
    transition: background 0.3s, transform 0.3s;
  }

  .btn:hover {
    background: #163b4d;
    transform: scale(1.05);
  }

  .illustration img {
    max-width: 100%;
    width: 500px;
    height: auto;
    animation: slide-in 1s ease forwards;
  }

  .fade-in {
    opacity: 0;
    animation: fade-in 1s forwards;
  }

  .delay-1 { animation-delay: 0.3s; }
  .delay-2 { animation-delay: 0.6s; }
  .delay-3 { animation-delay: 0.9s; }

  @keyframes fade-in {
    to { opacity: 1; }
  }

  @keyframes slide-in {
    from {
      opacity: 0;
      transform: translateX(80px);
    }
    to {
      opacity: 1;
      transform: translateX(0);
    }
  }

  .card {
    background: #f7f5f2;
    color: #333;
    border-radius: 12px;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.1);
    padding: 1.5rem;
    transition: transform 0.3s, box-shadow 0.3s;
  }

  .card:hover {
    transform: translateY(-5px);
    box-shadow: 0 8px 30px rgba(0, 0, 0, 0.15);
  }

  @media (max-width: 768px) {
    .hero {
      padding: 2rem;
    }

    h1 {
      font-size: 2.5rem;
    }

    .text {
      max-width: 100%;
    }
  }
</style>
