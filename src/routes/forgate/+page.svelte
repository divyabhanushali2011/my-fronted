<script>
  let email = '';
  let new_password = '';
  let error = '';
  let success = '';

  async function resetPassword() {
    error = '';
    success = '';

    if (!email || !new_password) {
      error = 'Please enter email and new password.';
      return;
    }

    try {
      const res = await fetch('http://localhost:5000/api/forgot', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ email, new_password })
      });

      const data = await res.json();

      if (res.ok) {
        success = data.message;
        error = '';
      } else {
        error = data.error || 'Something went wrong.';
      }
    } catch (err) {
      error = 'Failed to connect to server.';
    }
  }
</script>

<style>
  .forgot-container {
    max-width: 400px;
    margin: 60px auto;
    padding: 2rem;
    background: #fff3cd;
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
    background-color: #ffc107;
    color: black;
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

<div class="forgot-container">
  <h2>Reset Password</h2>

  <input type="email" bind:value={email} placeholder="Your registered email" />
  <input type="password" bind:value={new_password} placeholder="New password" />

  <button on:click={resetPassword}>Reset Password</button>

  {#if error}
    <p class="error">{error}</p>
  {/if}

  {#if success}
    <p class="success">{success}</p>
    <p><a href="/login">Go back to login</a></p>
  {/if}
</div>
