<script>
  import { onMount } from 'svelte';
  import Navbar from '$lib/components/Navbar.svelte';

  let img1, img2, img3;

  function fallback(img, fallbackUrl) {
    img.onerror = () => {
      img.src = fallbackUrl;
    };
  }

  onMount(() => {
    fallback(img1, 'https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/142fc0c8-0fa6-4a57-b21b-85352ddfe324.png');
    fallback(img2, 'https://placehold.co/220x220?text=Image+not+available');
    fallback(img3, 'https://placehold.co/220x220?text=Image+not+available');
  });
</script>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    font-family: 'Poppins', sans-serif;
    background-color: #5b79d6;
    overflow-x: hidden;
  }

  .container {
    width: 100%;
    max-width: 100%;
    margin: 0;
    padding: 2rem 4rem;
    background-color: #f4e8e1;
    border-radius: 12px;
    box-shadow: 0 8px 25px rgb(0 0 0 / 0.15);
    display: flex;
    flex-direction: column;
  }

  nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 2rem;
    font-size: 0.9rem;
  }

  .nav-left {
    font-weight: 600;
    color: #4a4a4a;
    user-select: none;
  }

  .nav-right {
    display: flex;
    gap: 2.4rem;
  }

  .nav-right a {
    text-decoration: none;
    font-weight: 600;
    color: #4FAE69;
    transition: color 0.3s ease;
  }

  .nav-right a.login {
    color: #d67854;
  }

  .nav-right a:hover {
    color: #39592d;
  }

  main {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 3rem;
    min-height: 100vh;
    padding-top: 2rem;
    padding-bottom: 2rem;
  }

  .content {
    flex: 1;
  }

  h1 {
    font-size: 2.75rem;
    font-weight: 800;
    color: #1e1e1e;
    margin: 0;
    letter-spacing: 2px;
  }

  .highlight {
    color: #d67854;
    font-weight: 700;
    font-size: 1.3rem;
    margin-top: 0.3rem;
    margin-bottom: 1rem;
    font-family: 'Poppins', sans-serif;
  }

  p {
    font-size: 1rem;
    color: #6f6f6f;
    max-width: 330px;
    line-height: 1.5;
    margin-bottom: 2rem;
    font-weight: 500;
  }

  .btn-learn-more {
    background-color: #385fc1;
    color: white;
    border: none;
    padding: 0.7rem 2rem;
    border-radius: 30px;
    font-weight: 600;
    font-size: 1rem;
    cursor: pointer;
    transition: box-shadow 0.3s ease, background-color 0.3s ease;
    user-select: none;
  }

  .btn-learn-more:hover {
    background-color: #2a4a91;
    box-shadow: 0 5px 15px rgb(56 95 193 / 0.7);
  }

  .illustrations {
    flex: 1;
    display: flex;
    justify-content: center;
    align-items: flex-end;
    gap: 1.5rem;
    position: relative;
    flex-wrap: wrap;
  }

  .animate-updown {
    animation: floatupdown 3s ease-in-out infinite;
  }

  .animate-updown-delay {
    animation-delay: 1.5s;
  }

  @keyframes floatupdown {
    0%, 100% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(-10px);
    }
  }

  .illustrations img {
    width: 220px;
    height: auto;
    border-radius: 10px;
    box-shadow: 0 8px 20px rgb(0 0 0 / 0.12);
    background-color: #fff;
  }

  .small-shape {
    position: absolute;
    width: 50px;
    height: 50px;
    background-color: #4fae69;
    border-radius: 50%;
    opacity: 0.85;
    filter: drop-shadow(1px 2px 1px rgb(0 0 0 / 0.1));
  }

  .kettlebell1 {
    bottom: 40px;
    left: 145px;
  }

  .kettlebell2 {
    bottom: 40px;
    left: 200px;
  }

  .pot {
    bottom: 18px;
    left: 265px;
    border-radius: 14px 14px 34px 14px;
    background-color: #e7c766;
    filter: drop-shadow(1px 2px 1px rgb(0 0 0 / 0.15));
  }

  @media (max-width: 768px) {
    main {
      flex-direction: column;
      align-items: center;
    }

    .illustrations {
      justify-content: center;
    }
  }
</style>

<div class="container" role="main" aria-label="Gym Fitness Homepage">
  <!-- ✅ Navbar placed here -->
  <Navbar />

  <main>
    <section class="content">
      <h1>GYM FITNESS</h1>
      <div class="highlight">Transform Your Body & Mind</div>
      <p>
        Welcome to GYM FITNESS — your destination for strength, stamina, and self-care.  
        We offer expert-designed workout routines, personalized fitness plans, and holistic wellness support.
      </p>
      <a href="/about" class="button">
        <button class="btn-learn-more">Learn More</button>
      </a>
    </section>

    <section class="illustrations">
      <img
        bind:this={img1}
        src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/06d4fd46-3e5d-4b45-9d51-d326ea7e07b6.png"
        alt="Woman lifting dumbbell"
        class="animate-updown"
      />
      <img
        bind:this={img2}
        src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/b01e5e51-20f5-4c96-8e60-54b093f71274.png"
        alt="Woman sitting and lifting weights"
        class="animate-updown animate-updown-delay"
      />
      <img
        bind:this={img3}
        src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/364af2fd-4416-467a-adbc-bf68f0938c3e.png"
        alt="Man jumping rope"
        class="animate-updown"
      />

      <div class="small-shape kettlebell1"></div>
      <div class="small-shape kettlebell2"></div>
      <div class="small-shape pot"></div>
    </section>
  </main>
</div>
