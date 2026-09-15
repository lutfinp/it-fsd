<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const galleryItems = [
    {
        id: 1,
        title: "Momen Bareng Pimpinan & Tim",
        desc: "Kehangatan dan kebersamaan antara pimpinan dan anggota tim IT FSD.",
        tag: "⭐ Kebersamaan",
        src: "/images/gallery/gallery-1.jpg",
        category: "Kebersamaan",
    },
    {
        id: 2,
        title: "Kekompakan Skuad FSD",
        desc: "Pose bersama penuh gaya dan antusiasme tinggi saat perayaan event spesial perusahaan.",
        tag: "🔥 Team Spirit",
        src: "/images/gallery/gallery-2.jpg",
        category: "Kebersamaan",
    },
    {
        id: 3,
        title: "Perayaan Ulang Tahun & Tumpengan Tim",
        desc: "Momen kehangatan seluruh anggota tim IT FSD saat merayakan acara ulang tahun bersama dengan potong tumpeng di kantor.",
        tag: "🎂 Ultah & Tumpengan",
        src: "/images/gallery/gallery-3.jpg",
        category: "Kebersamaan",
    },
];

const activeFilter = ref("Semua");
const filters = ["Semua", "Events", "Kebersamaan"];

const selectedIndex = ref(null);

const filteredItems = computed(() => {
    if (activeFilter.value === "Semua") return galleryItems;
    return galleryItems.filter((item) => item.category === activeFilter.value);
});

function openLightbox(index) {
    selectedIndex.value = index;
    document.body.style.overflow = "hidden";
}

function closeLightbox() {
    selectedIndex.value = null;
    document.body.style.overflow = "";
}

function nextImage() {
    if (selectedIndex.value !== null) {
        selectedIndex.value =
            (selectedIndex.value + 1) % filteredItems.value.length;
    }
}

function prevImage() {
    if (selectedIndex.value !== null) {
        selectedIndex.value =
            (selectedIndex.value - 1 + filteredItems.value.length) %
            filteredItems.value.length;
    }
}

function handleKeydown(e) {
    if (selectedIndex.value === null) return;
    if (e.key === "Escape") closeLightbox();
    if (e.key === "ArrowRight") nextImage();
    if (e.key === "ArrowLeft") prevImage();
}

onMounted(() => {
    window.addEventListener("keydown", handleKeydown);
});

onUnmounted(() => {
    window.removeEventListener("keydown", handleKeydown);
    document.body.style.overflow = "";
});
</script>

<script>
import { computed } from "vue";
</script>

<template>
    <section id="galeri" class="gallery-section">
        <div class="container">
            <div class="text-center">
                <span class="eyebrow">📸 Momen & Kebersamaan</span>
                <h2 class="section-title">
                    Galeri <span class="grad">IT FSD</span>
                </h2>
                <p class="section-desc">
                    Dokumentasi keseruan, kekompakan, dan semangat juang tim IT
                    FSD dalam berbagai event dan aktivitas seru.
                </p>
            </div>

            <!-- Filter Buttons -->
            <!-- <div class="filters-wrap">
        <button
          v-for="f in filters"
          :key="f"
          class="filter-btn"
          :class="{ active: activeFilter === f }"
          @click="activeFilter = f"
        >
          {{ f }}
        </button>
      </div> -->

            <!-- Gallery Grid -->
            <div class="gallery-grid">
                <div
                    v-for="(item, idx) in filteredItems"
                    :key="item.id"
                    class="gallery-card card"
                    @click="openLightbox(idx)"
                >
                    <div class="img-wrapper">
                        <img :src="item.src" :alt="item.title" loading="lazy" />
                        <div class="img-overlay">
                            <span class="zoom-icon">🔍</span>
                            <span class="overlay-tag">{{ item.tag }}</span>
                        </div>
                    </div>
                    <div class="card-body">
                        <div class="card-header">
                            <span class="tag-chip">{{ item.tag }}</span>
                        </div>
                        <h3>{{ item.title }}</h3>
                        <p>{{ item.desc }}</p>
                    </div>
                </div>
            </div>
        </div>

        <!-- Lightbox Modal -->
        <Teleport to="body">
            <Transition name="fade">
                <div
                    v-if="selectedIndex !== null"
                    class="lightbox-overlay"
                    @click.self="closeLightbox"
                >
                    <button
                        class="lightbox-close"
                        aria-label="Tutup"
                        @click="closeLightbox"
                    >
                        &times;
                    </button>

                    <button
                        v-if="filteredItems.length > 1"
                        class="lightbox-nav prev"
                        aria-label="Sebelumnya"
                        @click.stop="prevImage"
                    >
                        &#10094;
                    </button>

                    <div class="lightbox-content" @click.stop>
                        <img
                            :src="filteredItems[selectedIndex].src"
                            :alt="filteredItems[selectedIndex].title"
                        />
                        <div class="lightbox-caption">
                            <span class="lightbox-tag">{{
                                filteredItems[selectedIndex].tag
                            }}</span>
                            <h3>{{ filteredItems[selectedIndex].title }}</h3>
                            <p>{{ filteredItems[selectedIndex].desc }}</p>
                        </div>
                    </div>

                    <button
                        v-if="filteredItems.length > 1"
                        class="lightbox-nav next"
                        aria-label="Berikutnya"
                        @click.stop="nextImage"
                    >
                        &#10095;
                    </button>
                </div>
            </Transition>
        </Teleport>
    </section>
