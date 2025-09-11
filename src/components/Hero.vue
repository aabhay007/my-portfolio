<template>
  <div class="container">
    <!-- Navigation -->
    <nav class="navbar">
      <div class="nav-content">
        <div class="logo">
          <span>Portfolio</span>
        </div>
        <div class="nav-links">
          <a href="#about">About</a>
          <a href="#projects">Projects</a>
          <a href="#contact">Contact</a>
        </div>
      </div>
    </nav>
    
    <!-- Hero Section -->
    <section class="hero">
      <div class="hero-content">
        <div class="hero-text">
          <h1>Hi, I'm <span class="highlight">Abhay</span></h1>
          <div class="typewriter">{{ displayedText }}<span class="cursor">|</span></div>
          <div class="social-links">
            <a href="https://github.com/aabhay007" data-aos="fade-up" data-aos-delay="200">
              
              _<Icon name="lucide:github" size="24" />_
            </a>
            <a href="https://www.linkedin.com/in/abhay-bundel-540481271/" data-aos="fade-up" data-aos-delay="300">
              
              _<Icon name="lucide:linkedin" size="24" />_
            </a>
          </div>
        </div>
      </div>
    </section>

    <!-- Skills Section -->
    <section id="about" class="skills">
      <h2 data-aos="fade-up">Skills & Technologies</h2>
      <div class="skills-grid">
        <div v-for="(skillSet, index) in skills" :key="skillSet.category" class="skill-card" data-aos="fade-up"
          :data-aos-delay="index * 100">
          <h3>{{ skillSet.category }}</h3>
          <div class="tech-tags">
            <span v-for="tech in skillSet.technologies" :key="tech" class="tech-tag">
              {{ tech }}
            </span>
          </div>
        </div>
      </div>
    </section>

    <!-- Projects Section -->
    <section id="projects" class="projects">
      <h2 data-aos="fade-up">Featured Projects</h2>
      <div class="projects-grid">
        <div v-for="(project, index) in projects" :key="project.title" class="project-card" data-aos="fade-up"
          :data-aos-delay="index * 100">
          <h3>{{ project.title }}</h3>
          <p>{{ project.description }}</p>
          <div class="project-tags">
            <span v-for="tag in project.tags" :key="tag" class="project-tag">
              {{ tag }}
            </span>
          </div>
          <div class="project-links">
            <a :href="project.links.github">
              
              _<Icon name="lucide:github" size="20" />_
            </a>
            <a :href="project.links.live">
              
              _<Icon name="lucide:external-link" size="20" />_
            </a>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="contact">
      <h2 data-aos="fade-up">Get in Touch</h2>
      <div class="contact-card" data-aos="fade-up" data-aos-delay="100">
        <div class="contact-item">
          <Icon name="lucide:mail" size="20" />
          <a href="mailto:abhay007official@gmail.com">abhay007official@gmail.com</a>
        </div>
        <div class="contact-item">
          <Icon name="lucide:linkedin" size="20" />
          <a href="https://www.linkedin.com/in/abhay-bundel-540481271/">linkedin.com/in/abhay</a>
        </div>
        <div class="contact-item">
          <Icon name="lucide:github" size="20" />
          <a href="https://github.com/aabhay007">github.com/aabhay007</a>
        </div>
      </div>
    </section>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import AOS from 'aos';
import 'aos/dist/aos.css';

const texts = ["Full Stack Developer", "Software Developer", "Problem Solver"];
const displayedText = ref("");
let textIndex = 0;
let charIndex = 0;
let isDeleting = false;

const typeEffect = () => {
  const currentText = texts[textIndex];

  if (isDeleting) {
    displayedText.value = currentText.substring(0, charIndex--);
  } else {
    displayedText.value = currentText.substring(0, charIndex++);
  }

  if (!isDeleting && charIndex === currentText.length) {
    setTimeout(() => (isDeleting = true), 1000);
  } else if (isDeleting && charIndex === 0) {
    isDeleting = false;
    textIndex = (textIndex + 1) % texts.length;
  }

  setTimeout(typeEffect, isDeleting ? 50 : 100);
};

onMounted(typeEffect);
// Initialize AOS
onMounted(() => {
  AOS.init({
    duration: 1000,
    once: true,
    offset: 100
  });
});

const projects = ref([
  {
    title: "E-Commerce Platform",
    description: "Built a full-stack e-commerce platform using Dotnet MVC. Implemented features like user authentication, payment processing, and order management.",
    tags: ["Dotnet", "MVC", "MSSQL", "Stripe"],
    links: {
      github: "https://github.com/aabhay007/Ecomm_Web",
      live: "https://ecommerce-demo.com"
    }
  },
  {
    title: "MOCO",
    description: "Developed a project for Fun, using .Net core and Nuxt/Vue JS here we can upload images for free and in return we can get their live links",
    tags: ["NUXT JS", "Open Auth", ".NET CORE","Postgres DB"],
    links: {
      github: "https://github.com/aabhay007/moco-backend",
      live: "https://moco-frontend.vercel.app"
    }
  },
  {
    title: "AG Grid(POC)",
    description: "This is POC to demonstrate how to create a high performance AG Grid. Which handles 10 Millions+ records easily with out breaking and smooth performance.",
    tags: ["VUE JS", "AG GRID", "HYPER FORMULA"],
    links: {
      github: "https://github.com/aabhay007/AgGrid_With_HyperFormula",
      live: "https://ag-grid-with-hyper-formula.vercel.app/"
    }
  }
]);

