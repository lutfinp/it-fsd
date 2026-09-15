<script setup>
import { ref, computed } from "vue";

const projects = [
    {
        id: "beproactive",
        name: "Be Proactive Campaign",
        category: "Campaign & Support",
        icon: "☕",
        badge: "Voting App",
        desc: "Mengembangkan platform digital terintegrasi untuk mendukung rangkaian proses BeProactive Campaign, mulai dari voting Best Employee, Best Leader, dan Best Department hingga feedback 360° dan evaluasi antar-Department secara lebih terstruktur dan terdigitalisasi.",
        metrics: "Integrated 360° Feedback",
    },
    {
        id: "elit-gias",
        name: "ELITE GIAS",
        category: "Enterprise (ELITE)",
        icon: "⚡",
        badge: "Core ERP",
        desc: "Platform Enterprise & Operasional terintegrasi untuk mengelola seluruh ekosistem bisnis GIAS secara akurat dan real-time.",
        metrics: "400+ Active Users",
    },
    {
        id: "elit-mbc",
        name: "ELITE MBC",
        category: "Enterprise (ELITE)",
        icon: "🏬",
        badge: "Enterprise",
        desc: "Sistem operasional dan manajemen workflows bisnis unit MBC yang dirancang tinggi performa dan intuitif.",
        metrics: "High Availability",
    },
    {
        id: "elit-dpp",
        name: "ELITE DPP",
        category: "Enterprise (ELITE)",
        icon: "📊",
        badge: "Planning & Data",
        desc: "Sistem operasional dan manajemen workflows bisnis unit DDP yang dirancang tinggi performa dan intuitif.",
        metrics: "Real-time Sync",
    },
    {
        id: "elit-suite",
        name: "ELITE Systems (Lainnya)",
        category: "Enterprise (ELITE)",
        icon: "🚀",
        badge: "Ecosystem",
        desc: "Ekosistem modul & micro-applications ELITE pendukung operasional cabang serta integrasi sistem bisnis internal.",
        metrics: "Multi-branch Support",
    },
    {
        id: "hris-gias",
        name: "HRIS GIAS",
        category: "HR & Talent",
        icon: "👥",
        badge: "Employee Portal",
        desc: "Sistem Informasi Sumber Daya Manusia GIAS untuk absensi digital, penggajian, perizinan, dan portal karyawan.",
        metrics: "全 Corporate Portal",
    },
    {
        id: "hrms",
        name: "HRMS Platform",
        category: "HR & Talent",
        icon: "🏆",
        badge: "Management",
        desc: "Human Resource Management System komprehensif untuk pengawasan talent, evaluasi kinerja, dan struktur organisasi.",
        metrics: "KPI & Performance",
    },
    {
        id: "helpdesk",
        name: "IT Helpdesk",
        category: "Support & Edu",
        icon: "🎧",
        badge: "Ticketing System",
        desc: "Platform penanganan tiket kendala IT, sistem antrean penanganan masalah, dan SLA monitoring terpadu.",
        metrics: "Fast Response SLA",
    },
    {
        id: "lms",
        name: "LMS (Learning Management System)",
        category: "Support & Edu",
        icon: "📚",
        badge: "E-Learning",
        desc: "Platform pembelajaran & pelatihan mandiri karyawan dengan modul kursus interaktif, evaluasi, dan pelacakan progress.",
        metrics: "Interactive Modules",
    },
];

const activeCategory = ref("Semua");
const categories = [
    "Semua",
    "Enterprise (ELITE)",
    "HR & Talent",
    "Support & Edu",
];

const selectedProject = ref(null);

const filteredProjects = computed(() => {
    if (activeCategory.value === "Semua") return projects;
    return projects.filter((p) => p.category === activeCategory.value);
});

function openProjectModal(project) {
    selectedProject.value = project;
}

function closeProjectModal() {
    selectedProject.value = null;
}
</script>

