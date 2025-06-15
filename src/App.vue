<script setup>
import { ref, onMounted, watch } from 'vue'
import logoUxone from './assets/logo-uxone.png'

// Importa las imágenes de proyectos
import project1 from './assets/images/Proyecto-StudyLoop.png'
/*import project2 from './assets/images/proyecto-dashboard.png'
import project3 from './assets/images/proyecto-corporativo.png'
import project4 from './assets/images/proyecto-gestion.png'
import project5 from './assets/images/proyecto-reservas.png'
import project6 from './assets/images/proyecto-blog.png'
*/
const isMobileMenuOpen = ref(false)
const currentYear = new Date().getFullYear()
const isLoading = ref(true)

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
  if (isMobileMenuOpen.value) {
    document.body.style.overflow = 'hidden'
  } else {
    document.body.style.overflow = ''
  }
}

const closeMobileMenu = () => {
  isMobileMenuOpen.value = false
  document.body.style.overflow = ''
}

// Cerrar menú al cambiar el tamaño de la ventana
const handleResize = () => {
  if (window.innerWidth > 768 && isMobileMenuOpen.value) {
    closeMobileMenu()
  }
}

const createStars = () => {
  const starsContainers = document.querySelectorAll('.stars')
  if (!starsContainers.length) return

  starsContainers.forEach(container => {
    const starCount = container.classList.contains('nav-links') ? 50 : 100
    for (let i = 0; i < starCount; i++) {
      const star = document.createElement('div')
      star.className = 'star'
      star.style.left = `${Math.random() * 100}%`
      star.style.top = `${Math.random() * 100}%`
      star.style.width = `${Math.random() * 3}px`
      star.style.height = star.style.width
      star.style.setProperty('--duration', `${Math.random() * 3 + 2}s`)
      star.style.animationDelay = `${Math.random() * 2}s`
      container.appendChild(star)
    }
  })
}

const showMoreProjects = () => {
  const hiddenProjects = document.querySelectorAll('.hidden-project')
  const showMoreBtn = document.getElementById('showMoreProjects')
  
  hiddenProjects.forEach(project => {
    project.classList.add('show')
  })
  
  if (showMoreBtn) {
    showMoreBtn.textContent = 'Ver menos proyectos'
    showMoreBtn.onclick = showLessProjects
  }
}

const showLessProjects = () => {
  const hiddenProjects = document.querySelectorAll('.hidden-project')
  const showMoreBtn = document.getElementById('showMoreProjects')
  
  hiddenProjects.forEach(project => {
    project.classList.remove('show')
  })
  
  if (showMoreBtn) {
    showMoreBtn.textContent = 'Ver más proyectos'
    showMoreBtn.onclick = showMoreProjects
  }
}

onMounted(() => {
  createStars()
  window.addEventListener('resize', handleResize)
  
  // Add click event listener for show more projects button
  const showMoreBtn = document.getElementById('showMoreProjects')
  if (showMoreBtn) {
    showMoreBtn.addEventListener('click', showMoreProjects)
  }
  
  // Simular tiempo de carga
  setTimeout(() => {
    isLoading.value = false
  }, 2000)
})
</script>

