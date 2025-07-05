<script>
  import { onMount } from 'svelte';

  onMount(() => {
    document.title = "Thank You";
  });
</script>

<style>
  .thankyou-wrapper {
    min-height: 100vh;
    background: linear-gradient(135deg, #d0f2f0, #fdf3d8);
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 2rem;
  }

  .thankyou-card {
    background: #ffffff;
    padding: 3rem 2rem;
    border-radius: 2rem;
    box-shadow: 0 15px 30px rgba(0, 0, 0, 0.1);
    max-width: 500px;
    width: 100%;
    text-align: center;
    animation: popIn 0.4s ease-in-out;
  }

  @keyframes popIn {
    0% {
      transform: scale(0.9);
      opacity: 0;
    }
    100% {
      transform: scale(1);
      opacity: 1;
    }
  }

  h1 {
    font-size: 2.2rem;
    color: #2e7d32;
    margin-bottom: 1rem;
  }

  p {
    font-size: 1.1rem;
    color: #555;
    margin-bottom: 2rem;
  }

  .btn-home {
    display: inline-block;
    background: #4caf50;
    color: white;
    padding: 0.75rem 2rem;
    border-radius: 50px;
    text-decoration: none;
    font-weight: 600;
    font-size: 1rem;
    transition: background 0.3s ease;
  }

  .btn-home:hover {
    background: #388e3c;
  }

  .emoji {
    font-size: 3.5rem;
    margin-bottom: 1rem;
    animation: bounce 1.5s infinite;
  }

  @keyframes bounce {
    0%, 100% {
      transform: translateY(0);
    }
    50% {
      transform: translateY(-8px);
    }
  }

  @media (max-width: 600px) {
    .thankyou-card {
      padding: 2rem 1.5rem;
    }

    h1 {
      font-size: 1.8rem;
    }

    p {
      font-size: 1rem;
    }

    .emoji {
      font-size: 3rem;
    }
  }
</style>

<div class="thankyou-wrapper">
  <div class="thankyou-card">
    <div class="emoji">🎉</div>
    <h1>Registration Successful!</h1>
    <p>Thank you for joining us! <br>You can now access your account and explore.</p>
    <a href="dashboard" class="btn-home">Get start</a>
  </div>
</div>
