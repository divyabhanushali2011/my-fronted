<script>
  import { onMount } from 'svelte';
  import { goto } from '$app/navigation';

  let email = '';
  let password = '';
  let error = '';
  let success = '';

  async function handleLogin() {
  error = '';
  success = '';

  if (!email || !password) {
    error = 'Please enter both email and password.';
    return;
  }

  try {
    const res = await fetch('http://localhost:5000/api/login', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json' },
      body: JSON.stringify({ email, password })
    });

    const data = await res.json();
    console.log('Login response:', data); // 🐛 Log backend response

    if (res.ok) {
      localStorage.setItem('token', data.token);
      localStorage.setItem('api_key', data.api_key);
      localStorage.setItem('user', JSON.stringify(data.user));
      success = data.message;
      goto('thankyou');
    } else {
      error = data.error || 'Login failed';
    }
  } catch (err) {
    console.error('Catch block error:', err); // 🐛 See full error
    error = 'Something went wrong. Try again later.';
  }
}

</script>

<style>
  .login-container {
    max-width: 400px;
    margin: 60px auto;
    padding: 2rem;
    background: #f8f9fa;
    border-radius: 12px;
    box-shadow: 0 0 12px rgba(0,0,0,0.1);
  }

  input {
    width: 100%;
    padding: 0.75rem;
    margin-bottom: 1rem;
    border: 1px solid #ccc;
    border-radius: 8px;
  }

  button {
    width: 100%;
    padding: 0.75rem;
    background-color: #007bff;
    color: white;
    font-weight: bold;
    border: none;
    border-radius: 8px;
    cursor: pointer;
  }

  p {
    text-align: center;
    font-size: 0.9rem;
  }

  .error {
    color: red;
  }

  .success {
    color: green;
  }

  a {
    color: #007bff;
    text-decoration: none;
  }
</style>

<div class="login-container">
  <h2>Login</h2>

  <input type="email" bind:value={email} placeholder="Email" required />
  <input type="password" bind:value={password} placeholder="Password" required />

  <button on:click={handleLogin}>Login</button>

  {#if error}
    <p class="error">{error}</p>
  {/if}

  {#if success}
    <p class="success">{success}</p>
  {/if}

  <p><a href="forgate">Forgot Password?</a></p>
</div>