<template>
  <div>
    <!-- Loading Screen -->
    <div class="loading-screen" :class="{ 'loading-hidden': !isLoading }">
      <div class="loading-content">
        <div class="loading-text">
          <span class="text-wrapper">
            <span class="word">
              <span class="wave" style="--i:1">C</span>
              <span class="wave" style="--i:2">a</span>
              <span class="wave" style="--i:3">r</span>
              <span class="wave" style="--i:4">g</span>
              <span class="wave" style="--i:5">a</span>
              <span class="wave" style="--i:6">n</span>
              <span class="wave" style="--i:7">d</span>
              <span class="wave" style="--i:8">o</span>
            </span>
            <span class="word">
              <span class="wave" style="--i:9">e</span>
              <span class="wave" style="--i:10">x</span>
              <span class="wave" style="--i:11">p</span>
              <span class="wave" style="--i:12">e</span>
              <span class="wave" style="--i:13">r</span>
              <span class="wave" style="--i:14">i</span>
              <span class="wave" style="--i:15">e</span>
              <span class="wave" style="--i:16">n</span>
              <span class="wave" style="--i:17">c</span>
              <span class="wave" style="--i:18">i</span>
              <span class="wave" style="--i:19">a</span>
            </span>
          </span>
          <span class="dots">
            <span class="dot">.</span>
            <span class="dot">.</span>
            <span class="dot">.</span>
          </span>
        </div>
      </div>
    </div>

    <!-- Overlay para el menú móvil -->
    <div class="menu-overlay" :class="{ active: isMobileMenuOpen }" @click="closeMobileMenu"></div>

    <!-- Navegación -->
    <nav class="navbar">
      <div class="container nav-content">
        <a href="#" class="logo" data-text="uxone">
          <img :src="logoUxone" alt="UXONE Logo" class="logo-img" height="35" width="auto" />
        </a>
        <button class="mobile-menu-btn" :class="{ active: isMobileMenuOpen }" @click="toggleMobileMenu">
          <span></span>
          <span></span>
          <span></span>
        </button>
        <ul class="nav-links" :class="{ active: isMobileMenuOpen }">
          <div class="stars"></div>
          <li><a href="#home" @click="closeMobileMenu">Inicio</a></li>
          <li><a href="#services" @click="closeMobileMenu">Servicios</a></li>
          <li><a href="#projects" @click="closeMobileMenu">Proyectos</a></li>
          <li><a href="#about" @click="closeMobileMenu">Nosotros</a></li>
          <li><a href="#footer" @click="closeMobileMenu">Contactar</a></li>
        </ul>
      </div>
    </nav>

    <!-- Hero Section -->
    <section id="home" class="hero">
      <div class="stars"></div>
      <div class="container">
        <h1 data-text="DISEÑO WEB" class="helvetica-heavy">DISEÑO WEB</h1>
        <p class="subtitle">Transformamos ideas en experiencias digitales Extraordinarias</p>
        <div class="hero-buttons">
          <a href="#footer" class="btn btn-primary">Comenzar Proyecto</a>
          <a href="#projects" class="btn btn-secondary">Ver Proyectos</a>
        </div>
      </div>
    </section>

    <!-- Servicios -->
    <section id="services" class="services">
      <div class="container">
        <h2 class="section-title">Nuestros Servicios</h2>
        <div class="services-grid">
          <div class="service-card">
            <div class="service-icon">
              <i class="fas fa-paint-brush"></i>
            </div>
            <h3>Diseño Web</h3>
            <p>Creamos diseños web modernos y atractivos que cautivan a tus visitantes desde el primer momento.</p>
          </div>
          <div class="service-card">
            <div class="service-icon">
              <i class="fas fa-code"></i>
            </div>
            <h3>Desarrollo Web</h3>
            <p>Desarrollamos aplicaciones web robustas y escalables utilizando las últimas tecnologías como Laravel, Vue.js y Vite.</p>
          </div>
          <div class="service-card">
            <div class="service-icon">
              <i class="fas fa-cogs"></i>
            </div>
            <h3>Mantenimiento Web</h3>
            <p>Ofrecemos servicios de mantenimiento y actualización para mantener tu sitio web funcionando perfectamente.</p>
          </div>
          <div class="service-card">
            <div class="service-icon">
              <i class="fas fa-mobile-alt"></i>
            </div>
            <h3>Diseño Responsive</h3>
            <p>Garantizamos una experiencia perfecta en todos los dispositivos, desde móviles hasta pantallas de escritorio.</p>
          </div>
          <div class="service-card">
            <div class="service-icon">
              <i class="fas fa-search"></i>
            </div>
            <h3>SEO Optimización</h3>
            <p>Mejoramos tu visibilidad en buscadores y aumentamos el tráfico orgánico de tu sitio web.</p>
          </div>
          <div class="service-card">
            <div class="service-icon">
              <i class="fas fa-chart-line"></i>
            </div>
            <h3>Analítica Web</h3>
            <p>Implementamos herramientas de análisis para medir y optimizar el rendimiento de tu sitio web.</p>
          </div>
        </div>
      </div>
    </section>

    <!-- Technologies Carousel -->
    <section id="tecnologias" class="technologies">
      <div class="container">
        <h2 class="section-title">Tecnologías</h2>
        <div class="tech-carousel">
          <div class="tech-track">
            <div class="tech-item">
              <i class="fab fa-html5"></i>
              <span>HTML5</span>
            </div>
            <div class="tech-item">
              <i class="fab fa-css3-alt"></i>
              <span>CSS3</span>
            </div>
            <div class="tech-item">
              <i class="fab fa-js"></i>
              <span>JavaScript</span>
            </div>
            <div class="tech-item">
              <i class="fab fa-php"></i>
              <span>PHP</span>
            </div>
            <div class="tech-item">
              <i class="fab fa-laravel"></i>
              <span>Laravel</span>
            </div>
            <div class="tech-item">
              <i class="fab fa-vuejs"></i>
              <span>Vue.js</span>
            </div>
            <!-- Duplicate items for seamless loop -->
            <div class="tech-item">
              <i class="fab fa-html5"></i>
              <span>HTML5</span>
            </div>
            <div class="tech-item">
              <i class="fab fa-css3-alt"></i>
              <span>CSS3</span>
            </div>
            <div class="tech-item">
              <i class="fab fa-js"></i>
              <span>JavaScript</span>
            </div>
            <div class="tech-item">
              <i class="fab fa-php"></i>
              <span>PHP</span>
            </div>
            <div class="tech-item">
              <i class="fab fa-laravel"></i>
              <span>Laravel</span>
            </div>
            <div class="tech-item">
              <i class="fab fa-vuejs"></i>
              <span>Vue.js</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Proyectos -->
    <section id="projects" class="projects">
      <div class="container">
        <h2 class="section-title">Nuestros Proyectos</h2>
        <div class="projects-grid">
          <div class="project-card">
            <img :src="project1" alt="Proyecto StudyLoop" class="project-image">
            <div class="project-overlay">
              <h3 class="project-title">EstudyLoop</h3>
              <p class="project-description">App web para estudiantes, manejar y organizar sus tareas y apuntes.</p>
              <div class="project-tags">
                <span class="project-tag"><i class="fab fa-vuejs"></i> Vue.js</span>
                <span class="project-tag"><i class="fab fa-figma"></i> Figma</span>
              </div>
              <a href="https://u-x-o-n-e.github.io/Focus-App/" class="btn-ver-en-vivo">Ver en vivo</a>
            </div>
          </div>
          <!--
          <div class="project-card">
            <img :src="project2" alt="Proyecto Dashboard Analytics" class="project-image">
            <div class="project-overlay">
              <h3 class="project-title">Dashboard Analytics</h3>
              <p class="project-description">Panel de control con visualización de datos en tiempo real.</p>
              <div class="project-tags">
                <span class="project-tag"><i class="fab fa-vuejs"></i> Vue.js</span>
                <span class="project-tag"><i class="fab fa-vite"></i> Vite</span>
                <span class="project-tag"><i class="fab fa-css3-alt"></i> Tailwind</span>
              </div>
              <a href="#" class="btn-ver-en-vivo">Ver en vivo</a>
            </div>
          </div>
          <div class="project-card">
            <img :src="project3" alt="Proyecto Portal Corporativo" class="project-image">
            <div class="project-overlay">
              <h3 class="project-title">Portal Corporativo</h3>
              <p class="project-description">Sitio web corporativo con diseño moderno y responsive.</p>
              <div class="project-tags">
                <span class="project-tag"><i class="fab fa-laravel"></i> Laravel</span>
                <span class="project-tag"><i class="fab fa-vuejs"></i> Vue.js</span>
                <span class="project-tag"><i class="fab fa-figma"></i> Figma</span>
              </div>
              <a href="#" class="btn-ver-en-vivo">Ver en vivo</a>
            </div>
          </div>
          <div class="project-card hidden-project">
            <img :src="project4" alt="Proyecto Sistema de Gestión" class="project-image">
            <div class="project-overlay">
              <h3 class="project-title">Sistema de Gestión</h3>
              <p class="project-description">Plataforma integral para gestión empresarial.</p>
              <div class="project-tags">
                <span class="project-tag"><i class="fab fa-laravel"></i> Laravel</span>
                <span class="project-tag"><i class="fab fa-vuejs"></i> Vue.js</span>
                <span class="project-tag"><i class="fab fa-php"></i> PHP</span>
              </div>
              <a href="#" class="btn-ver-en-vivo">Ver en vivo</a>
            </div>
          </div>
          <div class="project-card hidden-project">
            <img :src="project5" alt="Proyecto App de Reservas" class="project-image">
            <div class="project-overlay">
              <h3 class="project-title">App de Reservas</h3>
              <p class="project-description">Sistema de reservas online con calendario integrado.</p>
              <div class="project-tags">
                <span class="project-tag"><i class="fab fa-vuejs"></i> Vue.js</span>
                <span class="project-tag"><i class="fab fa-vite"></i> Vite</span>
                <span class="project-tag"><i class="fab fa-js"></i> JavaScript</span>
              </div>
              <a href="#" class="btn-ver-en-vivo">Ver en vivo</a>
            </div>
          </div>
          <div class="project-card hidden-project">
            <img :src="project6" alt="Proyecto Blog Personal" class="project-image">
            <div class="project-overlay">
              <h3 class="project-title">Blog Personal</h3>
              <p class="project-description">Blog moderno con sistema de comentarios y categorías.</p>
              <div class="project-tags">
                <span class="project-tag"><i class="fab fa-html5"></i> HTML5</span>
                <span class="project-tag"><i class="fab fa-css3-alt"></i> CSS3</span>
                <span class="project-tag"><i class="fab fa-js"></i> JavaScript</span>
              </div>
              <a href="#" class="btn-ver-en-vivo">Ver en vivo</a>
            </div>
          </div>
        </div>
        <div class="projects-more">
          <button class="btn btn-secondary" id="showMoreProjects">Ver más proyectos</button>
        -->
        </div>
      </div>
    </section>

    <!-- About Us Section -->
    <section id="about" class="about">
      <div class="container">
        <h2 class="section-title">Sobre Nosotros</h2>
        <div class="about-content">
          <div class="about-text">
            <h3>Transformando Ideas en Experiencias Digitales Extraordinarias</h3>
            <p>En UXONE, somos un equipo apasionado de diseñadores y desarrolladores que creamos soluciones digitales innovadoras. Nuestra misión es transformar tu visión en una experiencia digital memorable que cautive a tus clientes.</p>
            <div class="about-stats">
              <div class="stat-item">
                <span class="stat-number">2+</span>
                <span class="stat-label">Años de Experiencia</span>
              </div>
              <div class="stat-item">
                <span class="stat-number">20+</span>
                <span class="stat-label">Proyectos Completados</span>
              </div>
              <div class="stat-item">
                <span class="stat-number">14+</span>
                <span class="stat-label">Clientes Satisfechos</span>
              </div>
            </div>
          </div>
          <div class="about-image">
            <img src="https://images.unsplash.com/photo-1522071820081-009f0129c71c?ixlib=rb-4.0.3&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1170&q=80" alt="Nuestro equipo">
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer id="footer" class="footer">
      <div class="container">
        <div class="footer-grid">
          <div>
            <h3><img :src="logoUxone" alt="UXONE Logo" class="logo-img" height="33" width="auto" /></h3>
            <p>Transformando ideas en experiencias digitales extraordinarias.</p>
            <div class="contact-info">
              <p><i class="fas fa-map-marker-alt"></i> Posadas, Misiones, Argentina</p>
              <p><i class="fas fa-envelope"></i> uxone.ar@gmail.com</p>
            </div>
          </div>
          <div>
            <h3>Servicios</h3>
            <ul class="footer-links">
              <li><a href="#services">Diseño Web</a></li>
              <li><a href="#services">Desarrollo Web</a></li>
              <li><a href="#services">Mantenimiento</a></li>
              <li><a href="#services">Consultoría</a></li>
            </ul>
          </div>
          <div>
            <h3>Tecnologías</h3>
            <ul class="footer-links">
              <li><a href="#tecnologias">Laravel</a></li>
              <li><a href="#tecnologias">Vue.js</a></li>
              <li><a href="#tecnologias">Figma</a></li>
              <li><a href="#tecnologias">WordPress</a></li>
            </ul>
          </div>
          <div>
            <h3>Síguenos</h3>
            <div class="social-links">
              <a href="#" aria-label="Facebook">
                <i class="fab fa-facebook"></i>
              </a>
              <a href="#" aria-label="Instagram">
                <i class="fab fa-instagram"></i>
              </a>
              <a href="#" aria-label="GitHub">
                <i class="fab fa-github"></i>
              </a>
              <a href="#" aria-label="LinkedIn">
                <i class="fab fa-linkedin"></i>
              </a>
            </div>
          </div>
        </div>
        <div class="footer-bottom">
          <p>
            &copy; {{ currentYear }}
            <span class="footer-uxone">
              <span class="footer-ux">UX</span><span class="footer-one">ONE</span>
              <sup>™</sup>
            </span>
            . Todos los derechos reservados.
          </p>
        </div>
      </div>
    </footer>
  </div>
