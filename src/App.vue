<script setup lang="ts">
import { ref, onMounted } from 'vue'

// Sample data - you can replace with your actual content
type Experience = {
  title: string
  company: string
  period: string
  description: string
  tech: string[]
  image?: string // e.g. "/experiences/occ-intern.jpg" placed under public/
  link?: string  // optional external project/case-study URL
}
const technologies = ref([
  'TypeScript', 'Vue.js', 'React', 'Node.js', 'Python', 'Java', 
  'C/C++', 'Linux', 'Selenium', 'Cucumber', 'Machine Learning', 'GraphQL',
  'PostgreSQL', 'MongoDB', 'Docker', 'AWS', 'Git', 'PHP', 'Networking', 'Embedded Systems'
])

const experiences = ref<Experience[]>([
  {
    title: 'Enterprise Technology Solutions - Summer Intern',
    company: 'Options Clearing Corporation | Chicago, IL',
    period: 'May 2024 - Aug 2024',
    description: 'Developed and executed automated Cucumber and ServiceNow tests using Java and Selenium to ensure critical business practices and regulatory compliance for enterprise-level applications.',
    tech: ['Java', 'Selenium', 'Cucumber', 'ServiceNow ATF']
  },
  {
    title: 'Full Stack Developer',
    company: 'Ask Captain Cyber',
    period: 'Aug 2024 - May 2025',
    description: 'Engineered and deployed a production-ready AI chatbot using JavaScript, PHP, and Flask on WordPress, applying security best practices to protect data flow and provide real-time cybersecurity insights.',
    link: 'https://acc.cyio.iastate.edu/ask-captain-cyber-chat/',
    image: '/public/Ask_Captian_Cyber.png',
    tech: ['Javascript', 'PHP', 'Python', 'WordPress']
  },
  {
    title: 'Song Popularity Machine Learning Model',
    company: 'Project',
    period: 'Jan 2025 - May 2025',
    description: 'Built a modular prediction system in Python using Pandas and Scikit-learn to analyze audio datasets, improving accuracy through feature selection and reporting model performance with cross-validation metrics.',
    tech: ['Python', 'Pandas', 'Scikit-learn']
  },
  {
    title: 'Hourly Android Application',
    company: 'Project',
    period: 'Jan 2023 - May 2023',
    description: 'Collaborated on a small development team to design an Android application for tracking work hours, contributing Kotlin-based components with Jetpack Compose and implementing a CI/CD pipeline using GitHub Actions.',
    tech: ['Kotlin', 'Android Studio', 'Postman']
  },
  {
    title: 'Admissions Call Center Student Supervisor',
    company: 'Iowa State University',
    period: 'Oct 2022 - May 2025',
    description: 'Interviewed, trained, onboarded student employees in order to provide excellent customer service to a variety of inquirers, collaborated across deparments of the university to provide accurate information.',
    tech: ['Salesforce', 'Workday']
  }
])

const currentExperienceIndex = ref(0)

onMounted(() => {
  // Auto-rotate experiences every 5 seconds
  setInterval(() => {
    currentExperienceIndex.value = (currentExperienceIndex.value + 1) % experiences.value.length
  }, 5000)
})

const scrollToSection = (sectionId: string) => {
  const element = document.getElementById(sectionId)
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' })
  }
}
</script>

