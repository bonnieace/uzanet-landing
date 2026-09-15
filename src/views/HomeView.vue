<script setup lang="ts">
import { ref } from 'vue'
import TitleComponent from '@/components/TitleComponent.vue'

const mobileMenuOpen = ref(false)
const currentYear = new Date().getFullYear()
const portalOrigin = (import.meta.env.VITE_PORTAL_URL || 'https://mikrotikke.netlify.app').replace(
  /\/$/,
  '',
)
const onboardingUrl = `${portalOrigin}/onboard`
const apiDocsUrl = import.meta.env.VITE_API_DOCS_URL || 'https://api.uzanet.co.ke/docs'
const showPricing = import.meta.env.VITE_SHOW_PUBLIC_PRICING === 'true'
const showCustomerProof = import.meta.env.VITE_SHOW_CUSTOMER_PROOF === 'true'
</script>

<style>
[v-cloak] {
  display: none;
}
.gradient-bg {
  background: linear-gradient(135deg, #0f2027 0%, #203a43 50%, #2c5364 100%);
}
.code-block {
  background-color: #1e293b;
  border-radius: 0.5rem;
  padding: 1.5rem;
  overflow-x: auto;
  color: #e2e8f0;
  font-family: monospace;
}
.nav-link {
  position: relative;
}
.nav-link::after {
  content: '';
  position: absolute;
  bottom: -2px;
  left: 0;
  width: 0;
  height: 2px;
  background-color: #3b82f6;
  transition: width 0.3s ease;
}
.nav-link:hover::after {
  width: 100%;
}
</style>
<template>
  <div class="font-sans text-gray-800 antialiased" v-cloak>
    <div id="app">
      <!-- Navigation -->
      <nav class="bg-white shadow-md fixed w-full z-14">
        <div class="container mx-auto px-4 md:px-6 lg:px-8">
          <div class="flex justify-between items-center py-4">
            <div class="flex items-center">
              <img
                src="/GAMER.png"
                alt="Uzanet Logo"
                class="h-10 mr-3"
              />
            </div>

            <!-- Desktop Navigation -->
            <div class="hidden md:flex items-center space-x-8">
              <a
                href="#services"
                class="nav-link text-gray-700 hover:text-blue-600 font-medium transition duration-300"
                >Services</a
              >
              <a
                href="#how-it-works"
                class="nav-link text-gray-700 hover:text-blue-600 font-medium transition duration-300"
                >How It Works</a
              >
              <a
                href="#developer"
                class="nav-link text-gray-700 hover:text-blue-600 font-medium transition duration-300"
                >Developers</a
              >
              <a
                v-if="showPricing"
                href="#pricing"
                class="nav-link text-gray-700 hover:text-blue-600 font-medium transition duration-300"
                >Pricing</a
              >
              <a
                href="#contact"
                class="bg-blue-600 hover:bg-blue-700 text-white font-medium py-2 px-4 rounded-md transition duration-300"
                >Get Started</a
              >
            </div>

            <!-- Mobile Menu Button -->
            <div class="md:hidden flex items-center">
              <button
                type="button"
                @click="mobileMenuOpen = !mobileMenuOpen"
                class="text-gray-700 focus:outline-none"
                aria-label="Toggle navigation menu"
                :aria-expanded="mobileMenuOpen"
                aria-controls="mobile-navigation"
              >
                <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path
                    v-if="!mobileMenuOpen"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M4 6h16M4 12h16M4 18h16"
                  ></path>
                  <path
                    v-else
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                    d="M6 18L18 6M6 6l12 12"
                  ></path>
                </svg>
              </button>
            </div>
          </div>
        </div>

        <!-- Mobile Menu -->
        <div id="mobile-navigation" v-if="mobileMenuOpen" class="md:hidden bg-white shadow-lg py-2">
          <a
            href="#services"
            @click="mobileMenuOpen = false"
            class="block px-4 py-2 text-gray-700 hover:bg-blue-50"
            >Services</a
          >
          <a
            href="#how-it-works"
            @click="mobileMenuOpen = false"
            class="block px-4 py-2 text-gray-700 hover:bg-blue-50"
            >How It Works</a
          >
          <a
            href="#developer"
            @click="mobileMenuOpen = false"
            class="block px-4 py-2 text-gray-700 hover:bg-blue-50"
            >Developers</a
          >
          <a
            v-if="showPricing"
            href="#pricing"
            @click="mobileMenuOpen = false"
            class="block px-4 py-2 text-gray-700 hover:bg-blue-50"
            >Pricing</a
          >
          <a
            href="#contact"
            @click="mobileMenuOpen = false"
            class="block px-4 py-2 text-blue-600 font-medium hover:bg-blue-50"
            >Get Started</a
          >
        </div>
      </nav>

      <!-- Hero Section -->
      <section class="relative overflow-hidden  pt-24 pb-16 md:pt-32 md:pb-24 bg-gradient-to-br from-blue-600 to-purple-600 text-white">
  <!-- Decorative animated blobs -->
  <div class="absolute top-0 left-0 w-72 h-72 bg-purple-500 opacity-30 rounded-full mix-blend-multiply filter blur-3xl animate-blob"></div>
  <div class="absolute bottom-0 right-0 w-96 h-96 bg-blue-300 opacity-20 rounded-full mix-blend-multiply filter blur-3xl animate-blob animation-delay-2000"></div>
  
  <div class="container mx-auto px-4 md:px-6 lg:px-8 relative z-10 flex flex-col-reverse md:flex-row items-center">
    <!-- Text Content -->
    <div class="md:w-1/2 space-y-6">
      <h1 class="text-4xl md:text-5xl font-extrabold leading-tight">
        Simplified 
        <span class="bg-clip-text text-transparent bg-gradient-to-r from-white to-purple-300">
          Internet Solutions.
        </span>
      </h1>
      <p class="text-lg md:text-xl text-gray-200">
        Cheap , Fast & Secure Solutions designed to elevate your digital experience. Join us in shaping the future of internet services in Africa.        
        
      </p>
      <div class="flex flex-col sm:flex-row gap-4">
        <a href="#services" class="inline-flex items-center justify-center bg-white text-blue-600 font-semibold py-3 px-6 rounded-lg shadow-lg hover:shadow-xl transition">
          Get Started
        </a>
        <a href="#developer" class="inline-flex items-center justify-center border-2 border-white text-white font-semibold py-3 px-6 rounded-lg hover:bg-white hover:text-blue-600 transition">
          Try API
        </a>
      </div>
      
    </div>

    <!-- Illustrative Media -->
    <div class="md:w-1/2 mb-10 md:mb-0 flex justify-center">
      <img 
        src="/1.svg" 
        alt="Abstract network illustration" 
        class="w-full max-w-md rounded-xl "
      />
    </div>

  </div>
  <!-- Feature Icons Row -->
  <div class="mt-24 px-4 md:px-6 lg:px-8 relative z-10">
    <div class="grid grid-cols-2 sm:grid-cols-3 gap-6">
      <!-- First row on mobile (2 items) -->
      <div class="flex flex-col items-center text-center space-y-2">
        <img class="w-16 h-16 sm:w-24 sm:h-24" src="/hotspot.svg" alt="ISP Billing Software"/>
        <span class="text-sm sm:text-base">ISP Billing Software</span>
      </div>
      <div class="flex flex-col items-center text-center space-y-2">
        <img class="w-16 h-16 sm:w-24 sm:h-24" src="/host.svg" alt="Web & Cloud Hosting"/>
        <span class="text-sm sm:text-base">Web & Cloud Hosting</span>
      </div>
      <!-- Second row on mobile (1 item), same row on desktop -->
      <div class="col-span-2 sm:col-span-1 flex flex-col items-center text-center space-y-2">
        <img class="w-16 h-16 sm:w-24 sm:h-24" src="/pro.svg" alt="API-as-a-Service"/>
        <span class="text-sm sm:text-base">API-as-a-Service</span>
      </div>
    </div>
  </div>
</section>

      <!-- Services Section -->
      <section id="services" class="py-24 bg-gray-50">
        <div class="container mx-auto px-4 md:px-6 lg:px-8">
          <TitleComponent
          image="/space.svg"
            title="Our Services"
            subtitle="Comprehensive solutions designed for everyone from small ISPs to large enterprises. Our services are tailored to meet the unique needs of your network, ensuring seamless connectivity and management."
          />


          <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
            <!-- Service Card 1 -->
            <div
              class="bg-white rounded-lg shadow-lg overflow-hidden transition duration-300 hover:shadow-xl"
            >
              <div class="p-6">
                <div class="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center mb-4">
                  <i class="fas fa-server text-blue-600 text-xl"></i>
                </div>
                <h3 class="text-xl font-bold mb-2">ISP Software Suite</h3>
                <ul class="space-y-2 mb-4">
                  <li class="flex items-start">
                    <i class="fas fa-check text-green-500 mt-1 mr-2"></i>
                    <span>Billing, package management, user provisioning (Hotspot & PPPoE).</span>
                  </li>
                  <li class="flex items-start">
                    <i class="fas fa-check text-green-500 mt-1 mr-2"></i>
                    <span>Real-time RX/TX monitoring.</span>
                  </li>
                  <li class="flex items-start">
                    <i class="fas fa-check text-green-500 mt-1 mr-2"></i>
                    <span>User management and access control.</span>
                  </li>
                </ul>
                <a href="#" class="text-blue-600 hover:text-blue-800 font-medium flex items-center">
                  Learn more
                  <svg
                    class="w-4 h-4 ml-1"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M9 5l7 7-7 7"
                    ></path>
                  </svg>
                </a>
              </div>
            </div>

            <!-- Service Card 2 -->
            <div
              class="bg-white rounded-lg shadow-lg overflow-hidden transition duration-300 hover:shadow-xl"
            >
              <div class="p-6">
                <div class="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center mb-4">
                  <i class="fas fa-code text-blue-600 text-xl"></i>
                </div>
                <h3 class="text-xl font-bold mb-2">API as a Service</h3>
                <ul class="space-y-2 mb-4">
                  <li class="flex items-start">
                    <i class="fas fa-check text-green-500 mt-1 mr-2"></i>
                    <span>Fully documented REST endpoints for payments, user management.</span>
                  </li>
                  <li class="flex items-start">
                    <i class="fas fa-check text-green-500 mt-1 mr-2"></i>
                    <span>Logs and network statistics endpoints.</span>
                  </li>
                  <li class="flex items-start">
                    <i class="fas fa-check text-green-500 mt-1 mr-2"></i>
                    <span>Instant onboarding.</span>
                  </li>
                </ul>
                <a href="#" class="text-blue-600 hover:text-blue-800 font-medium flex items-center">
                  Learn more
                  <svg
                    class="w-4 h-4 ml-1"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M9 5l7 7-7 7"
                    ></path>
                  </svg>
                </a>
              </div>
            </div>

            <!-- Service Card 3 -->
            <div
              class="bg-white rounded-lg shadow-lg overflow-hidden transition duration-300 hover:shadow-xl"
            >
              <div class="p-6">
                <div class="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center mb-4">
                  <i class="fas fa-wifi text-blue-600 text-xl"></i>
                </div>
                <h3 class="text-xl font-bold mb-2">MikroTik & Access Point Sales</h3>
                <ul class="space-y-2 mb-4">
                  <li class="flex items-start">
                    <i class="fas fa-check text-green-500 mt-1 mr-2"></i>
                    <span>MikroTik routers and access-point options for supported deployments.</span>
                  </li>
                  <li class="flex items-start">
                    <i class="fas fa-check text-green-500 mt-1 mr-2"></i>
                    <span>Deployment sizing and hardware sourcing guidance.</span>
                  </li>
                  <li class="flex items-start">
                    <i class="fas fa-check text-green-500 mt-1 mr-2"></i>
                    <span>Pre-configured hardware options available.</span>
                  </li>
                </ul>
                <a href="#" class="text-blue-600 hover:text-blue-800 font-medium flex items-center">
                  Learn more
                  <svg
                    class="w-4 h-4 ml-1"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M9 5l7 7-7 7"
                    ></path>
                  </svg>
                </a>
              </div>
            </div>

            <!-- Service Card 4 -->
            <div
              class="bg-white rounded-lg shadow-lg overflow-hidden transition duration-300 hover:shadow-xl"
            >
              <div class="p-6">
                <div class="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center mb-4">
                  <i class="fas fa-palette text-blue-600 text-xl"></i>
                </div>
                <h3 class="text-xl font-bold mb-2">Hotspot Landing-Page Customization</h3>
                <ul class="space-y-2 mb-4">
                  <li class="flex items-start">
                    <i class="fas fa-check text-green-500 mt-1 mr-2"></i>
                    <span>Custom hotspot login.</span>
                  </li>
                  <li class="flex items-start">
                    <i class="fas fa-check text-green-500 mt-1 mr-2"></i>
                    <span>payment intergrated login.</span>
                  </li>
                  <li class="flex items-start">
                    <i class="fas fa-check text-green-500 mt-1 mr-2"></i>
                    <span>Mobile-responsive designs.</span>
                  </li>
                </ul>
                <a href="#" class="text-blue-600 hover:text-blue-800 font-medium flex items-center">
                  Learn more
                  <svg
                    class="w-4 h-4 ml-1"
                    fill="none"
                    stroke="currentColor"
                    viewBox="0 0 24 24"
                    xmlns="http://www.w3.org/2000/svg"
                  >
                    <path
                      stroke-linecap="round"
                      stroke-linejoin="round"
                      stroke-width="2"
                      d="M9 5l7 7-7 7"
                    ></path>
                  </svg>
                </a>
              </div>
            </div>

            <!-- Service Card 5 -->
            <div
              class="bg-white rounded-lg shadow-lg overflow-hidden transition duration-300 hover:shado