<template>
    <section id="project" class="projects-section">
        <div class="container">
            <div class="text-center">
                <span class="eyebrow">💻 Ekosistem Sistem & Aplikasi</span>
                <h2 class="section-title">
                    Project Karya <span class="grad">IT FSD</span>
                </h2>
                <p class="section-desc">
                    Berbagai sistem unggulan dan platform digital yang dibangun
                    serta dikembangkan oleh tim IT FSD untuk mengakselerasi
                    operasional bisnis.
                </p>
            </div>

            <!-- Filter Categories -->
            <div class="filters-wrap">
                <button
                    v-for="cat in categories"
                    :key="cat"
                    class="filter-btn"
                    :class="{ active: activeCategory === cat }"
                    @click="activeCategory = cat"
                >
                    {{ cat }}
                </button>
            </div>

            <!-- Projects Grid -->
            <div class="projects-grid">
                <div
                    v-for="p in filteredProjects"
                    :key="p.id"
                    class="project-card card"
                    @click="openProjectModal(p)"
                >
                    <div class="card-top">
                        <div class="project-icon">{{ p.icon }}</div>
                        <span class="badge">{{ p.badge }}</span>
                    </div>

                    <h3>{{ p.name }}</h3>
                    <p class="desc">{{ p.desc }}</p>

                    <div class="card-footer">
                        <div class="stack-list">
                            <span
                                v-for="s in p.stack"
                                :key="s"
                                class="stack-pill"
                                >{{ s }}</span
                            >
                        </div>
                        <div class="action-link">
                            <span>Detail System</span>
                            <span class="arrow">→</span>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Project Detail Modal -->
        <Teleport to="body">
            <Transition name="fade">
                <div
                    v-if="selectedProject"
                    class="modal-overlay"
                    @click.self="closeProjectModal"
                >
                    <div class="modal-card">
                        <button class="modal-close" @click="closeProjectModal">
                            &times;
                        </button>
                        <div class="modal-header">
                            <div class="modal-icon">
                                {{ selectedProject.icon }}
                            </div>
                            <div>
                                <span class="badge">{{
                                    selectedProject.badge
                                }}</span>
                                <h2>{{ selectedProject.name }}</h2>
                            </div>
                        </div>
                        <p class="modal-desc">{{ selectedProject.desc }}</p>

                        <div class="modal-meta">
                            <div class="meta-item">
                                <span class="meta-label">Kategori</span>
                                <span class="meta-val">{{
                                    selectedProject.category
                                }}</span>
                            </div>
                            <div class="meta-item">
                                <span class="meta-label">Status</span>
                                <span class="meta-val status-badge">{{
                                    selectedProject.status
                                }}</span>
                            </div>
                            <div class="meta-item">
                                <span class="meta-label">Keunggulan</span>
                                <span class="meta-val">{{
                                    selectedProject.metrics
                                }}</span>
                            </div>
                        </div>

                        <div class="modal-stack">
                            <h4>Teknologi & Stack Utama</h4>
                            <div class="stack-list">
                                <span
                                    v-for="s in selectedProject.stack"
                                    :key="s"
                                    class="stack-pill large"
                                >
                                    {{ s }}
                                </span>
                            </div>
                        </div>

                        <button class="btn btn-full" @click="closeProjectModal">
                            Tutup Detail
                        </button>
                    </div>
                </div>
            </Transition>
        </Teleport>
    </section>
</template>

<style scoped>
.projects-section {
    padding: 96px 0;
    background: var(--dark);
    border-bottom: 1px solid var(--border);
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
    padding: 10px 22px;
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
    box-shadow: 0 4px 16px rgba(52, 207, 235, 0.35);
}

.projects-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 24px;
}

.project-card {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 28px;
    cursor: pointer;
    position: relative;
    overflow: hidden;
    transition:
        transform 0.3s ease,
        border-color 0.3s ease,
        box-shadow 0.3s ease;
}

.project-card:hover {
    transform: translateY(-8px);
    border-color: var(--primary);
    box-shadow: 0 16px 40px rgba(52, 207, 235, 0.2);
}

.card-top {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 18px;
}

.project-icon {
    width: 52px;
    height: 52px;
    border-radius: 14px;
    background: rgba(52, 207, 235, 0.1);
    border: 1px solid rgba(52, 207, 235, 0.25);
    display: grid;
    place-items: center;
    font-size: 1.6rem;
    transition: transform 0.3s ease;
}

.project-card:hover .project-icon {
    transform: scale(1.1) rotate(4deg);
    background: rgba(52, 207, 235, 0.18);
}

.badge {
    font-size: 0.75rem;
    font-weight: 700;
    color: var(--primary);
    background: rgba(52, 207, 235, 0.12);
    padding: 4px 12px;
    border-radius: 999px;
    border: 1px solid rgba(52, 207, 235, 0.3);
}

.project-card h3 {
    font-size: 1.25rem;
    font-weight: 800;
    color: var(--text);
    margin-bottom: 10px;
}

.desc {
    color: var(--muted);
    font-size: 0.92rem;
    line-height: 1.6;
    margin-bottom: 24px;
    flex: 1;
}

