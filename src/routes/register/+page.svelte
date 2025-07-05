<script>
  import { goto } from '$app/navigation';
  import Navbar from '$lib/components/Navbar.svelte';

  let firstName = '', lastName = '', email = '', phone = '';
  let address = '', city = '', state = '', zip = '', birthdate = '';
  let gender = '', password = '', confirmPassword = '';
  let plan = '', planType = 'monthly', selectedPaymentMethod = 'qr';
  let agreeTerms = false;

  async function handleSubmit(event) {
  event.preventDefault();

  const res = await fetch('http://localhost:5000/api/register', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json'
    },
    body: JSON.stringify({
      firstName,
      lastName,
      email,
      phone,
      address,
      city,
      state,
      zip,
      birthdate,
      gender,
      password,
      confirmPassword,
      plan,
      planType,
      selectedPaymentMethod
    })
  });

  const result = await res.json();

  if (res.ok) {
    alert(result.message);
    goto('login');  // ✅ redirect
  } else {
    alert(result.error || "Something went wrong.");
  }
}
</script>

<style>
  header {
    background: white;
    padding: 1.2rem 3rem;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    position: sticky;
    top: 0;
    z-index: 10;
  }

  nav {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .logo {
    font-size: 1.8rem;
    font-weight: bold;
    color: #222;
  }

  ul {
    list-style: none;
    display: flex;
    gap: 1.5rem;
  }

  ul li a {
    text-decoration: none;
    color: #444;
    font-weight: 500;
    position: relative;
    transition: color 0.3s;
  }

  ul li a::after {
    content: '';
    position: absolute;
    bottom: -4px;
    left: 0;
    width: 0;
    height: 2px;
    background: #ff6a3d;
    transition: 0.3s ease;
  }

  ul li a:hover::after {
    width: 100%;
  }

  .login-btn {
    background: #ff6a3d;
    color: white;
    padding: 0.5rem 1rem;
    border-radius: 6px;
  }

  h1 {
    font-size: 3rem;
    color: rgb(30, 30, 30);
  }
</style>

<Navbar />

<!-- Form -->
<div class="flex flex-col items-center justify-center px-4 py-12 sm:py-20 bg-gradient-to-b from-white to-gray-100 min-h-screen">
  <div class="w-full max-w-xl mx-auto overflow-hidden rounded-3xl shadow-2xl bg-black">
    <div class="bg-gray-900 bg-opacity-95 p-6 sm:p-8 rounded-3xl">
      <h2 class="text-3xl sm:text-4xl font-bold text-white mb-4 text-center">Join Health & Fitness</h2>

      <form on:submit={handleSubmit} class="space-y-4">
        <!-- Personal Details -->
        <div class="flex flex-col sm:flex-row sm:space-x-4">
          <div class="w-full">
            <label class="block text-white font-bold mb-1">First Name</label>
            <input bind:value={firstName} required pattern="[A-Za-z\s]+" on:input={(e) => firstName = e.target.value.replace(/[^a-zA-Z\s]/g, '')} class="w-full px-4 py-2 rounded-xl bg-gray-800 text-white" />
          </div>
          <div class="w-full mt-4 sm:mt-0">
            <label class="block text-white font-bold mb-1">Last Name</label>
            <input bind:value={lastName} required pattern="[A-Za-z\s]+" on:input={(e) => lastName = e.target.value.replace(/[^a-zA-Z\s]/g, '')} class="w-full px-4 py-2 rounded-xl bg-gray-800 text-white" />
          </div>
        </div>

        <div>
          <label class="block text-white font-bold mb-1">Email</label>
          <input bind:value={email} type="email" required class="w-full px-4 py-2 rounded-xl bg-gray-800 text-white" />
        </div>

        <div>
          <label class="block text-white font-bold mb-1">Phone</label>
          <input bind:value={phone} type="tel" inputmode="numeric" pattern="[0-9]*" maxlength="10" on:input={(e) => phone = e.target.value.replace(/\D/g, '')} required class="w-full px-4 py-2 rounded-xl bg-gray-800 text-white" />
        </div>

        <div>
          <label class="block text-white font-bold mb-1">Address</label>
          <input bind:value={address} type="text" class="w-full px-4 py-2 rounded-xl bg-gray-800 text-white" />
        </div>

        <div class="flex flex-col sm:flex-row sm:space-x-4">
          <div class="w-full">
            <label class="block text-white font-bold mb-1">City</label>
            <input bind:value={city} type="text" class="w-full px-4 py-2 rounded-xl bg-gray-800 text-white" />
          </div>
          <div class="w-full mt-4 sm:mt-0">
            <label class="block text-white font-bold mb-1">State</label>
            <input bind:value={state} type="text" class="w-full px-4 py-2 rounded-xl bg-gray-800 text-white" />
          </div>
          <div class="w-full mt-4 sm:mt-0">
            <label class="block text-white font-bold mb-1">Zip</label>
            <input bind:value={zip} type="text" inputmode="numeric" pattern="[0-9]*" maxlength="6" on:input={(e) => zip = e.target.value.replace(/\D/g, '')} class="w-full px-4 py-2 rounded-xl bg-gray-800 text-white" />
          </div>
        </div>

        <div>
          <label class="block text-white font-bold mb-1">Birthdate</label>
          <input bind:value={birthdate} type="date" required class="w-full px-4 py-2 rounded-xl bg-gray-800 text-white" />
        </div>

        <div>
          <label class="block text-white font-bold mb-1">Gender</label>
          <select bind:value={gender} required class="w-full px-4 py-2 rounded-xl bg-gray-800 text-white">
            <option value="" disabled selected>Select Gender</option>
            <option value="male">Male</option>
            <option value="female">Female</option>
            <option value="other">Other</option>
          </select>
        </div>

        <div>
          <label class="block text-white font-bold mb-1">Password</label>
          <input bind:value={password} type="password" required class="w-full px-4 py-2 rounded-xl bg-gray-800 text-white" />
        </div>

        <div>
          <label class="block text-white font-bold mb-1">Confirm Password</label>
          <input bind:value={confirmPassword} type="password" required class="w-full px-4 py-2 rounded-xl bg-gray-800 text-white" />
        </div>

        <div>
          <label class="block text-white font-bold mb-1">Choose Your Plan</label>
          <div class="flex gap-4 text-white">
            <label><input type="radio" bind:group={plan} value="free" /> Free Plan</label>
            <label><input type="radio" bind:group={plan} value="paid" /> Buy Now Plan</label>
          </div>
        </div>

        {#if plan === 'paid'}
          <div class="bg-gray-800 text-white p-4 rounded-xl mt-4">
            <label class="block mb-1">Select Plan Type:</label>
            <select bind:value={planType} class="w-full px-4 py-2 mb-4 rounded-xl bg-gray-700 text-white">
              <option value="monthly">Monthly</option>
              <option value="quarterly">Quarterly</option>
              <option value="yearly">Yearly</option>
            </select>

            <p class="text-sm mb-2">Choose Payment Method:</p>
            <select bind:value={selectedPaymentMethod} class="w-full px-4 py-2 mb-4 rounded-xl bg-gray-700 text-white">
              <option value="qr">UPI QR Code</option>
              <option value="card">Card Payment</option>
              <option value="bank">Bank Transfer</option>
            </select>

            {#if selectedPaymentMethod === 'qr'}
              <div>
                <p class="mb-2">Scan the QR to pay:</p>
                <img src="/images/paymentqr.jpg" alt="QR Code" class="w-40 mx-auto" />
              </div>
            {/if}

            {#if selectedPaymentMethod === 'card'}
              <div class="space-y-2">
                <label class="block">Cardholder Name</label>
                <input type="text" class="w-full px-4 py-2 rounded-xl bg-gray-700 text-white" placeholder="John Doe" />

                <label class="block">Card Number</label>
                <input type="text" maxlength="16" class="w-full px-4 py-2 rounded-xl bg-gray-700 text-white" placeholder="1234 5678 9012 3456" />

                <div class="flex gap-2">
                  <div class="w-1/2">
                    <label>Expiry</label>
                    <input type="text" maxlength="5" placeholder="MM/YY" class="w-full px-4 py-2 rounded-xl bg-gray-700 text-white" />
                  </div>
                  <div class="w-1/2">
                    <label>CVV</label>
                    <input type="password" maxlength="3" class="w-full px-4 py-2 rounded-xl bg-gray-700 text-white" />
                  </div>
                </div>
              </div>
            {/if}

            {#if selectedPaymentMethod === 'bank'}
              <div>
                <p>Transfer to the following account:</p>
                <ul class="mt-2 space-y-1 text-sm">
                  <li><strong>Bank Name:</strong> HDFC Bank</li>
                  <li><strong>Account No:</strong> 123456789012</li>
                  <li><strong>IFSC Code:</strong> HDFC0001234</li>
                  <li><strong>Account Holder:</strong> GYM FORCE Pvt. Ltd.</li>
                </ul>
              </div>
            {/if}
          </div>
        {/if}

        <div class="flex items-center">
          <input type="checkbox" bind:checked={agreeTerms} class="mr-2" />
          <label class="text-white">I agree to the Terms & Conditions</label>
        </div>

        <button type="submit" class="w-full bg-red-600 hover:bg-red-700 text-white py-3 rounded-xl font-semibold tracking-wide">
          {plan === 'paid' ? 'Submit & Pay' : 'Join Free Plan'}
        </button>
      </form>
    </div>
  </div>
</div>