</template>

<style scoped>
.gallery-section {
    padding: 96px 0;
    background: var(--dark);
}

.filters-wrap {
    display: flex;
    justify-content: center;
    gap: 12px;
    margin-top: 32px;
    margin-bottom: 48px;
    flex-wrap: wrap;
}

.filter-btn {
    padding: 8px 20px;
    border-radius: 999px;
    border: 1px solid var(--border);
    background: var(--dark-soft);
    color: var(--muted);
    font-size: 0.9rem;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.25s ease;
}

.filter-btn:hover {
    border-color: var(--primary);
    color: var(--text);
}

.filter-btn.active {
    background: var(--gradient);
    color: #0b1020;
    border-color: transparent;
    font-weight: 800;
    box-shadow: 0 4px 16px rgba(52, 207, 235, 0.3);
}

.gallery-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(270px, 1fr));
    gap: 24px;
}

.gallery-card {
    padding: 0;
    overflow: hidden;
    cursor: pointer;
    display: flex;
    flex-direction: column;
    border: 1px solid var(--border);
    transition:
        transform 0.3s ease,
        border-color 0.3s ease,
        box-shadow 0.3s ease;
}

.gallery-card:hover {
    transform: translateY(-8px);
    border-color: var(--primary);
    box-shadow: 0 16px 40px rgba(52, 207, 235, 0.2);
}

.img-wrapper {
    position: relative;
    width: 100%;
    aspect-ratio: 4 / 3;
    overflow: hidden;
    background: var(--dark-soft);
}

.img-wrapper img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    transition: transform 0.5s ease;
}

.gallery-card:hover .img-wrapper img {
    transform: scale(1.08);
}

.img-overlay {
    position: absolute;
    inset: 0;
    background: rgba(11, 16, 32, 0.6);
    backdrop-filter: blur(3px);
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 8px;
    opacity: 0;
    transition: opacity 0.3s ease;
}

.gallery-card:hover .img-overlay {
    opacity: 1;
}

.zoom-icon {
    font-size: 2rem;
    transform: scale(0.7);
    transition: transform 0.3s ease;
}

.gallery-card:hover .zoom-icon {
    transform: scale(1);
}

.overlay-tag {
    font-size: 0.8rem;
    font-weight: 700;
    color: var(--primary);
    background: rgba(11, 16, 32, 0.8);
    padding: 4px 12px;
    border-radius: 999px;
    border: 1px solid var(--primary);
}

.card-body {
    padding: 20px;
    display: flex;
    flex-direction: column;
    flex: 1;
}

.card-header {
    margin-bottom: 8px;
}

.tag-chip {
    font-size: 0.75rem;
    font-weight: 700;
    color: var(--primary);
    background: rgba(52, 207, 235, 0.1);
    padding: 3px 10px;
    border-radius: 999px;
    border: 1px solid rgba(52, 207, 235, 0.25);
}

.card-body h3 {
    font-size: 1.1rem;
    font-weight: 800;
    color: var(--text);
    margin-bottom: 6px;
    line-height: 1.3;
}

