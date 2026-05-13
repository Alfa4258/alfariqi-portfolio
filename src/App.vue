<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue'

const profileImage = ref('/profil.jpg')

const projectWrapper = ref(null)
const projectRow = ref(null)

let dragStartX = 0
let dragStartScroll = 0
let isDragging = false
let moveHandler = null
let upHandler = null
let timelineObserver = null

const experiences = ref([
  {
    title: 'Software Developer (Internship)',
    role: 'PT Labsco Arena Technology',
    meta: 'Aug 2024 - Dec 2024 | South Jakarta',
    tasks: [
      'Developed a desktop application using Flutter and the Dart language to display and manage data from an RFID reader.',
      'Integrated Excel-based data import/export and SQLite local storage, enabling seamless offline data handling and synchronization.',
    ],
  },
  {
    title: 'IT Operational Service (Internship)',
    role: 'PT Sinergi Informatika Semen Indonesia',
    meta: 'Jan 2024 - Jun 2024 | South Jakarta',
    tasks: [
      'Designed and developed the backend system and REST APIs for an internal monitoring dashboard using PHP and the Laravel framework.',
      'Managed and structured the application database using MySQL, creating schemas and queries to ensure efficient data storage and retrieval for monitoring logs.',
      'Collaborated with frontend developers using GitHub for version control and integration testing, maintaining consistent communication to ensure seamless connection between REST APIs and user interface components.',
    ],
  },
])

const projects = ref([
  {
    title: 'RFID Desktop App',
    description:
      'A robust desktop application tailored for offline environments, handling real-time RFID data capture with local SQLite caching.',
    tags: ['Flutter', 'Dart', 'SQLite'],
    link: 'https://github.com/Alfa4258/project-rfid',
  },
  {
    title: 'Internal Monitoring Dashboard',
    description:
      'Backend infrastructure powering an internal company dashboard. Engineered optimized REST APIs to serve extensive monitoring logs seamlessly.',
    tags: ['PHP', 'Laravel', 'MySQL', 'REST API'],
    link: 'https://github.com/Alfa4258/motoo-backend',
  },
  {
    title: 'MyTask',
    description:
      'This website showcases my transition into front-end styling alongside my backend expertise.',
    tags: ['Vue.js', 'TypeScript', 'UI/UX'],
    link: 'https://github.com/Alfa4258/my-task',
  },
  {
    title: 'Inventory API',
    description:
      'A scalable RESTful API built to handle thousands of inventory requests per minute with built-in JWT authentication.',
    tags: ['Node.js', 'Express', 'PostgreSQL'],
    link: 'https://github.com/yourusername/inventory-api',
  },
])

onMounted(() => {
  if (projectRow.value) {
    moveHandler = (event) => {
      if (!isDragging || !projectRow.value) return
      const delta = event.clientX - dragStartX
      projectRow.value.scrollLeft = dragStartScroll - delta
    }

    upHandler = () => {
      isDragging = false
      if (projectRow.value) {
        projectRow.value.classList.remove('dragging')
      }
      window.removeEventListener('mousemove', moveHandler)
      window.removeEventListener('mouseup', upHandler)
    }

    projectRow.value.addEventListener('mousedown', (event) => {
      if (!projectRow.value) return
      isDragging = true
      dragStartX = event.clientX
      dragStartScroll = projectRow.value.scrollLeft
      projectRow.value.classList.add('dragging')
      window.addEventListener('mousemove', moveHandler)
      window.addEventListener('mouseup', upHandler)
    })
  }

  const timelineItems = document.querySelectorAll('.timeline-item')
  if (timelineItems.length > 0) {
    timelineObserver = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            entry.target.classList.add('active')
          } else {
            entry.target.classList.remove('active')
          }
        })
      },
      { rootMargin: '-20% 0px -40% 0px' },
    )
    timelineItems.forEach((item) => timelineObserver?.observe(item))
  }
})

onBeforeUnmount(() => {
  if (moveHandler) window.removeEventListener('mousemove', moveHandler)
  if (upHandler) window.removeEventListener('mouseup', upHandler)
  if (timelineObserver) timelineObserver.disconnect()
})
</script>

