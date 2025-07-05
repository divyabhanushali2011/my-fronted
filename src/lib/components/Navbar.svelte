<script>
  import { goto } from '$app/navigation';
  import { onMount } from 'svelte';

  let token = '';
  let showMenu = false;
  let user = null;

  onMount(() => {
    token = localStorage.getItem('token');
    const storedUser = localStorage.getItem('user');
    if (storedUser) {
      user = JSON.parse(storedUser);
    }
  });

  function logout() {
    localStorage.removeItem('token');
    localStorage.removeItem('user');
    token = '';
    user = null;
    goto('/');
  }

  function toggleMenu() {
    showMenu = !showMenu;
  }
</script>

<style>
  nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1.2rem 2rem;
    background-color: hwb(0 68% 18% / 0.614);
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
    font-size: 1rem;
    min-height: 70px;
    position: relative;
    z-index: 10;
    flex-wrap: wrap;
  }

  .nav-left {
    font-weight: 700;
    color: #2c2c2c;
    font-size: 1.4rem;
    text-transform: uppercase;
    letter-spacing: 1px;
    user-select: none;
  }

  .menu-toggle {
    display: none;
    background: none;
    border: none;
    font-size: 1.6rem;
    cursor: pointer;
  }

  .nav-right {
    display: flex;
    gap: 2rem;
    align-items: center;
  }

  .nav-right a {
    text-decoration: none;
    font-weight: 600;
    font-size: 1rem;
    color: #4FAE69;
    transition: color 0.3s ease;
  }

  .nav-right a.login {
    color: #d67854;
  }

  .nav-right a:hover {
    color: #39592d;
  }

  button.logout {
    background: none;
    border: none;
    font-size: 1rem;
    color: #d67854;
    font-weight: 600;
    cursor: pointer;
  }

  button.logout:hover {
    color: #a13e28;
  }

  @media (max-width: 768px) {
    .menu-toggle {
      display: block;
      color: #2c2c2c;
    }

    .nav-right {
      display: none;
      flex-direction: column;
      width: 100%;
      padding: 1rem 0;
    }

    .nav-right.show {
      display: flex;
    }

    .nav-right a,
    button.logout {
      width: 100%;
      text-align: left;
      padding: 0.5rem 0;
    }
  }
</style>

<nav aria-label="Primary navigation">
  <div class="nav-left">GYMNEST</div>

  <!-- Hamburger Menu -->
  <button class="menu-toggle" on:click={toggleMenu} aria-label="Toggle menu">
    &#9776;
  </button>

  <!-- Navigation Links -->
  <div class="nav-right {showMenu ? 'show' : ''}">
    <a href="/">Home</a>
    <a href="/about">About Us</a>
    <a href="contect">Contact Us</a>

    {#if token && user}
      <a href="/dashboard">Dashboard</a>
      <button class="logout" on:click={logout}>Logout</button>
    {:else}
      <a href="/login">Login</a>
      <a href="/register" class="login">Join Now</a>
    {/if}
  </div>
</nav>