.card-body p {
    font-size: 0.88rem;
    color: var(--muted);
    line-height: 1.5;
}

/* Lightbox Modal */
.lightbox-overlay {
    position: fixed;
    inset: 0;
    z-index: 9999;
    background: rgba(5, 8, 18, 0.92);
    backdrop-filter: blur(16px);
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 24px;
}

.lightbox-close {
    position: absolute;
    top: 24px;
    right: 28px;
    background: rgba(255, 255, 255, 0.1);
    border: 1px solid rgba(255, 255, 255, 0.2);
    color: #fff;
    font-size: 2.2rem;
    line-height: 1;
    width: 48px;
    height: 48px;
    border-radius: 50%;
    cursor: pointer;
    display: grid;
    place-items: center;
    transition:
        background 0.2s,
        transform 0.2s;
    z-index: 10001;
}

.lightbox-close:hover {
    background: rgba(255, 255, 255, 0.25);
    transform: scale(1.1);
}

.lightbox-nav {
    position: absolute;
    top: 50%;
    transform: translateY(-50%);
    background: rgba(255, 255, 255, 0.1);
    border: 1px solid rgba(255, 255, 255, 0.2);
    color: #fff;
    font-size: 1.6rem;
    width: 52px;
    height: 52px;
    border-radius: 50%;
    cursor: pointer;
    display: grid;
    place-items: center;
    transition:
        background 0.2s,
        transform 0.2s;
    z-index: 10001;
}

.lightbox-nav:hover {
    background: var(--primary);
    color: #0b1020;
    transform: translateY(-50%) scale(1.1);
}

.lightbox-nav.prev {
    left: 28px;
}

.lightbox-nav.next {
    right: 28px;
}

.lightbox-content {
    max-width: 900px;
    width: 100%;
    background: var(--dark-soft);
    border: 1px solid var(--border);
    border-radius: 20px;
    overflow: hidden;
    box-shadow:
        0 30px 90px rgba(0, 0, 0, 0.8),
        0 0 40px rgba(52, 207, 235, 0.2);
    display: flex;
    flex-direction: column;
    max-height: 90vh;
}

.lightbox-content img {
    width: 100%;
    max-height: 65vh;
    object-fit: contain;
    background: #050812;
}

.lightbox-caption {
    padding: 24px 28px;
    background: var(--dark-soft);
}

.lightbox-tag {
    display: inline-block;
    font-size: 0.8rem;
    font-weight: 700;
    color: var(--primary);
    background: rgba(52, 207, 235, 0.12);
    padding: 4px 12px;
    border-radius: 999px;
    margin-bottom: 10px;
    border: 1px solid rgba(52, 207, 235, 0.3);
}

.lightbox-caption h3 {
    font-size: 1.35rem;
    font-weight: 800;
    color: var(--text);
    margin-bottom: 6px;
}

.lightbox-caption p {
    color: var(--muted);
    font-size: 0.95rem;
}

/* Transitions */
.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.3s ease;
}
.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}

@media (max-width: 768px) {
    .lightbox-nav {
        width: 42px;
        height: 42px;
        font-size: 1.2rem;
    }
    .lightbox-nav.prev {
        left: 12px;
    }
    .lightbox-nav.next {
        right: 12px;
    }
    .lightbox-close {
        top: 16px;
        right: 16px;
        width: 40px;
        height: 40px;
        font-size: 1.8rem;
    }
    .gallery-grid {
        grid-template-columns: 1fr;
        gap: 16px;
    }
    .lightbox-caption {
        padding: 16px 20px;
    }
    .lightbox-caption h3 {
        font-size: 1.1rem;
    }
}

@media (max-width: 480px) {
    .lightbox-overlay {
        padding: 12px;
        align-items: flex-end;
    }
    .lightbox-content {
        border-radius: 20px 20px 0 0;
        max-height: 88vh;
    }
    .lightbox-content img {
        max-height: 55vh;
    }
    .lightbox-nav {
        width: 36px;
        height: 36px;
        font-size: 1rem;
    }
    .lightbox-nav.prev { left: 8px; }
    .lightbox-nav.next { right: 8px; }
}
</style>