<template>
  <div class="page">
    <div class="site-header-wrapper">
      <header class="site-header">
        <div class="header-left">
          <div class="header-logo">
            <span>A</span>
          </div>
          <nav class="site-nav">
            <a href="#profile">ABOUT ME</a>
            <a href="#projects">PROJECTS</a>
            <a href="#experience">EXPERIENCE</a>
          </nav>
        </div>

        <div class="header-right">
          <div class="header-socials">
            <a href="mailto:alfariqi395@gmail.com" aria-label="Email">
              <svg
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <path
                  d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"
                ></path>
                <polyline points="22,6 12,13 2,6"></polyline>
              </svg>
            </a>
            <a href="https://github.com" target="_blank" aria-label="GitHub">
              <svg
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <path
                  d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"
                ></path>
              </svg>
            </a>
            <a href="https://linkedin.com/in/ahmad-alfariqi" target="_blank" aria-label="LinkedIn">
              <svg
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <path
                  d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"
                ></path>
                <rect x="2" y="9" width="4" height="12"></rect>
                <circle cx="4" cy="4" r="2"></circle>
              </svg>
            </a>
            <a href="#" aria-label="Instagram">
              <svg
                viewBox="0 0 24 24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect>
                <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path>
                <line x1="17.5" y1="6.5" x2="17.51" y2="6.5"></line>
              </svg>
            </a>
          </div>
        </div>
      </header>
    </div>

    <main>
      <section id="profile" class="hero">
        <div class="hero-avatar">
          <div class="avatar">
            <img v-if="profileImage" :src="profileImage" alt="Ahmad Alfariqi" class="profile-img" />
            <span v-else>A</span>
          </div>
        </div>
        <div class="hero-content">
          <p class="hero-kicker">Hi, I'm Ahmad Alfariqi</p>
          <h1>Entry-Level Web & Software Developer</h1>
          <p class="hero-body">
            Computer Engineering graduate with a strong foundation in Web Development. Experienced
            in Laravel, Node.js, and Flutter through involvement in both corporate and independent
            projects. Seeking an Entry-Level Web Developer position to apply skills in designing
            REST APIs, database management (SQL/NoSQL), and using Git. Committed to efficient
            development systems, rapid adaptation to new technologies, and effective team
            collaboration.
          </p>
        </div>
      </section>

      <section id="skills" class="section">
        <div class="section-title">
          <h2><span class="icon">&lt;/&gt;</span>Technical Stack</h2>
        </div>
        <div class="pill-grid">
          <span>PHP</span>
          <span>Dart</span>
          <span>JavaScript</span>
          <span>Python</span>
          <span>C++</span>
          <span>Laravel</span>
          <span>Flutter</span>
          <span>Node.js</span>
          <span>Vue.js</span>
          <span>MySQL</span>
          <span>SQLite</span>
          <span>Git & GitHub</span>
          <span>Postman</span>
        </div>
      </section>

      <section id="experience" class="section">
        <div class="section-title">
          <h2>
            <span class="icon">
              <svg
                viewBox="0 0 24 24"
                width="24"
                height="24"
                fill="none"
                stroke="currentColor"
                stroke-width="2"
                stroke-linecap="round"
                stroke-linejoin="round"
              >
                <rect x="2" y="7" width="20" height="14" rx="2" ry="2"></rect>
                <path d="M16 21V5a2 2 0 0 0-2-2h-4a2 2 0 0 0-2 2v16"></path>
              </svg>
            </span>
            Work Experience
          </h2>
        </div>
        <div class="timeline">
          <div v-for="(exp, index) in experiences" :key="index" class="timeline-item">
            <div class="dot"></div>
            <div class="timeline-content-wrapper">
              <div class="timeline-header">
                <div class="timeline-info">
                  <h3>{{ exp.title }}</h3>
                  <p class="role">{{ exp.role }}</p>
                  <p class="meta">{{ exp.meta }}</p>
                </div>
              </div>
              <div class="desc-wrapper">
                <div class="desc-inner">
                  <ul class="desc-list">
                    <li v-for="(task, i) in exp.tasks" :key="i">{{ task }}</li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        </div>
      </section>

      <section id="projects" ref="projectWrapper" class="section">
        <div class="section-title">
          <h2>Featured Projects</h2>
        </div>
        <div ref="projectRow" class="project-row full-bleed-row">
          <article v-for="(project, index) in projects" :key="index" class="project-card">
            <h3>{{ project.title }}</h3>
            <p>{{ project.description }}</p>
            <div class="tags">
              <span v-for="(tag, i) in project.tags" :key="i">{{ tag }}</span>
            </div>
            <div class="card-footer">
              <a
                :href="project.link"
                target="_blank"
                rel="noopener noreferrer"
                class="project-type"
              >
                GitHub Repo ↗
              </a>
            </div>
          </article>
        </div>
      </section>
    </main>

    <footer class="site-footer">
      <div class="footer-socials">
        <a href="mailto:alfariqi395@gmail.com" aria-label="Email">
          <svg
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
            <path
              d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"
            ></path>
            <polyline points="22,6 12,13 2,6"></polyline>
          </svg>
        </a>
        <a href="https://github.com" target="_blank" aria-label="GitHub">
          <svg
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
            <path
              d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"
            ></path>
          </svg>
        </a>
        <a href="https://linkedin.com/in/ahmad-alfariqi" target="_blank" aria-label="LinkedIn">
          <svg
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
            <path
              d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"
            ></path>
            <rect x="2" y="9" width="4" height="12"></rect>
            <circle cx="4" cy="4" r="2"></circle>
          </svg>
        </a>
        <a href="#" aria-label="Instagram">
          <svg
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
            <rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect>
            <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path>
            <line x1="17.5" y1="6.5" x2="17.51" y2="6.5"></line>
          </svg>
        </a>
      </div>
      <p>© 2026 Ahmad Alfariqi. All rights reserved.</p>
    </footer>
  </div>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Manrope:wght@400;600;700;800&family=Space+Grotesk:wght@300;500;700&display=swap');

