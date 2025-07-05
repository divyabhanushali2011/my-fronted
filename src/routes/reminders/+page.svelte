<script>
  import Navbar from '$lib/components/Navbar.svelte';
  // Reactive variables to store reminder data for each category
  let workout = { type: 'hour', time: '', option: '', msg: '' };
  let skincare = { type: 'hour', time: '', option: '', msg: '' };
  let healthcare = { type: 'hour', time: '', option: '', msg: '' };

  // Options for time units and reminder types
  const timeOptions = ['hour', 'minute', 'day'];
  const workoutOptions = ['Cardio', 'Yoga', 'Strength Training', 'Zumba'];
  const skincareOptions = ['Morning Routine', 'Night Routine', 'Hydration', 'Sunscreen'];
  const healthcareOptions = ['Vitamins', 'Doctor Visit', 'Hydrate', 'Meditation'];

  /**
   * Sends a reminder request to the backend API.
   * @param {Object} data - The reminder data (time, type, option).
   * @param {string} category - The category of the reminder (e.g., 'workout').
   * @returns {Promise<string>} - A promise that resolves with a success or error message.
   */
  async function sendReminder(data, category) {
    // Basic validation: check if time and option are filled
    if (!data.time || !data.option) {
      return 'Please fill in all fields.';
    }

    try {
      // Make a POST request to the backend API
      const response = await fetch('http://localhost:5000/api/reminder', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({
          category,
          task: data.option,
          interval: parseInt(data.time), // Ensure interval is an integer
          unit: data.type
        })
      });

      const result = await response.json(); // Parse the JSON response

      // Check if the response was not OK (e.g., 400, 500 status codes)
      if (!response.ok) {
        // Return the error message from the backend or a generic one
        return result.error || 'Something went wrong!';
      }

      // Return the success message from the backend or a generic one
      return result.message || 'Reminder set successfully!';
    } catch (error) {
      // Catch network errors or issues connecting to the server
      console.error('Fetch error:', error); // Log the error for debugging
      return 'Error connecting to the server.';
    }
  }

  /**
   * Sets a reminder for a specific category and updates the UI message.
   * @param {Object} reminderState - The reactive state object for the reminder category.
   * @param {string} categoryName - The name of the category (e.g., 'workout').
   */
  async function setReminder(reminderState, categoryName) {
    // Send the reminder and get the response message
    const msg = await sendReminder(reminderState, categoryName);

    // Update the message property of the reminderState object
    reminderState.msg = msg;

    // Force Svelte to reactively update the component by reassigning the object.
    // This is crucial for Svelte to detect changes within nested object properties.
    if (categoryName === 'workout') workout = { ...reminderState };
    else if (categoryName === 'skincare') skincare = { ...reminderState };
    else if (categoryName === 'healthcare') healthcare = { ...reminderState };

    // Clear the message after 60 seconds (1 minute)
    setTimeout(() => {
      reminderState.msg = ''; // Clear the message
      // Force reactivity again to hide the message
      if (categoryName === 'workout') workout = { ...reminderState };
      else if (categoryName === 'skincare') skincare = { ...reminderState };
      else if (categoryName === 'healthcare') healthcare = { ...reminderState };
    }, 60000); // 60000 milliseconds = 1 minute
  }

  // Helper functions to bind click events to the generic setReminder function
  const setWorkoutReminder = () => setReminder(workout, 'workout');
  const setSkincareReminder = () => setReminder(skincare, 'skincare');
  const setHealthcareReminder = () => setReminder(healthcare, 'healthcare');
</script>

<!-- Tailwind CSS CDN for styling -->