const skills = ref([
  {
    category: "Frontend",
    technologies: ["Vue JS", "React JS", "TypeScript", "Javascript", "Tailwind CSS"]
  },
  {
    category: "Backend",
    technologies: ["DotNet", "Python", "Node JS", "Django", "PostgreSQL", "MSSQL", "MySQL"]
  },
  {
    category: "Tools & Others",
    technologies: ["Git", "Docker", "AWS", "Azure", "AI Tools"]
  }
]);
</script>

<style scoped>
/* Previous styles remain the same */
.typewriter-container {
  font-size: 24px;
  font-weight: bold;
}
/* Add new styles for typewriter effect */
.typewriter-container {
  height: 50px;
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 1rem 0;
}

.typewriter {
  font-size: 24px;
  font-weight: bold;
  white-space: nowrap;
  overflow: hidden;
}
.cursor {
  animation: blink 1s infinite;
}
@keyframes blink {
  50% { opacity: 0; }
}
/* Animation transitions */
.skill-card,
.project-card,
.contact-card {
  transition: transform 0.3s ease;
}

.skill-card:hover,
.project-card:hover {
  transform: translateY(-5px);
}

/* Ensure AOS animations work properly */
[data-aos] {
  pointer-events: none;
}

[data-aos].aos-animate {
  pointer-events: auto;
}

/* Previous responsive styles remain the same */
</style>

<style scoped>
/* Base Styles */
.container {
  min-height: 100vh;
  background-color: #f9fafb;
}

/* Navigation */
.navbar {
  position: fixed;
  top: 0;
  width: 100%;
  background-color: white;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
  z-index: 1000;
}

.nav-content {
  max-width: 1280px;
  margin: 0 auto;
  padding: 1rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.logo span {
  font-size: 1.25rem;
  font-weight: bold;
  color: #111827;
}

.nav-links {
  display: flex;
  gap: 2rem;
}

.nav-links a {
  color: #4b5563;
  text-decoration: none;
  transition: color 0.3s;
}

.nav-links a:hover {
  color: #111827;
}

/* Hero Section */
.hero {
  padding: 8rem 1rem 6rem;
  background: linear-gradient(to right, #2563eb, #4f46e5);
  color: white;
}

.hero-content {
  max-width: 1280px;
  margin: 0 auto;
  text-align: center;
}

.hero h1 {
  font-size: 3rem;
  font-weight: bold;
  margin-bottom: 1rem;
}

.highlight {
  color: #bfdbfe;
}

.social-links {
  display: flex;
  justify-content: center;
  gap: 1.5rem;
  margin-top: 2rem;
}

.social-links a {
  color: #bfdbfe;
  transition: color 0.3s;
}

.social-links a:hover {
  color: white;
}

/* Skills Section */
.skills {
  padding: 5rem 1rem;
}

.skills h2 {
  text-align: center;
  font-size: 2rem;
  font-weight: bold;
  color: #111827;
  margin-bottom: 3rem;
}

.skills-grid {
  max-width: 1280px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  padding: 0 1rem;
}

.skill-card {
  background: white;
  padding: 1.5rem;
  border-radius: 0.5rem;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.skill-card h3 {
  font-size: 1.25rem;
  font-weight: 600;
  color: #111827;
  margin-bottom: 1rem;
}

.tech-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.tech-tag {
  background-color: #dbeafe;
  color: #1e40af;
  padding: 0.25rem 0.75rem;
  border-radius: 9999px;
  font-size: 0.875rem;
}

/* Projects Section */
.projects {
  padding: 5rem 1rem;
  background-color: #f3f4f6;
}

.projects h2 {
  text-align: center;
  font-size: 2rem;
  font-weight: bold;
  color: #111827;
  margin-bottom: 3rem;
}

.projects-grid {
  max-width: 1280px;
  margin: 0 auto;
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
}

.project-card {
  background: white;
  padding: 1.5rem;
  border-radius: 0.5rem;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.project-card h3 {
  font-size: 1.25rem;
  font-weight: 600;
  color: #111827;
  margin-bottom: 1rem;
}

.project-card p {
  color: #4b5563;
  margin-bottom: 1rem;
}

.project-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  margin-bottom: 1rem;
}

.project-tag {
  background-color: #f3f4f6;
  color: #4b5563;
  padding: 0.25rem 0.5rem;
  border-radius: 0.25rem;
  font-size: 0.875rem;
}

.project-links {
  display: flex;
  gap: 1rem;
}

.project-links a {
  color: #4b5563;
  transition: color 0.3s;
}

.project-links a:hover {
  color: #111827;
}

/* Contact Section */
.contact {
  padding: 5rem 1rem;
}

.contact h2 {
  text-align: center;
  font-size: 2rem;
  font-weight: bold;
  color: #111827;
  margin-bottom: 3rem;
}

.contact-card {
  max-width: 32rem;
  margin: 0 auto;
  background: white;
  padding: 1.5rem;
  border-radius: 0.5rem;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.contact-item {
  display: flex;
  align-items: center;
  gap: 0.75rem;
  padding: 0.75rem 0;
}

.contact-item:not(:last-child) {
  border-bottom: 1px solid #e5e7eb;
}

.contact-item svg {
  color: #2563eb;
}

.contact-item a {
  color: #4b5563;
  text-decoration: none;
  transition: color 0.3s;
}

.contact-item a:hover {
  color: #111827;
}

/* Responsive Design */
@media (max-width: 768px) {
  .nav-content {
    padding: 1rem 2rem;
  }

  .hero h1 {
    font-size: 2.5rem;
  }

  .skills-grid,
  .projects-grid {
    grid-template-columns: 1fr;
  }
}

/* Smooth Scrolling */
html {
  scroll-behavior: smooth;
}
</style>