:root {
  color-scheme: dark;
  font-family: 'Manrope', sans-serif;
  --bg-color: #1a1a1a;
  --text-main: #ffffff;
  --text-muted: #a1a1a1;
  --border: rgba(255, 255, 255, 0.1);
  --card-bg: #222222;
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  background-color: var(--bg-color);
  color: var(--text-main);
  min-height: 100vh;
}

.page {
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 24px;
}

/* --- HEADER STYLES --- */
.site-header-wrapper {
  position: sticky;
  top: 24px;
  z-index: 100;
  display: flex;
  justify-content: center;
  width: 100%;
  margin-bottom: 24px;
}

.site-header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: #1f1f1f;
  border: 1px solid var(--border);
  border-radius: 50px;
  padding: 12px 24px;
  width: 100%;
  box-shadow: 0 4px 20px rgba(0, 0, 0, 0.3);
  backdrop-filter: blur(10px);
}

.header-left {
  display: flex;
  align-items: center;
  gap: 32px;
}

.header-logo {
  width: 34px;
  height: 34px;
  border: 1px solid var(--text-muted);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: 'Space Grotesk', sans-serif;
  font-weight: 300;
  font-size: 16px;
  color: var(--text-main);
  opacity: 0.8;
}

.site-nav {
  display: flex;
  gap: 28px;
}

.site-nav a {
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 1.5px;
  color: var(--text-muted);
  text-transform: uppercase;
  transition: color 0.2s ease;
  text-decoration: none;
}

.site-nav a:hover {
  color: var(--text-main);
}

.header-right {
  display: flex;
  align-items: center;
}

.header-socials {
  display: flex;
  gap: 16px;
}

.header-socials a {
  color: var(--text-muted);
  transition:
    color 0.2s ease,
    transform 0.2s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

.header-socials a:hover {
  color: var(--text-main);
  transform: translateY(-1px);
}

.header-socials svg {
  width: 18px;
  height: 18px;
}

/* --- MAIN CONTENT STYLES --- */
.hero {
  padding: 80px 0 100px;
  display: flex;
  flex-direction: row;
  align-items: center;
  gap: 48px;
}

.avatar {
  width: 200px;
  height: 200px;
  background: #333;
  color: #fff;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  font-size: 64px;
  font-family: 'Space Grotesk', sans-serif;
  border: 1px solid var(--border);
  overflow: hidden;
  flex-shrink: 0;
}

.profile-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  /* Grayscale and darken to blend with the dark background */
  filter: grayscale(100%) brightness(0.7);
  /* Smooth animation for the color change */
  transition: filter 0.4s ease;
}

/* When the mouse hovers over the avatar circle, restore the image */
.avatar:hover .profile-img {
  filter: grayscale(0%) brightness(1);
}

.hero-kicker {
  font-size: 48px;
  font-weight: 800;
  font-family: 'Space Grotesk', sans-serif;
  line-height: 1;
}

.hero-content h1 {
  font-size: 18px;
  color: var(--text-muted);
  font-weight: 400;
}

.hero-body {
  max-width: 600px;
  color: var(--text-muted);
  line-height: 1.6;
}

.section {
  padding: 80px 0;
  border-top: 1px solid var(--border);
}