<style>
  /* Base styles for alert messages */
  .alert {
    font-weight: 500;
    border-radius: 0.5rem;
    padding: 1rem;
    margin-top: 1rem;
    background-color: rgba(255, 255, 255, 0.85);
    border: 1px solid transparent;
    /* Added for better visibility */
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }

  /* Success alert specific styles */
  .alert-success {
    background-color: #d4edda;
    border: 1px solid #c3e6cb;
    color: #155724;
  }

  /* Danger/Error alert specific styles */
  .alert-danger {
    background-color: #f8d7da;
    border: 1px solid #f5c6cb;
    color: #721c24;
  }

  /* Body styling */
  body {
    background-color: #f0f4f8;
    font-family: 'Inter', sans-serif; /* Using Inter font as per instructions */
    color: #333;
  }

  /* Card box styling for each reminder section */
  .card-box {
    background: linear-gradient(to right, #f0e5cf, #e8f8f5);
    border-radius: 1.5rem;
    box-shadow: 0 8px 20px rgba(0, 0, 0, 0.2);
    padding: 2.5rem;
    margin-bottom: 2rem;
    transition: transform 0.3s ease-in-out; /* Smooth transition for hover effect */
  }

  /* Hover effect for card boxes */
  .card-box:hover {
    transform: translateY(-5px);
  }

  /* Heading 2 styling */
  h2 {
    font-size: 2.5rem;
    margin-bottom: 1rem;
    text-align: center;
    text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
  }

  /* Heading 4 styling */
  h4 {
    font-weight: 700;
    color: #4a4a4a;
    margin-bottom: 1.5rem;
  }

  /* Label styling */
  label {
    font-weight: 600;
    margin-bottom: 0.75rem;
    display: block;
    color: #555;
  }

  /* Form select and input control styling */
  .form-select,
  .form-control {
    border-radius: 0.5rem;
    padding: 1rem;
    border: 1px solid #ccc;
    transition: border-color 0.3s, box-shadow 0.3s;
    width: 100%; /* Ensure full width within their columns */
  }

  /* Focus styles for form elements */
  .form-select:focus,
  .form-control:focus {
    border-color: #007bff;
    box-shadow: 0 0 5px rgba(0, 123, 255, 0.5);
    outline: none; /* Remove default outline */
  }

  /* Button base styling */
  .btn {
    border-radius: 0.5rem;
    padding: 0.75rem 1.5rem;
    font-weight: 700;
    transition: background-color 0.3s ease-in-out, transform 0.3s ease-in-out;
    border: none; /* Remove default button border */
    cursor: pointer; /* Indicate clickable element */
  }

  /* Button hover effect */
  .btn:hover {
    transform: scale(1.05);
  }

  /* Specific button colors */
  .btn-success { background-color: #28a745; color: white; }
  .btn-warning { background-color: #ffc107; color: white; }
  .btn-primary { background-color: #007bff; color: white; }

  /* Responsive adjustments for smaller screens */
  @media (max-width: 767.98px) {
    .card-box {
      padding: 2rem;
    }

    h2 {
      font-size: 2rem;
    }

    h4 {
      font-size: 1.5rem;
    }

    /* Ensure buttons take full width on small screens */
    .btn {
      width: 100%;
    }
  }
</style>
<Navbar/>
<!-- Main container for the application, centered with max width -->
<div class="container mx-auto py-5 px-4 max-w-4xl">
  <h2 class="text-center mb-5 text-4xl font-bold">🔔 Set Your Personalized Reminders</h2>

  <!-- Workout Reminder Section -->
  <div class="card-box">
    <h4 class="text-2xl">🏋️ Workout Reminder</h4>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
      <div class="col-span-1">
        <label for="workoutType" class="block text-gray-700 text-sm font-bold mb-2">Reminder Type</label>
        <select id="workoutType" class="form-select" bind:value={workout.type}>
          {#each timeOptions as opt}
            <option value={opt}>{opt}</option>
          {/each}
        </select>
      </div>
      <div class="col-span-1">
        <label for="workoutTime" class="block text-gray-700 text-sm font-bold mb-2">Every ({workout.type})</label>
        <input id="workoutTime" class="form-control" type="number" min="1" placeholder="Enter time" bind:value={workout.time} />
      </div>
      <div class="col-span-1">
        <label for="workoutOption" class="block text-gray-700 text-sm font-bold mb-2">Workout Type</label>
        <select id="workoutOption" class="form-select" bind:value={workout.option}>
          <option value="" disabled>Select Workout</option>
          {#each workoutOptions as w}
            <option value={w}>{w}</option>
          {/each}
        </select>
      </div>
    </div>
    <button class="btn btn-success mt-4 w-full md:w-auto" on:click={setWorkoutReminder}>Set Workout Reminder</button>
    {#if workout.msg}
      <!-- Display success or error message based on content -->
      <div class="alert {workout.msg.includes('Error') || workout.msg.includes('Please fill') ? 'alert-danger' : 'alert-success'}">
        {workout.msg}
      </div>
    {/if}
  </div>

  <!-- Skincare Reminder Section -->
  <div class="card-box">
    <h4 class="text-2xl">💆 Skincare Reminder</h4>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
      <div class="col-span-1">
        <label for="skincareType" class="block text-gray-700 text-sm font-bold mb-2">Reminder Type</label>
        <select id="skincareType" class="form-select" bind:value={skincare.type}>
          {#each timeOptions as opt}
            <option value={opt}>{opt}</option>
          {/each}
        </select>
      </div>
      <div class="col-span-1">
        <label for="skincareTime" class="block text-gray-700 text-sm font-bold mb-2">Every ({skincare.type})</label>
        <input id="skincareTime" class="form-control" type="number" min="1" placeholder="Enter time" bind:value={skincare.time} />
      </div>
      <div class="col-span-1">
        <label for="skincareOption" class="block text-gray-700 text-sm font-bold mb-2">Skincare Type</label>
        <select id="skincareOption" class="form-select" bind:value={skincare.option}>
          <option value="" disabled>Select Skincare</option>
          {#each skincareOptions as s}
            <option value={s}>{s}</option>
          {/each}
        </select>
      </div>
    </div>
    <button class="btn btn-warning mt-4 w-full md:w-auto" on:click={setSkincareReminder}>Set Skincare Reminder</button>
    {#if skincare.msg}
      <div class="alert {skincare.msg.includes('Error') || skincare.msg.includes('Please fill') ? 'alert-danger' : 'alert-success'}">
        {skincare.msg}
      </div>
    {/if}
  </div>

  <!-- Healthcare Reminder Section -->
  <div class="card-box">
    <h4 class="text-2xl">🩺 Healthcare Reminder</h4>
    <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
      <div class="col-span-1">
        <label for="healthcareType" class="block text-gray-700 text-sm font-bold mb-2">Reminder Type</label>
        <select id="healthcareType" class="form-select" bind:value={healthcare.type}>
          {#each timeOptions as opt}
            <option value={opt}>{opt}</option>
          {/each}
        </select>
      </div>
      <div class="col-span-1">
        <label for="healthcareTime" class="block text-gray-700 text-sm font-bold mb-2">Every ({healthcare.type})</label>
        <input id="healthcareTime" class="form-control" type="number" min="1" placeholder="Enter time" bind:value={healthcare.time} />
      </div>
      <div class="col-span-1">
        <label for="healthcareOption" class="block text-gray-700 text-sm font-bold mb-2">Healthcare Type</label>
        <select id="healthcareOption" class="form-select" bind:value={healthcare.option}>
          <option value="" disabled>Select Healthcare</option>
          {#each healthcareOptions as h}
            <option value={h}>{h}</option>
          {/each}
        </select>
      </div>
    </div>
    <button class="btn btn-primary mt-4 w-full md:w-auto" on:click={setHealthcareReminder}>Set Healthcare Reminder</button>
    {#if healthcare.msg}
      <div class="alert {healthcare.msg.includes('Error') || healthcare.msg.includes('Please fill') ? 'alert-danger' : 'alert-success'}">
        {healthcare.msg}
      </div>
    {/if}
  </div>
</div>
