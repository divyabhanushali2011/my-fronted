<script>
  import Navbar from '$lib/components/Navbar.svelte';
  let socialLinks = [
    {
      name: "Instagram",
      icon: "M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zM12 0C8.741 0 8.333.014 7.053.072 2.695.272.273 2.69.073 7.052.014 8.333 0 8.741 0 12c0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98C8.333 23.986 8.741 24 12 24c3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98C15.668.014 15.259 0 12 0zm0 5.838a6.162 6.162 0 100 12.324 6.162 6.162 0 000-12.324zM12 16a4 4 0 110-8 4 4 0 010 8zm6.406-11.845a1.44 1.44 0 100 2.881 1.44 1.44 0 000-2.881z",
      url: "https://instagram.com/yourprofile",
      username: "@fitnesstrainer",
      followers: "12.5K"
    },
    {
      name: "Facebook",
      icon: "M22.675 0H1.325C.593 0 0 .593 0 1.325v21.351C0 23.407.593 24 1.325 24H12.82v-9.294H9.692v-3.622h3.128V8.413c0-3.1 1.893-4.788 4.659-4.788 1.325 0 2.463.099 2.795.143v3.24l-1.918.001c-1.504 0-1.795.715-1.795 1.763v2.313h3.587l-.467 3.622h-3.12V24h6.116c.73 0 1.323-.593 1.323-1.325V1.325C24 .593 23.407 0 22.675 0z",
      url: "https://facebook.com/yourprofile",
      username: "@fitness.coach",
      followers: "8.2K"
    },
    {
      name: "Twitter",
      icon: "M23.953 4.57a10 10 0 01-2.825.775 4.958 4.958 0 002.163-2.723c-.951.555-2.005.959-3.127 1.184a4.92 4.92 0 00-8.384 4.482C7.69 8.095 4.067 6.13 1.64 3.162a4.822 4.822 0 00-.666 2.475c0 1.71.87 3.213 2.188 4.096a4.904 4.904 0 01-2.228-.616v.06a4.923 4.923 0 003.946 4.827 4.996 4.996 0 01-2.212.085 4.936 4.936 0 004.604 3.417 9.867 9.867 0 01-6.102 2.105c-.39 0-.779-.023-1.17-.067a13.995 13.995 0 007.557 2.209c9.053 0 13.998-7.496 13.998-13.985 0-.21 0-.42-.015-.63A9.935 9.935 0 0024 4.59z",
      url: "https://twitter.com/yourprofile",
      username: "@fitcoach",
      followers: "5.7K"
    },
    {
      name: "YouTube",
      icon: "M23.498 6.186a3.016 3.016 0 0 0-2.122-2.136C19.505 3.545 12 3.545 12 3.545s-7.505 0-9.377.505A3.017 3.017 0 0 0 .502 6.186C0 8.07 0 12 0 12s0 3.93.502 5.814a3.016 3.016 0 0 0 2.122 2.136c1.871.505 9.377.505 9.377.505s7.505 0 9.377-.505a3.015 3.015 0 0 0 2.122-2.136C24 15.93 24 12 24 12s0-3.93-.502-5.814zM9.545 15.568V8.432L15.818 12l-6.273 3.568z",
      url: "https://youtube.com/yourchannel",
      username: "@fitnesschannel",
      followers: "24.3K"
    }
  ];

  let gymInfo = {
    name: "GYMNEST & FITNESS",
    address: "123 Health Street, Fitness City, FC 12345",
    phone: "+91 9876543210",
    email: "trainer@fitlifegym.com",
    hours: [
      { day: "Monday-Friday", time: "6:00 AM - 10:00 PM" },
      { day: "Saturday", time: "8:00 AM - 8:00 PM" },
      { day: "Sunday", time: "8:00 AM - 6:00 PM" }
    ],
    facilities: [
      "Cardio Zone",
      "Weight Training",
      "Group Classes",
      "Personal Training",
      "Sauna & Spa"
    ]
  };

  function followSocial(platform) {
    alert(`Following ${platform} profile!`);
    // In a real app, this would redirect to the social media or make an API call
  }