.section-title h2 {
  display: flex;
  align-items: center;
  gap: 10px;
  font-family: 'Space Grotesk', sans-serif;
  font-size: 24px;
  margin-bottom: 32px;
}

.section-title .icon {
  display: flex;
  align-items: center;
  color: var(--text-main);
}

.pill-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
}

.pill-grid span {
  padding: 8px 16px;
  border: 1px solid var(--border);
  border-radius: 4px;
  font-size: 14px;
}

.timeline-item {
  margin-bottom: 40px;
  padding-left: 20px;
  border-left: 1px solid var(--border);
}

.timeline-info h3 {
  font-size: 20px;
}

.role,
.meta {
  color: var(--text-muted);
  font-size: 14px;
}

.desc-list {
  padding: 16px 0 0 16px;
  color: var(--text-muted);
  font-size: 14px;
  line-height: 1.6;
}

/* --- HORIZONTAL DRAG & SCROLL ROW --- */
.project-row.full-bleed-row {
  width: 100vw;
  margin-left: calc(50% - 50vw);
  display: flex;
  flex-wrap: nowrap;
  gap: 24px;

  padding-left: max(24px, calc((100vw - 1100px) / 2 + 24px));
  padding-right: max(24px, calc((100vw - 1100px) / 2 + 24px));

  scroll-padding-left: max(24px, calc((100vw - 1100px) / 2 + 24px));

  overflow-x: auto;
  scrollbar-width: none;
  -ms-overflow-style: none;
  cursor: grab;
  scroll-snap-type: x mandatory;
}

.project-row.full-bleed-row::-webkit-scrollbar {
  display: none;
}

.project-row.dragging {
  cursor: grabbing;
  user-select: none;
  scroll-snap-type: none;
}

/* --- PROJECT CARDS --- */
.project-card {
  flex: 0 0 auto;
  width: 350px;
  max-width: 80vw;
  background: var(--card-bg);
  padding: 24px;
  border: 1px solid var(--border);
  border-radius: 8px;
  display: flex;
  flex-direction: column;
  scroll-snap-align: start;
  transition:
    transform 0.3s cubic-bezier(0.2, 0.8, 0.2, 1),
    border-color 0.3s ease,
    box-shadow 0.3s ease,
    background-color 0.3s ease;
}

.project-card:hover {
  transform: translateY(-8px);
  background-color: #282828;
  border-color: rgba(255, 255, 255, 0.3);
  box-shadow: 0 16px 32px rgba(0, 0, 0, 0.5);
}

.project-card h3 {
  margin-bottom: 12px;
}

.project-card p {
  font-size: 14px;
  color: var(--text-muted);
  margin-bottom: 24px;
  flex-grow: 1;
}

.tags {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;
  margin-bottom: 16px;
}

.tags span {
  font-size: 11px;
  color: var(--text-muted);
  border: 1px solid var(--border);
  padding: 4px 10px;
  border-radius: 4px;
}

/* Link styling */
.project-type {
  font-size: 12px;
  text-decoration: underline;
  text-underline-offset: 4px;
  color: var(--text-muted);
  transition: color 0.2s ease;
}

.project-type:hover {
  color: var(--text-main);
}

/* --- MINIMAL FOOTER STYLES --- */
.site-footer {
  padding: 40px 0 60px;
  margin-top: 40px;
  text-align: center;
  font-size: 13px;
  color: var(--text-muted);
  border-top: 1px solid var(--border);
  letter-spacing: 0.5px;
}

.footer-socials {
  display: flex;
  justify-content: center;
  gap: 24px;
  margin-bottom: 20px;
}

.footer-socials a {
  color: var(--text-muted);
  transition:
    color 0.2s ease,
    transform 0.2s ease;
  display: flex;
  align-items: center;
  justify-content: center;
}

.footer-socials a:hover {
  color: var(--text-main);
  transform: translateY(-2px);
}

.footer-socials svg {
  width: 22px;
  height: 22px;
}

/* Responsive Adjustments */
@media (max-width: 768px) {
  .header-left {
    gap: 16px;
  }
  .site-nav {
    gap: 16px;
  }
  .site-nav a {
    font-size: 10px;
    letter-spacing: 1px;
  }
  .header-socials {
    display: none;
  }
  .hero-kicker {
    font-size: 36px;
  }

  .hero {
    flex-direction: column;
    align-items: flex-start;
    gap: 32px;
  }

  .avatar {
    width: 120px;
    height: 120px;
    font-size: 40px;
  }
}
</style>
