<script setup lang="ts">
import { ref, onMounted } from 'vue'
import emailjs from '@emailjs/browser'

const formRef = ref<HTMLFormElement | null>(null)
const sending = ref(false)
const statusMsg = ref('')
const statusColor = ref('')

const name = ref('')
const email = ref('')
const message = ref('')

const sendEmail = async (e: Event) => {
  e.preventDefault()
  if (!formRef.value) return

  sending.value = true
  statusMsg.value = ''
  statusColor.value = ''

  try {
    const response = await emailjs.sendForm(
      import.meta.env.VITE_EMAILJS_SERVICE_ID,
      import.meta.env.VITE_EMAILJS_TEMPLATE_ID,
      formRef.value,
      import.meta.env.VITE_EMAILJS_PUBLIC_KEY
    )

    if (response.status == 200) {
      statusMsg.value = 'Message sent successfully!'
      statusColor.value = 'text-green-400'
      name.value = ''
      email.value = ''
      message.value = ''
    } else {
      statusMsg.value = 'Failed to send message. Please try again'
      statusColor.value = 'text-red-400'
    }
  } catch (error) {
    console.error('EmailJS error: ', error)
    statusMsg.value = 'An error occured while sending. Please try again.'
    statusColor.value = 'text-red-400'
  } finally {
    sending.value = false
  }
}

// Sample data - you can replace with your actual content
type Experience = {
  title: string
  company: string
  period: string
  description: string
  tech: string[]
  image?: string
  link?: string
}
const technologies = ref([
  'Java', 'Python', 'C/C++', 'React', 'Node.js', 'Linux', 'Selenium', 'Cucumber', 'Machine Learning',
  'DBMS', 'PHP', 'Git', 'AWS', 'Embedded Systems', 'Networking', 'Vue.js', 'CI/CD'
])

const experiences = ref<Experience[]>([
  {
    title: 'Enterprise Technology Solutions - Summer Intern',
    company: 'Options Clearing Corporation | Chicago, IL',
    period: 'May 2024 - Aug 2024',
    description: 'Developed and executed automated Cucumber and ServiceNow tests using Java and Selenium to ensure critical business practices and regulatory compliance for enterprise-level applications.',
    image: '/occ_formatted.png',
    tech: ['Java', 'Selenium', 'Cucumber', 'ServiceNow ATF']
  },
  {
    title: 'Full Stack Developer',
    company: 'Ask Captain Cyber',
    period: 'Aug 2024 - May 2025',
    description: 'Engineered and deployed a production-ready AI chatbot using JavaScript, PHP, and Flask on WordPress, applying security best practices to protect data flow and provide real-time cybersecurity insights.',
    link: 'https://acc.cyio.iastate.edu/ask-captain-cyber-chat/',
    image: '/Ask_Captain_Cyber.png',
    tech: ['Javascript', 'PHP', 'Python', 'WordPress']
  },
  {
    title: 'Song Popularity Machine Learning Model',
    company: 'Project',
    period: 'Jan 2025 - May 2025',
    description: 'Built a modular prediction system in Python using Pandas and Scikit-learn to analyze audio datasets, improving accuracy through feature selection and reporting model performance with cross-validation metrics.',
    image: '/Song_Popularity.png',
    link: 'https://github.com/cdnmrph/Song-Popularity-ML-Model',
    tech: ['Python', 'Pandas', 'Scikit-learn']
  },
  {
    title: 'Hourly Android Application',
    company: 'Project',
    period: 'Jan 2023 - May 2023',
    description: 'Collaborated on a small development team to design an Android application for tracking work hours, contributing Kotlin-based components with Jetpack Compose and implementing a CI/CD pipeline using GitHub Actions.',
    image: '/hourly_collage.png',
    tech: ['Kotlin', 'Android Studio', 'Postman']
  },
  {
    title: 'Admissions Call Center Student Supervisor',
    company: 'Iowa State University',
    period: 'Oct 2022 - May 2025',
    description: 'Interviewed, trained, onboarded student employees in order to provide excellent customer service to a variety of inquirers, collaborated across deparments of the university to provide accurate information.',
    image: '/ISU.png',
    tech: ['Salesforce', 'Workday']
  }
])

const currentExperienceIndex = ref(0)