<template>
  <div class="min-h-screen bg-web3-dark text-white">
    <!-- Navigation -->
    <nav class="fixed top-0 w-full z-50 glass-effect">
      <div class="container-max section-padding py-4">
        <div class="flex justify-between items-center">
          <div class="text-2xl font-bold text-gradient">
            Portfolio
          </div>
          <div class="hidden md:flex space-x-8">
            <button @click="scrollToSection('hero')" class="hover:text-web3-accent transition-colors">Home</button>
            <button @click="scrollToSection('about')" class="hover:text-web3-accent transition-colors">About</button>
            <button @click="scrollToSection('experience')" class="hover:text-web3-accent transition-colors">Experience</button>
            <button @click="scrollToSection('contact')" class="hover:text-web3-accent transition-colors">Contact</button>
          </div>
        </div>
      </div>
    </nav>

    <!-- Hero Section -->
    <section id="hero" class="min-h-screen flex items-center justify-center relative overflow-hidden">
      <!-- Background Effects -->
      <div class="absolute inset-0 bg-gradient-to-br from-web3-dark via-web3-gray to-web3-dark"></div>
      <div class="absolute top-1/4 left-1/4 w-96 h-96 bg-web3-accent/10 rounded-full blur-3xl animate-float"></div>
      <div class="absolute bottom-1/4 right-1/4 w-96 h-96 bg-web3-purple/10 rounded-full blur-3xl animate-float" style="animation-delay: -3s;"></div>
      
      <div class="container-max section-padding text-center relative z-10">
        <div class="max-w-4xl mx-auto">
          <!-- Profile Image Placeholder -->
          <div class="w-48 h-48 mx-auto mb-8 rounded-full bg-gradient-to-br from-web3-accent to-web3-cyan p-1">
            <div class="w-full h-full rounded-full bg-web3-gray flex items-center justify-center">
              <span class="text-4xl">👨‍💻</span>
            </div>
          </div>
          
          <h1 class="text-5xl md:text-7xl font-bold mb-6">
            <span class="text-gradient">Caden Murphy</span>
          </h1>
          
          
          <p class="text-xl md:text-2xl text-gray-300 mb-8 max-w-2xl mx-auto">
            B.S. in Computer Engineering
          </p>
          
          <div class="flex flex-col sm:flex-row gap-4 justify-center">
            <button @click="scrollToSection('contact')" class="px-8 py-4 bg-gradient-to-r from-web3-accent to-web3-cyan text-black font-semibold rounded-lg hover:scale-105 transition-transform neon-glow">
              Get In Touch
            </button>
            <button @click="scrollToSection('experience')" class="px-8 py-4 glass-effect border border-web3-accent/30 text-web3-accent font-semibold rounded-lg hover:bg-web3-accent/10 transition-colors">
              View Experience
            </button>
          </div>
        </div>
      </div>
    </section>

    <!-- Tech Ticker -->
    <section class="py-8 bg-web3-gray/50 overflow-hidden">
      <div class="flex animate-ticker">
        <div class="flex space-x-8 whitespace-nowrap">
          <div v-for="tech in [...technologies, ...technologies]" :key="tech" class="text-web3-accent font-mono text-lg font-semibold">
            {{ tech }}
          </div>
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="py-24">
      <div class="container-max section-padding">
        <div class="max-w-6xl mx-auto">
          <h2 class="text-4xl md:text-5xl font-bold text-center mb-16">
            About <span class="text-gradient">Me</span>
          </h2>
          
          <div class="grid md:grid-cols-2 gap-12 items-center">
            <div class="space-y-6">
              <p class="text-lg text-gray-300 leading-relaxed">
               Graduate of Iowa State University in Computer Engineering. Developed strong skills regarding software/hardware development, project management,
               and high level communication skills. Has experience working within a highly regulated financial market utility environment and incorporating AI 
               into live products. Passionate about building high quality software designed for the user and interacting with technical and non-technical parties.
              </p>
              <div class="flex flex-wrap gap-3">
                <span class="px-4 py-2 glass-effect rounded-full text-sm">Full Stack Development</span>
                <span class="px-4 py-2 glass-effect rounded-full text-sm">Project Management</span>
                <span class="px-4 py-2 glass-effect rounded-full text-sm">Quality Assurance</span>
              </div>
            </div>
            
            <div class="relative">
              <div class="w-full h-96 bg-gradient-to-br from-web3-accent/20 to-web3-purple/20 rounded-2xl p-8 glass-effect">
                <div class="w-full h-full bg-web3-gray/50 rounded-xl flex items-center justify-center">
                  <span class="text-6xl">🚀</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Experience Section -->
    <section id="experience" class="py-24 bg-web3-gray/30">
      <div class="container-max section-padding">
        <div class="max-w-6xl mx-auto">
          <h2 class="text-4xl md:text-5xl font-bold text-center mb-16">
            <span class="text-gradient">Experience</span> & Projects
          </h2>
          
          <div class="relative">
            <!-- Experience Carousel -->
            <div class="overflow-hidden rounded-2xl">
              <div class="flex transition-transform duration-500 ease-in-out" :style="{ transform: `translateX(-${currentExperienceIndex * 100}%)` }">
                <div v-for="(exp, index) in experiences" :key="index" class="w-full flex-shrink-0">
                  <div class="glass-effect rounded-2xl p-8 md:p-12">
                    <div class="grid md:grid-cols-2 gap-8 items-center">
                      <div>
                        <div>
                        <h3 class="text-2xl md:text-3xl font-bold mb-4 text-gradient">{{ exp.title }}</h3>
                        <p class="text-xl text-web3-accent mb-2">{{ exp.company }}</p>
                        <p class="text-gray-400 mb-6">{{ exp.period }}</p>
                        <p class="text-lg text-gray-300 leading-relaxed mb-6">{{ exp.description }}</p>
                        <div class="flex flex-wrap gap-2">
                          <span v-for="tech in exp.tech" :key="tech" class="px-3 py-1 bg-web3-accent/20 text-web3-accent rounded-full text-sm">
                            {{ tech }}
                          </span>
                        </div>
                      </div>
                      <div class="w-full h-64 bg-gradient-to-br from-web3-purple/20 to-web3-cyan/20 rounded-xl flex items-center justify-center overflow-hidden">
                          <img 
                            v-if="exp.image"
                            :src="exp.image"
                            alt="Project image"
                            class="w-full h-full object-cover"
                          />
                        <span v-else class="text-4xl">💼</span>
                      </div>
                    </div>
                    <div v-if="exp.link" class="mt-6">
                      <a 
                        :href="exp.link" 
                        target="_blank" 
                        rel="noopener noreferrer"
                        class="inline-flex items-center gap-2 px-5 py-3 bg-gradient-to-r from-web3-accent to-web3-cyan text-black font-semibold rounded-lg hover:scale-105 transition-transform neon-glow"
                      >
                        View Project
                        <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-5 h-5">
                          <path d="M13.5 4.5H19.5V10.5"/>
                          <path d="M19.5 4.5L12 12"/>
                          <path d="M19.5 13.5V18C19.5 19.2426 18.4926 20.25 17.25 20.25H6.75C5.50736 20.25 4.5 19.2426 4.5 18V6.75C4.5 5.50736 5.50736 4.5 6.75 4.5H11.25"/>
                        </svg>
                      </a>
                    </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            
            <!-- Carousel Controls -->
            <div class="flex justify-center mt-8 space-x-4">
              <button 
                v-for="(_, index) in experiences" 
                :key="index"
                @click="currentExperienceIndex = index"
                :class="[
                  'w-3 h-3 rounded-full transition-all duration-300',
                  currentExperienceIndex === index ? 'bg-web3-accent scale-125' : 'bg-gray-600 hover:bg-gray-400'
                ]"
              ></button>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="py-24">
      <div class="container-max section-padding">
        <div class="max-w-4xl mx-auto text-center">
          <h2 class="text-4xl md:text-5xl font-bold mb-16">
            Let's <span class="text-gradient">Connect</span>
          </h2>
          
          <div class="grid md:grid-cols-2 gap-12">
            <div class="space-y-8">
              <div class="glass-effect rounded-2xl p-8">
                <h3 class="text-2xl font-bold mb-6 text-gradient">Get In Touch</h3>
                <p class="text-gray-300 mb-6">
                  Ready to collaborate on your next Web3 project? Let's discuss how we can build something amazing together.
                </p>
                <div class="space-y-4">
                  <div class="flex items-center space-x-4">
                    <span class="text-web3-accent">📧</span>
                    <span>your.email@example.com</span>
                  </div>
                  <div class="flex items-center space-x-4">
                    <span class="text-web3-accent">💼</span>
                    <span>LinkedIn Profile</span>
                  </div>
                  <div class="flex items-center space-x-4">
                    <span class="text-web3-accent">🐙</span>
                    <span>GitHub Profile</span>
                  </div>
                </div>
              </div>
            </div>
            
            <div class="glass-effect rounded-2xl p-8">
              <h3 class="text-2xl font-bold mb-6 text-gradient">Send Message</h3>
              <form class="space-y-6">
                <div>
                  <input 
                    type="text" 
                    placeholder="Your Name" 
                    class="w-full p-4 bg-web3-gray/50 border border-gray-600 rounded-lg focus:border-web3-accent focus:outline-none transition-colors"
                  >
                </div>
                <div>
                  <input 
                    type="email" 
                    placeholder="Your Email" 
                    class="w-full p-4 bg-web3-gray/50 border border-gray-600 rounded-lg focus:border-web3-accent focus:outline-none transition-colors"
                  >
                </div>
                <div>
                  <textarea 
                    placeholder="Your Message" 
                    rows="4"
                    class="w-full p-4 bg-web3-gray/50 border border-gray-600 rounded-lg focus:border-web3-accent focus:outline-none transition-colors resize-none"
                  ></textarea>
                </div>
                <button 
                  type="submit"
                  class="w-full py-4 bg-gradient-to-r from-web3-accent to-web3-cyan text-black font-semibold rounded-lg hover:scale-105 transition-transform neon-glow"
                >
                  Send Message
                </button>
              </form>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="py-8 border-t border-gray-800">
      <div class="container-max section-padding text-center">
        <p class="text-gray-400">
          © 2024 Web3 Portfolio. Built with Vue.js & Tailwind CSS.
        </p>
      </div>
    </footer>
  </div>
</template>

<style scoped>
/* Additional custom styles if needed */
</style>