</template>

<style>
@import url('https://rsms.me/inter/inter.css');
@import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0/css/all.min.css');

/* Loading Screen Styles */
.loading-screen {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: var(--darker-bg);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 9999;
  transition: opacity 0.5s ease-out, visibility 0.5s ease-out;
}

.loading-screen.loading-hidden {
  opacity: 0;
  visibility: hidden;
}

.loading-content {
  text-align: center;
}

.loading-text {
  font-family: 'ClashDisplay', sans-serif;
  font-size: clamp(1.2rem, 6vw, 2.5rem);
  font-weight: 700;
  color: var(--white);
  display: flex;
  align-items: center;
  gap: clamp(0.3rem, 2vw, 1rem);
}

.text-wrapper {
  display: inline-flex;
  align-items: center;
  gap: clamp(0.5rem, 3vw, 1.5rem);
}

.word {
  display: inline-flex;
  align-items: center;
}

.wave {
  display: inline-block;
  animation: wave 2s ease-in-out infinite;
  color: var(--white);
  animation-delay: calc(0.1s * var(--i));
  transform-origin: bottom;
}

.dots {
  display: flex;
  gap: clamp(0.1rem, 1vw, 0.5rem);
  margin-left: clamp(0.2rem, 1vw, 0.5rem);
}

