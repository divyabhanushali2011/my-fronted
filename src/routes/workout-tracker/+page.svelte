<script>
  import { onMount } from 'svelte';

  let workout = {
    type: '',
    name: '',
    sets: '',
    reps: '',
    duration: '',
    calories: ''
  };

  let history = [];
  let chart = null;

  // Fetch workouts
  async function loadWorkouts() {
    const res = await fetch('http://localhost:5000/api/workouts');
    history = await res.json();
    updateChart();
  }

  // Submit new workout
  async function handleSubmit() {
    const formattedWorkout = {
      type: workout.type,
      name: workout.name,
      sets: parseInt(workout.sets),
      reps: parseInt(workout.reps),
      duration: parseInt(workout.duration),
      calories: parseInt(workout.calories)
    };

    try {
      const res = await fetch('http://localhost:5000/api/workout', {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(formattedWorkout)
      });

      const result = await res.json();
      if (!res.ok) {
        alert("Error: " + result.error);
        console.error(result.error);
      }

      workout = { type: '', name: '', sets: '', reps: '', duration: '', calories: '' };
      loadWorkouts();
    } catch (err) {
      alert("Network error");
      console.error(err);
    }
  }

  // Delete workout
  async function deleteWorkout(id) {
    await fetch(`http://localhost:5000/api/workout/${id}`, {
      method: 'DELETE'
    });
    loadWorkouts();
  }

  // Update chart
  function updateChart() {
    if (!window.ApexCharts) return;
    const options = {
      chart: { type: 'line' },
      series: [
        {
          name: 'Calories',
          data: history.map(h => h.calories)
        }
      ],
      xaxis: {
        categories: history.map(h => h.name)
      }
    };

    if (chart) {
      chart.updateSeries(options.series);
      chart.updateOptions({ xaxis: options.xaxis });
    } else {
      chart = new ApexCharts(document.querySelector("#chart"), options);
      chart.render();
    }
  }

  onMount(loadWorkouts);
</script>

<!-- UI -->
<div class="max-w-4xl mx-auto p-6">
  <h1 class="text-3xl font-bold mb-4 text-center">🏋️ Gym Workout Tracker</h1>

  <div class="bg-white rounded p-4 shadow mb-6 grid grid-cols-2 gap-4">
    <input bind:value={workout.name} placeholder="Workout Name" class="input" />
    <input bind:value={workout.type} placeholder="Type (Cardio/Strength)" class="input" />
    <input bind:value={workout.sets} type="number" placeholder="Sets" class="input" />
    <input bind:value={workout.reps} type="number" placeholder="Reps" class="input" />
    <input bind:value={workout.duration} type="number" placeholder="Duration (min)" class="input" />
    <input bind:value={workout.calories} type="number" placeholder="Calories Burned" class="input" />
    <button on:click={handleSubmit} class="col-span-2 bg-blue-600 text-white px-4 py-2 rounded hover:bg-blue-700">Add Workout</button>
  </div>

  <!-- Table -->
  <div class="overflow-x-auto bg-white shadow rounded mb-6">
    <table class="w-full table-auto text-left border">
      <thead class="bg-gray-100">
        <tr>
          <th>Name</th><th>Type</th><th>Sets</th><th>Reps</th><th>Duration</th><th>Calories</th><th>Action</th>
        </tr>
      </thead>
      <tbody>
        {#each history as h}
          <tr>
            <td>{h.name}</td>
            <td>{h.type}</td>
            <td>{h.sets}</td>
            <td>{h.reps}</td>
            <td>{h.duration} min</td>
            <td>{h.calories}</td>
            <td><button on:click={() => deleteWorkout(h.id)} class="text-red-500">🗑️</button></td>
          </tr>
        {/each}
      </tbody>
    </table>
  </div>

  <!-- Chart -->
  <div class="bg-white p-4 rounded shadow">
    <h2 class="text-xl font-semibold mb-2">📈 Progress Chart</h2>
    <div id="chart" class="w-full"></div>
  </div>
</div>

<style>
  .input {
    padding: 0.5rem;
    border: 1px solid #ccc;
    border-radius: 6px;
    width: 100%;
  }
</style>

<!-- Include ApexCharts CDN -->
<svelte:head>
  <script src="https://cdn.jsdelivr.net/npm/apexcharts"></script>
</svelte:head>
