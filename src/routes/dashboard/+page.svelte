<script>
  import Navbar from '$lib/components/Navbar.svelte';
  import { onMount } from 'svelte';

  let user = {
    first_name: '',
    email: '',
    
  };

  
  // Load user from localStorage
  onMount(() => {
    try {
      const storedUser = localStorage.getItem('user');
      const apiKey = localStorage.getItem('api_key');

      if (storedUser) {
        const parsedUser = JSON.parse(storedUser);
        user = {
          first_name: parsedUser.first_name || '',
          email: parsedUser.email || '',
          api_key: apiKey || ''
        };
      }
    } catch (err) {
      console.error("Failed to load user from localStorage:", err);
    }
  });

  const cards = [
    {
      emoji: '🕒',
      title: 'Set Your Reminders',
      desc: 'Never miss your medicine or water intake. Set smart health reminders.',
      link: '/reminders',
      button: 'Go to Reminders'
    },
    {
      emoji: '🎥',
      title: 'Workout Video Guide',
      desc: 'Access yoga and gym exercise videos to learn every move with ease.',
      link: '/workoutguide',
      button: 'Explore Videos'
    },
    {
      emoji: '🧴',
      title: 'Skin Care Tips',
      desc: 'Personalized tips for glowing skin based on your skin type.',
      link: '/skincare',
      button: 'Get Skin Tips'
    },
    {
      emoji: '🧘',
      title: 'Health Advice',
      desc: 'Customized health suggestions like weight gain/loss and diet plans.',
      link: '/healthcare',
      button: 'Get Health Tips'
    },
    {
      emoji: '🏋️‍♀️',
      title: 'Track Your Workout',
      desc: 'Add your daily workouts, track progress, and stay fit with your own workout log.',
      link: '/workout-tracker',
      button: 'Add Workout'
    }
  ];
</script>

<style>
  .dashboard-wrapper {
    padding: 2rem;
    background: #f2f9ff;
    min-height: 100vh;
  }

  .welcome-box {
    background: linear-gradient(to right, #c6f0ff, #e0faff);
    border-radius: 1rem;
    padding: 1.5rem 2rem;
    margin-bottom: 2rem;
    box-shadow: 0 4px 12px rgba(0, 170, 255, 0.2);
  }

  .welcome-box h2 {
    margin-bottom: 0.5rem;
    color: #0077aa;
  }

  .welcome-box p {
    font-size: 0.95rem;
    color: #444;
    margin-bottom: 0.5rem;
    word-break: break-word;
  }

  .dashboard {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(270px, 1fr));
    gap: 1.5rem;
  }

  .card {
    background: #ffffff;
    border-radius: 1.5rem;
    padding: 2rem;
    box-shadow: 0 10px 24px rgba(0, 0, 0, 0.08);
    border: 1px solid #e0e0e0;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }

  .card:hover {
    transform: translateY(-8px);
    box-shadow: 0 12px 32px rgba(0, 0, 0, 0.12);
  }

  .emoji {
    font-size: 2.8rem;
    margin-bottom: 1rem;
  }

  h3 {
    font-size: 1.4rem;
    margin-bottom: 0.5rem;
    color: #333;
  }

  a.button {
    display: inline-block;
    text-align: center;
    padding: 0.6rem 1.4rem;
    background-color: #00aaff;
    color: #fff;
    text-decoration: none;
    border-radius: 30px;
    font-weight: 600;
    font-size: 0.95rem;
    transition: background-color 0.3s ease;
  }

  a.button:hover {
    background-color: #0077aa;
  }


  @media (max-width: 600px) {
    .dashboard-wrapper {
      padding: 1rem;
    }

    .card {
      padding: 1.5rem;
    }

    .welcome-box {
      padding: 1rem 1.5rem;
    }
  }
</style>

<Navbar />

<div class="dashboard-wrapper">
  <div class="welcome-box">
    <h2>Welcome, {user.first_name || 'User'} 👋</h2>
    <p><strong>Email:</strong> {user.email || 'Not available'}</p>
    
  </div>

  <div class="dashboard">
    {#each cards as card}
      <div class="card">
        <div class="emoji">{card.emoji}</div>
        <h3>{card.title}</h3>
        <p>{card.desc}</p>
        <a class="button" href={card.link}>{card.button}</a>
      </div>
    {/each}
  </div>
</div>