.dot {
  opacity: 0;
  animation: dotTyping 1.4s infinite;
  font-size: 0.8em;
}

.dot:nth-child(2) {
  animation-delay: 0.2s;
}

.dot:nth-child(3) {
  animation-delay: 0.4s;
}

@keyframes wave {
  0%, 100% {
    transform: translateY(0) rotate(0deg);
  }
  25% {
    transform: translateY(-20px) rotate(5deg);
  }
  50% {
    transform: translateY(0) rotate(0deg);
  }
  75% {
    transform: translateY(20px) rotate(-5deg);
  }
}

@keyframes dotTyping {
  0%, 20% {
    opacity: 0;
    transform: translateY(0);
  }
  50% {
    opacity: 1;
    transform: translateY(-5px);
  }
  80%, 100% {
    opacity: 0;
    transform: translateY(0);
  }
}

@media (max-width: 768px) {
  .loading-text {
    font-size: clamp(1.1rem, 8vw, 2rem);
  }
}

/* About Section Styles */
.about {
  padding: 100px 0;
  background-color: var(--darker-bg);
  position: relative;
}

.about::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 1px;
  background: linear-gradient(90deg, transparent, var(--white), transparent);
}

.about-content {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
}

.about-text h3 {
  font-size: 2.5rem;
  margin-bottom: 1.5rem;
  color: var(--white);
  line-height: 1.2;
}