</script>
<Navbar/>
<div class="contact-container">
  <header class="header">
    <h1>Connect With Me</h1>
    <p>Follow my fitness journey and get in touch for training inquiries</p>
  </header>

  <div class="social-section">
    <h2>Social Media Profiles</h2>
    <div class="social-grid">
      {#each socialLinks as link}
        <div class="social-card">
          <div class="social-icon">
            <svg viewBox="0 0 24 24" aria-hidden="true">
              <path fill="currentColor" d={link.icon} />
            </svg>
          </div>
          <div class="social-info">
            <h3>{link.name}</h3>
            <p>{link.username}</p>
            <p>{link.followers} followers</p>
          </div>
          <button on:click={() => followSocial(link.name)}>
            Follow
          </button>
        </div>
      {/each}
    </div>
  </div>

  <div class="contact-section">
    <div class="gym-info">
      <h2>Gym Information</h2>
      <div class="info-card">
        <h3>{gymInfo.name}</h3>
        <p><strong>Address:</strong> {gymInfo.address}</p>
        <p><strong>Phone:</strong> {gymInfo.phone}</p>
        <p><strong>Email:</strong> <a href={`mailto:${gymInfo.email}`}>{gymInfo.email}</a></p>
        
        <div class="working-hours">
          <h4>Working Hours:</h4>
          <ul>
            {#each gymInfo.hours as hour}
              <li>{hour.day}: {hour.time}</li>
            {/each}
          </ul>
        </div>
        
        <div class="facilities">
          <h4>Facilities:</h4>
          <ul>
            {#each gymInfo.facilities as facility}
              <li>{facility}</li>
            {/each}
          </ul>
        </div>
      </div>
    </div>

    <div class="contact-form">
      <h2>Send a Message</h2>
      <form>
        <div class="form-group">
          <label for="name">Name</label>
          <input type="text" id="name" placeholder="Your name" />
        </div>
        <div class="form-group">
          <label for="email">Email</label>
          <input type="email" id="email" placeholder="Your email" />
        </div>
        <div class="form-group">
          <label for="subject">Subject</label>
          <input type="text" id="subject" placeholder="Subject" />
        </div>
        <div class="form-group">
          <label for="message">Message</label>
          <textarea id="message" placeholder="Your message"></textarea>
        </div>
        <button type="submit">Send Message</button>
      </form>
    </div>
  </div>
</div>

<style>
  :global(body) {
    margin: 0;
    padding: 0;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    background-color: #f5f7fa;
    color: #333;
  }

  .contact-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 2rem;
  }

  .header {
    text-align: center;
    margin-bottom: 3rem;
  }

  .header h1 {
    font-size: 2.5rem;
    color: #2c3e50;
    margin-bottom: 0.5rem;
  }

  .header p {
    font-size: 1.1rem;
    color: #7f8c8d;
  }

  .social-section {
    margin-bottom: 3rem;
  }

  .social-section h2 {
    font-size: 1.8rem;
    color: #2c3e50;
    margin-bottom: 1.5rem;
    position: relative;
    display: inline-block;
  }

  .social-section h2::after {
    content: '';
    position: absolute;
    left: 0;
    bottom: -8px;
    width: 60px;
    height: 4px;
    background: #3498db;
    border-radius: 2px;
  }

  .social-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
    gap: 1.5rem;
  }

  .social-card {
    background: white;
    border-radius: 10px;
    padding: 1.5rem;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
    transition: transform 0.3s, box-shadow 0.3s;
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
  }

  .social-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 10px 15px rgba(0, 0, 0, 0.1);
  }

  .social-icon {
    width: 50px;
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    margin-bottom: 1rem;
  }

  .social-icon svg {
    width: 30px;
    height: 30px;
  }

  /* Different colors for each social platform */
  .social-card:nth-child(1) .social-icon {
    background: linear-gradient(45deg, #f09433, #e6683c, #dc2743, #cc2366, #bc1888);
  }
  .social-card:nth-child(2) .social-icon {
    background: #3b5998;
  }
  .social-card:nth-child(3) .social-icon {
    background: #1da1f2;
  }
  .social-card:nth-child(4) .social-icon {
    background: #ff0000;
  }

  .social-info h3 {
    margin: 0;
    font-size: 1.2rem;
    color: #2c3e50;
  }

  .social-info p {
    margin: 0.3rem 0;
    font-size: 0.9rem;
    color: #7f8c8d;
  }

  .social-card button {
    margin-top: 1rem;
    padding: 0.5rem 1.5rem;
    border: none;
    border-radius: 20px;
    background: #3498db;
    color: white;
    font-weight: 600;
    cursor: pointer;
    transition: background 0.3s;
  }

  .social-card button:hover {
    background: #2980b9;
  }

  .contact-section {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2rem;
    margin-top: 2rem;
  }

  @media (max-width: 768px) {
    .contact-section {
      grid-template-columns: 1fr;
    }
  }

  .gym-info h2, .contact-form h2 {
    font-size: 1.8rem;
    color: #2c3e50;
    margin-bottom: 1.5rem;
    position: relative;
    display: inline-block;
  }

  .gym-info h2::after, .contact-form h2::after {
    content: '';
    position: absolute;
    left: 0;
    bottom: -8px;
    width: 60px;
    height: 4px;
    background: #3498db;
    border-radius: 2px;
  }

  .info-card {
    background: white;
    border-radius: 10px;
    padding: 1.5rem;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }

  .info-card h3 {
    margin-top: 0;
    color: #2c3e50;
  }

  .info-card p {
    margin: 0.8rem 0;
  }

  .info-card a {
    color: #3498db;
    text-decoration: none;
  }

  .info-card a:hover {
    text-decoration: underline;
  }

  .working-hours, .facilities {
    margin-top: 1.5rem;
  }

  .working-hours h4, .facilities h4 {
    margin-bottom: 0.5rem;
    color: #2c3e50;
  }

  .working-hours ul, .facilities ul {
    padding-left: 1.2rem;
    margin: 0;
  }

  .working-hours li, .facilities li {
    margin-bottom: 0.3rem;
  }

  .contact-form {
    background: white;
    border-radius: 10px;
    padding: 1.5rem;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }

  .form-group {
    margin-bottom: 1.2rem;
  }

  .form-group label {
    display: block;
    margin-bottom: 0.5rem;
    font-weight: 600;
    color: #2c3e50;
  }

  .form-group input,
  .form-group textarea {
    width: 100%;
    padding: 0.8rem;
    border: 1px solid #ddd;
    border-radius: 5px;
    font-family: inherit;
    font-size: 1rem;
  }

  .form-group textarea {
    height: 120px;
    resize: vertical;
  }

  .contact-form button {
    width: 100%;
    padding: 0.8rem;
    border: none;
    border-radius: 5px;
    background: #3498db;
    color: white;
    font-size: 1rem;
    font-weight: 600;
    cursor: pointer;
    transition: background 0.3s;
  }

  .contact-form button:hover {
    background: #2980b9;
  }
</style>
