<script setup>
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import StatsSection from './components/StatsSection.vue'
import PerksSection from './components/PerksSection.vue'
import TeamSection from './components/TeamSection.vue'
import VoteCampaignSection from './components/VoteCampaignSection.vue'
import TestimonialSection from './components/TestimonialSection.vue'
import CTASection from './components/CTASection.vue'
import FooterSection from './components/FooterSection.vue'
</script>

<template>
  <NavBar />
  <main>
    <HeroSection />
    <StatsSection />
    <PerksSection />
    <TeamSection />
    <VoteCampaignSection />
    <TestimonialSection />
    <CTASection />
  </main>
  <FooterSection />
</template>