.about-text p {
  font-size: 1.1rem;
  color: var(--text-color);
  margin-bottom: 2rem;
  line-height: 1.8;
}

.about-stats {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
  margin-top: 3rem;
}

.stat-item {
  text-align: center;
}

.stat-number {
  display: block;
  font-size: 2.5rem;
  font-weight: 700;
  color: var(--primary-color);
  margin-bottom: 0.5rem;
}

.stat-label {
  color: var(--text-color);
  font-size: 1rem;
}

.about-image {
  position: relative;
  border-radius: var(--border-radius);
  overflow: hidden;
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3);
}

.about-image img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.5s ease;
}

.about-image:hover img {
  transform: scale(1.05);
}

@media (max-width: 768px) {
  .about-content {
    grid-template-columns: 1fr;
    gap: 2rem;
  }

  .about-text h3 {
    font-size: 2rem;
  }

  .about-stats {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }

  .services-grid {
    grid-template-columns: 1fr;
    gap: 1.5rem;
  }

  .service-card {
    padding: 1.5rem;
  }

  .service-icon {
    width: 50px;
    height: 50px;
  }

  .service-card h3 {
    font-size: 1.5rem;
  }

  .service-card p {
    font-size: 1rem;
  }
}

@font-face {
  font-family: 'Helvetica Neue Heavy';
  src: url('./assets/fonts/HelveticaNeueHeavy.otf') format('opentype');
  font-weight: 900;
  font-style: normal;
  font-display: swap;
}

.helvetica-heavy {
  font-family: 'Helvetica Neue Heavy', 'ClashDisplay', sans-serif !important;
  font-weight: 900 !important;
}
</style>