.card-footer {
    display: flex;
    flex-direction: column;
    gap: 16px;
}

.stack-list {
    display: flex;
    flex-wrap: wrap;
    gap: 6px;
}

.stack-pill {
    font-size: 0.72rem;
    font-weight: 600;
    padding: 4px 10px;
    border-radius: 999px;
    background: rgba(255, 255, 255, 0.05);
    border: 1px solid var(--border);
    color: var(--muted);
}

.stack-pill.large {
    font-size: 0.82rem;
    padding: 6px 14px;
    color: var(--primary);
    background: rgba(52, 207, 235, 0.1);
    border-color: rgba(52, 207, 235, 0.25);
}

.action-link {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 0.88rem;
    font-weight: 700;
    color: var(--primary);
    padding-top: 12px;
    border-top: 1px dashed var(--border);
    transition: color 0.2s ease;
}

.arrow {
    transition: transform 0.2s ease;
}

.project-card:hover .arrow {
    transform: translateX(6px);
}

/* Modal Styling */
.modal-overlay {
    position: fixed;
    inset: 0;
    z-index: 9999;
    background: rgba(5, 8, 18, 0.85);
    backdrop-filter: blur(14px);
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 20px;
}

.modal-card {
    width: min(560px, 92%);
    background: var(--dark-soft);
    border: 1px solid var(--border);
    border-radius: 24px;
    padding: 32px;
    position: relative;
    box-shadow:
        0 30px 80px rgba(0, 0, 0, 0.7),
        0 0 40px rgba(52, 207, 235, 0.25);
}

.modal-close {
    position: absolute;
    top: 20px;
    right: 20px;
    background: rgba(255, 255, 255, 0.08);
    border: 1px solid var(--border);
    color: var(--text);
    font-size: 1.6rem;
    width: 36px;
    height: 36px;
    border-radius: 50%;
    cursor: pointer;
    display: grid;
    place-items: center;
    transition: background 0.2s;
}

.modal-close:hover {
    background: rgba(255, 255, 255, 0.2);
}

.modal-header {
    display: flex;
    align-items: center;
    gap: 16px;
    margin-bottom: 18px;
}

.modal-icon {
    width: 60px;
    height: 60px;
    border-radius: 16px;
    background: rgba(52, 207, 235, 0.12);
    border: 1px solid rgba(52, 207, 235, 0.3);
    display: grid;
    place-items: center;
    font-size: 2rem;
}

.modal-header h2 {
    font-size: 1.4rem;
    font-weight: 800;
    margin-top: 4px;
}

.modal-desc {
    color: var(--muted);
    font-size: 0.95rem;
    line-height: 1.6;
    margin-bottom: 24px;
}

.modal-meta {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 12px;
    padding: 16px;
    background: rgba(255, 255, 255, 0.03);
    border: 1px solid var(--border);
    border-radius: 14px;
    margin-bottom: 24px;
}

.meta-item {
    display: flex;
    flex-direction: column;
    gap: 4px;
}

.meta-label {
    font-size: 0.75rem;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 0.5px;
}

.meta-val {
    font-size: 0.88rem;
    font-weight: 700;
    color: var(--text);
}

.status-badge {
    color: #34d399;
}

.modal-stack h4 {
    font-size: 0.92rem;
    margin-bottom: 10px;
    color: var(--text);
}

.btn-full {
    width: 100%;
    margin-top: 24px;
    text-align: center;
}

.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.25s ease;
}
.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}

@media (max-width: 768px) {
    .projects-grid {
        grid-template-columns: 1fr;
    }

    .filters-wrap {
        gap: 8px;
        margin-bottom: 32px;
    }

    .filter-btn {
        padding: 8px 16px;
        font-size: 0.85rem;
    }

    .modal-card {
        padding: 24px 20px;
        border-radius: 20px;
        max-height: 90vh;
        overflow-y: auto;
    }

    .modal-meta {
        grid-template-columns: 1fr 1fr;
    }

    .modal-header h2 {
        font-size: 1.2rem;
    }
}

@media (max-width: 480px) {
    .projects-grid {
        gap: 16px;
    }

    .project-card {
        padding: 20px;
    }

    .modal-meta {
        grid-template-columns: 1fr;
    }

    .modal-overlay {
        padding: 12px;
        align-items: flex-end;
    }

    .modal-card {
        border-radius: 24px 24px 0 0;
        width: 100%;
        max-height: 85vh;
    }
}
</style>
