<template>
    <nav class="navbar">
      <!-- Dynamic Island container -->
      <div 
        class="dynamic-island" 
        :class="{ expanded: isHovered }" 
        @mouseover="isHovered = true" 
        @mouseleave="isHovered = false"
      >
        <div class="logo">
          <NuxtLink to="/">A</NuxtLink>
        </div>
  
        <ul v-if="isHovered" class="nav-links">
          <li><NuxtLink to="/">Home</NuxtLink></li>
          <li><NuxtLink to="/about">About</NuxtLink></li>
          <li><NuxtLink to="/projects">Projects</NuxtLink></li>
          <li><NuxtLink to="/contact">Contact</NuxtLink></li>
        </ul>
      </div>
    </nav>
  </template>
  
  <script setup>
  import { ref } from "vue";
  
  const isHovered = ref(false);
  </script>
  
  <style scoped>
  /* Navbar Container */
  .navbar {
    display: none;
    justify-content: center;
    align-items: center;
    padding: 1rem;
    background: transparent;
    position: fixed;
    top: 20px;
    left: 50%;
    transform: translateX(-50%);
    z-index: 100;
  }
  
  /* Dynamic Island Style */
  .dynamic-island {
    background: linear-gradient(135deg, #222, #333);
    color: white;
    padding: 0.6rem 1.2rem;
    border-radius: 30px;
    display: flex;
    align-items: center;
    gap: 1rem;
    transition: all 0.4s ease-in-out;
    cursor: pointer;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
    min-width: 50px;
    justify-content: center;
    overflow: hidden;
  }
  
  /* Hover effect - Expands */
  .dynamic-island.expanded {
    min-width: 350px;
    padding: 1rem 2rem;
    border-radius: 40px;
    background: linear-gradient(135deg, #111, #444);
    box-shadow: 0 8px 20px rgba(0, 255, 204, 0.5);
  }
  
  /* Logo */
  .logo a {
    font-size: 1.4rem;
    font-weight: bold;
    color: white;
    text-decoration: none;
    transition: transform 0.3s ease;
  }
  
  /* Navigation Links */
  .nav-links {
    display: flex;
    gap: 1rem;
    list-style: none;
    opacity: 0;
    transition: opacity 0.3s ease-in-out;
  }
  
  .dynamic-island.expanded .nav-links {
    opacity: 1;
  }
  
  .nav-links a {
    color: white;
    text-decoration: none;
    font-size: 1rem;
    font-weight: bold;
    transition: color 0.3s ease-in-out;
  }
  
  .nav-links a:hover {
    color: #00ffcc;
  }
  
  /* Responsive */
  @media (max-width: 768px) {
    .dynamic-island.expanded {
      min-width: 250px;
    }
  }
  </style>
  