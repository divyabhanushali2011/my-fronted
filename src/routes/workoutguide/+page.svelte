<script>
  let searchQuery = '';
  let selectedCategory = 'All';

  let videos = [
    {
      id: 'UBMk30rjy0o',
      title: '15 Minute Full Body Workout (No Equipment)',
      channel: 'Chloe Ting',
      views: '15M views',
      duration: '15:05',
      uploaded: '6 months ago',
      category: 'Strength'
    },
    {
      id: 'ml6cT4AZdqI',
      title: '30 Min HIIT Cardio Workout',
      channel: 'SELF',
      views: '8.2M views',
      duration: '30:00',
      uploaded: '1 year ago',
      category: 'Cardio'
    },
    {
      id: 'v7AYKMP6rOE',
      title: '10 Minute Morning Yoga for Beginners',
      channel: 'Yoga With Adriene',
      views: '12M views',
      duration: '10:00',
      uploaded: '2 years ago',
      category: 'Yoga'
    },
    {
      id: '4pKly2JojMw',
      title: 'Stretching & Flexibility Routine',
      channel: 'MadFit',
      views: '6.7M views',
      duration: '20:10',
      uploaded: '11 months ago',
      category: 'Flexibility'
    },
    {
      id: 'qWy_aOlB45Y',
      title: '20 Minute Full Body Strength Workout',
      channel: 'Caroline Girvan',
      views: '4.3M views',
      duration: '20:00',
      uploaded: '3 months ago',
      category: 'Strength'
    },
    {
      id: '50kH47ZztHs',
      title: '30 Minute Cardio Workout at Home',
      channel: 'POPSUGAR Fitness',
      views: '9.5M views',
      duration: '30:00',
      uploaded: '9 months ago',
      category: 'Cardio'
    },
    {
      id: 'sTANio_2E0Q',
      title: 'Yoga for Complete Beginners',
      channel: 'Yoga With Adriene',
      views: '30M views',
      duration: '20:30',
      uploaded: '4 years ago',
      category: 'Yoga'
    },
    {
      id: 'ef4QHUS5760',
      title: 'Stretch & Cool Down Routine',
      channel: 'MadFit',
      views: '2.2M views',
      duration: '15:00',
      uploaded: '5 months ago',
      category: 'Flexibility'
    },
    {
      id: 'UItWltVZZmE',
      title: '25 Min Strength & Toning Workout',
      channel: 'Heather Robertson',
      views: '3.1M views',
      duration: '25:00',
      uploaded: '7 months ago',
      category: 'Strength'
    },
    {
      id: '1919eTCoESo',
      title: '30-Minute Cardio Dance Workout',
      channel: 'POPSUGAR Fitness',
      views: '13M views',
      duration: '30:00',
      uploaded: '2 years ago',
      category: 'Cardio'
    }
  ];

  $: filteredVideos = videos.filter(video => {
    const query = searchQuery.toLowerCase();
    const matchesSearch =
      video.title.toLowerCase().includes(query) || video.channel.toLowerCase().includes(query);
    const matchesCategory = selectedCategory === 'All' || video.category === selectedCategory;
    return matchesSearch && matchesCategory;
  });

  function playVideo(id) {
    window.open(`https://www.youtube.com/watch?v=${id}`, '_blank');
  }
</script>

<style>
  .video-card:hover {
    transform: scale(1.03);
    box-shadow: 0 10px 25px -5px rgba(0, 0, 0, 0.1);
  }

  .duration-badge {
    background: rgba(0, 0, 0, 0.7);
    color: white;
    bottom: 8px;
    right: 8px;
  }

  .play-button {
    background-color: #1d72b8;
    color: white;
    padding: 10px 15px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    margin-top: 10px;
  }

  .play-button:hover {
    background-color: #155a8a;
  }
</style>

<div class="container mx-auto px-4 py-8">
  <h1 class="text-4xl font-bold text-center mb-8 text-gray-900">
    👟 10 Workout Videos to Transform Your Fitness Journey
  </h1>

  <div class="flex flex-col md:flex-row justify-between items-center mb-8 gap-4">
    <div class="relative w-full md:w-1/2">
      <input
        type="text"
        placeholder="Search workout videos..."
        class="w-full px-4 py-3 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-500"
        bind:value={searchQuery}
      />
      <svg
        class="absolute right-3 top-3 h-6 w-6 text-gray-400"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
        />
      </svg>
    </div>

    <div class="w-full md:w-auto">
      <select
        class="px-4 py-3 rounded-lg border border-gray-300 focus:outline-none focus:ring-2 focus:ring-blue-500 w-full"
        bind:value={selectedCategory}
      >
        <option value="All">All Categories</option>
        <option value="Cardio">Cardio</option>
        <option value="Strength">Strength</option>
        <option value="Flexibility">Flexibility</option>
        <option value="Yoga">Yoga</option>
      </select>
    </div>
  </div>

  {#if filteredVideos.length > 0}
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
      {#each filteredVideos as video}
        <div
          class="video-card bg-white rounded-lg overflow-hidden shadow-md hover:shadow-lg transition-all duration-300 cursor-pointer"
        >
          <div class="relative">
            <img
              src={`https://img.youtube.com/vi/${video.id}/0.jpg`}
              alt={`Thumbnail for ${video.title}`}
              class="w-full h-48 object-cover"
              on:error={(e) =>
                (e.target.src = 'https://via.placeholder.com/400x200?text=No+Preview')
              }
            />
            <span class="duration-badge absolute px-2 py-1 rounded text-xs font-medium">
              {video.duration}
            </span>
          </div>
          <div class="p-4">
            <h3 class="font-semibold text-lg mb-1">{video.title}</h3>
            <p class="text-gray-600 text-sm mb-1">{video.channel}</p>
            <div class="flex text-xs text-gray-500">
              <span>{video.views}</span>
              <span class="mx-2">•</span>
              <span>{video.uploaded}</span>
            </div>
            <button class="play-button" on:click={() => playVideo(video.id)}>
              Play Video
            </button>
          </div>
        </div>
      {/each}
    </div>
  {:else}
    <div class="text-center py-12">
      <svg
        class="mx-auto h-12 w-12 text-gray-400"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M9.172 9.172a4 4 0 015.656 0m0 0a4 4 0 015.656 5.656M12 21a9 9 0 11-18 0 9 9 0 0118 0z"
        />
      </svg>
      <h3 class="mt-2 text-lg font-medium text-gray-900">No videos found</h3>
      <p class="mt-1 text-gray-500">Try adjusting your search or filter to find what you're looking for.</p>
    </div>
  {/if}
</div>