onMounted(() => {
  // Auto-rotate experiences every 9 seconds
  setInterval(() => {
    currentExperienceIndex.value = (currentExperienceIndex.value + 1) % experiences.value.length
  }, 9000)
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
            Computer Engineering Portfolio
          </div>
          <div class="hidden md:flex space-x-8">
            <button @click="scrollToSection('hero')" class="hover:text-web3-accent transition-colors">Home</button>
            <button @click="scrollToSection('about')" class="hover:text-web3-accent transition-colors">About</button>
            <button @click="scrollToSection('experience')"
              class="hover:text-web3-accent transition-colors">Experience</button>
            <button @click="scrollToSection('contact')"
              class="hover:text-web3-accent transition-colors">Contact</button>
          </div>
        </div>
      </div>
    </nav>

    <!-- Hero Section -->
    <section id="hero" class="min-h-screen flex items-center justify-center relative overflow-hidden">
      <!-- Background Effects -->
      <div class="absolute inset-0 bg-gradient-to-br from-web3-dark via-web3-gray to-web3-dark"></div>
      <div class="absolute top-1/4 left-1/4 w-96 h-96 bg-web3-accent/10 rounded-full blur-3xl animate-float"></div>
      <div class="absolute bottom-1/4 right-1/4 w-96 h-96 bg-web3-purple/10 rounded-full blur-3xl animate-float"
        style="animation-delay: -3s;"></div>

      <div class="container-max section-padding text-center relative z-10">
        <div class="max-w-4xl mx-auto">
          <!-- Profile Image Placeholder -->
          <div class="w-48 h-48 mx-auto mb-8 rounded-full bg-gradient-to-br from-web3-accent to-web3-cyan p-1">
            <div class="w-full h-full rounded-full bg-web3-gray flex items-center justify-center">
              <img src="/sitting_formatted_pfp.png" alt="Caden Murphy pfp" class="w-full h-full object-cover rounded-full"/>
            </div>
          </div>

          <h1 class="text-5xl md:text-7xl font-bold mb-6">
            <span class="text-gradient">Caden Murphy</span>
          </h1>


          <p class="text-xl md:text-2xl text-gray-300 mb-8 max-w-2xl mx-auto">
            B.S. in Computer Engineering
          </p>

          <div class="flex flex-col sm:flex-row gap-4 justify-center">
            <button @click="scrollToSection('contact')"
              class="px-8 py-4 bg-gradient-to-r from-web3-accent to-web3-cyan text-black font-semibold rounded-lg hover:scale-105 transition-transform neon-glow">
              Get In Touch
            </button>
            <button @click="scrollToSection('experience')"
              class="px-8 py-4 glass-effect border border-web3-accent/30 text-web3-accent font-semibold rounded-lg hover:bg-web3-accent/10 transition-colors">
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
          <div v-for="tech in [...technologies, ...technologies]" :key="tech"
            class="text-web3-accent font-mono text-lg font-semibold">
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
            About Me
          </h2>

          <div class="grid md:grid-cols-2 gap-12 items-center">
            <div class="space-y-6">
              <p class="text-lg text-gray-300 leading-relaxed">
                Graduate of Iowa State University with a Bachelors in Computer Engineering. Through curriculum and experience, developed skills regarding
                software/hardware development, project management,
                and high level communication. Worked within a highly regulated financial market
                utility environment, incorporating AI into live products, and acted as a point of contact between technical and non-techical parties.
                Passionate about building high quality software designed for the user ensuring security, scalability, and maintainability.
              </p>
              <div class="flex flex-wrap gap-3">
                <span class="px-4 py-2 glass-effect rounded-full text-sm">Full Stack Development</span>
                <span class="px-4 py-2 glass-effect rounded-full text-sm">Quality Assurance</span>
                <span class="px-4 py-2 glass-effect rounded-full text-sm">Machine Learning</span>
                <span class="px-4 py-2 glass-effect rounded-full text-sm">Computer/Software Engineering</span>
                <span class="px-4 py-2 glass-effect rounded-full text-sm">Networking</span>
              </div>
            </div>

            <div class="relative">
              <div
                class="w-full h-96 bg-gradient-to-br from-web3-accent/20 to-web3-purple/20 rounded-2xl p-8 glass-effect overflow-hidden">
                <div class="w-full h-full bg-web3-gray/50 rounded-xl overflow-hidden">
                  <img
                    src="/formatted_pfp.png"
                    alt="About section image"
                    class="w-full h-full object-cover rounded-xl"
                  />
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
            <span class="text-gradient">Experience & Projects</span>
          </h2>

          <div class="relative">
            <!-- Experience Carousel -->
            <div class="overflow-hidden rounded-2xl">
              <div class="flex transition-transform duration-700 ease-in-out"
                :style="{ transform: `translateX(-${currentExperienceIndex * 100}%)` }">
                <div v-for="(exp, index) in experiences" :key="index" class="w-full flex-shrink-0 px-4 md:px-8">
                  <div class="glass-effect rounded-2xl p-8 md:p-12 grid md:grid-cols-2 gap-10 items-center">
                    <!-- Left side: Text -->
                    <div class="space-y-4">
                      <h3 class="text-2xl md:text-3xl font-bold text-gradient">
                        {{ exp.title }}
                      </h3>
                      <p class="text-xl text-web3-accent">
                        {{ exp.company }}
                      </p>
                      <p class="text-gray-400 text-sm mb-4">{{ exp.period }}</p>
                      <p class="text-lg text-gray-300 leading-relaxed border-l-4 border-web3-accent pl-4">
                        {{ exp.description }}
                      </p>
                      <div class="flex flex-wrap gap-2 mt-4">
                        <span v-for="tech in exp.tech" :key="tech"
                          class="px-3 py-1 bg-web3-accent/20 text-web3-accent rounded-full text-sm">
                          {{ tech }}
                        </span>
                      </div>

                      <div v-if="exp.link" class="mt-6">
                        <a :href="exp.link" target="_blank" rel="noopener noreferrer"
                          class="inline-flex items-center gap-2 px-5 py-3 bg-gradient-to-r from-web3-accent to-web3-cyan text-black font-semibold rounded-lg hover:scale-105 transition-transform neon-glow">
                          View Project
                          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor"
                            class="w-5 h-5">
                            <path d="M13.5 4.5H19.5V10.5" />
                            <path d="M19.5 4.5L12 12" />
                            <path
                              d="M19.5 13.5V18C19.5 19.2426 18.4926 20.25 17.25 20.25H6.75C5.50736 20.25 4.5 19.2426 4.5 18V6.75C4.5 5.50736 5.50736 4.5 6.75 4.5H11.25" />
                          </svg>
                        </a>
                      </div>
                    </div>

                    <!-- Right side: Image or Icon -->
                    <div
                      class="w-full h-64 bg-gradient-to-br from-web3-purple/20 to-web3-cyan/20 rounded-xl flex items-center justify-center overflow-hidden">
                      <img v-if="exp.image" :src="exp.image" alt="Project image" class="w-full h-full object-cover" />
                      <span v-else class="text-5xl">💼</span>
                    </div>
                  </div>
                </div>
              </div>
            </div>

            <!-- Carousel Controls -->
            <div class="flex justify-center mt-10 space-x-3">
              <button v-for="(_, index) in experiences" :key="index" @click="currentExperienceIndex = index" :class="[
                'w-3 h-3 rounded-full transition-all duration-300',
                currentExperienceIndex === index
                  ? 'bg-web3-accent scale-125'
                  : 'bg-gray-600 hover:bg-gray-400',
              ]"></button>
            </div>
          </div>
        </div>
      </div>
    </section>
    ```


    <!-- Contact Section -->
    <section id="contact" class="py-24">
      <div class="container-max section-padding">
        <div class="max-w-4xl mx-auto text-center">
          <h2 class="text-4xl md:text-5xl font-bold mb-16">
            <span class="text-gradient">Let's Connect</span>
          </h2>

          <div class="grid md:grid-cols-2 gap-12">
            <div class="space-y-8">
              <div class="glass-effect rounded-2xl p-8">
                <h3 class="text-2xl font-bold mb-6 text-gradient">Get In Touch</h3>
                <p class="text-gray-300 mb-6">
                  Take a look at my sites and continue the conversation!
                </p>
                <div class="space-y-4">
                  <div class="flex items-center space-x-4">
                    <span class="text-web3-accent">📧</span>
                    <span>murphycadenr@gmail.com</span>
                  </div>
                  <div class="flex items-center space-x-4">
                    <span class="text-web3-accent">💼</span>
                    <span><a href="http://www.linkedin.com/in/cadenmurphy">Connect on LinkedIn</a></span>
                  </div>
                  <div class="flex items-center space-x-4">
                    <span class="text-web3-accent">🐙</span>
                    <span><a href="https://github.com/cdnmrph">GitHub</a></span>
                  </div>
                </div>
              </div>
            </div>

            <div class="glass-effect rounded-2xl p-8">
              <h3 class="text-2xl font-bold mb-6 text-gradient">Send Message</h3>
              <form ref="formRef" @submit="sendEmail" class="space-y-6">
                <div>
                  <input v-model="name" type="text" name="name" placeholder="Your Name" required
                    class="w-full p-4 bg-web3-gray/50 border border-gray-600 rounded-lg focus:border-web3-accent focus:outline-none transition-colors">
                </div>
                <div>
                  <input v-model="email" type="email" name="email" placeholder="Your Email" required
                    class="w-full p-4 bg-web3-gray/50 border border-gray-600 rounded-lg focus:border-web3-accent focus:outline-none transition-colors">
                </div>
                <div>
                  <textarea v-model="message" name="message" placeholder="Your Message" rows="4" required
                    class="w-full p-4 bg-web3-gray/50 border border-gray-600 rounded-lg focus:border-web3-accent focus:outline-none transition-colors resize-none"></textarea>
                </div>

                <button type="submit" :disabled="sending"
                  class="w-full py-4 bg-gradient-to-r from-web3-accent to-web3-cyan text-black font-semibold rounded-lg hover:scale-105 transition-transform neon-glow disabled:opacity-50">
                  {{ sending ? 'Sending...' : 'Send Message' }}
                </button>

                <p v-if="statusMsg" :class="['mt-4 font-semibold', statusColor]">{{ statusMsg }}</p>
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
          © 2025 Portfolio. Built with Vue.js & Tailwind CSS.
        </p>
      </div>
    </footer>
  </div>
</template>

<style scoped>
/* Additional custom styles if needed */
</style>
