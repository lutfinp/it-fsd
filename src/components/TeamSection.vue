<script setup>
const manager = {
  name: 'Efendi',
  role: 'Manager IT FSD',
  grad: 'linear-gradient(135deg, #34cfeb, #00f2fe)',
}

const supervisors = [
  { name: 'Erland', role: 'Supervisor', grad: 'linear-gradient(135deg, #34cfeb, #38bdf8)' },
]

const staff = [
  { name: 'Lutfi', role: 'Frontend Developer', grad: 'linear-gradient(135deg, #34cfeb, #00e5ff)' },
  { name: 'Andrianata', role: 'Mobile Developer', grad: 'linear-gradient(135deg, #ec4899, #34cfeb)' },
  { name: 'Rofi', role: 'Backend Developer', grad: 'linear-gradient(135deg, #10b981, #34cfeb)' },
  { name: 'Atha', role: 'Backend Developer', grad: 'linear-gradient(135deg, #f59e0b, #34cfeb)' },
  { name: 'Haikal', role: 'Backend Developer', grad: 'linear-gradient(135deg, #38bdf8, #ec4899)' },
  { name: 'Ian', role: 'Backend Developer', grad: 'linear-gradient(135deg, #34cfeb, #ec4899)' },
  { name: 'Millata', role: 'Backend Developer', grad: 'linear-gradient(135deg, #ef4444, #34cfeb)' },
]

const initials = (name) =>
  name
    .split(' ')
    .map((n) => n[0])
    .join('')
</script>

<template>
  <section id="tim" class="team">
    <div class="container team-container">
      <div class="text-center">
        <span class="eyebrow">Struktur Tim</span>
        <h2 class="section-title">Hierarki Departemen IT FSD</h2>
        <p class="section-desc">
          Satu arah, satu visi. Dari manager hingga staff, setiap level punya peran
          penting untuk menjaga IT FSD tetap menjadi yang terbaik.
        </p>
      </div>

      <div class="hierarchy mt-12">
        <!-- Level 1: Manager -->
        <span class="level-label">1 Manager</span>

        <div class="manager-node">
          <div class="manager-card card">
            <div class="avatar" :style="{ background: manager.grad }">{{ initials(manager.name) }}</div>
            <h3>{{ manager.name }}</h3>
            <p class="role">{{ manager.role }}</p>
          </div>
        </div>

        <!-- Connector -->
        <div class="connector">
          <span class="connector-pill">1 Supervisor</span>
        </div>

        <!-- Level 2: Supervisors -->
        <div class="level-wrapper">
          <div class="level single-node">
            <div v-for="s in supervisors" :key="s.name" class="node">
              <div class="node-card card">
                <div class="avatar sm" :style="{ background: s.grad }">{{ initials(s.name) }}</div>
                <h4>{{ s.name }}</h4>
                <p class="role">{{ s.role }}</p>
              </div>
            </div>
          </div>
        </div>

        <!-- Connector -->
        <div class="connector">
          <span class="connector-pill">7 Staff</span>
        </div>

        <!-- Level 3: Staff -->
        <div class="level-wrapper">
          <div class="level staff-level">
            <div v-for="s in staff" :key="s.name" class="node">
              <div class="node-card card">
                <div class="avatar sm" :style="{ background: s.grad }">{{ initials(s.name) }}</div>
                <h4>{{ s.name }}</h4>
                <p class="role">{{ s.role }}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.team {
  background: var(--dark-soft);
  border-block: 1px solid var(--border);
}

.team-container {
  width: min(1340px, 96%);
}

.hierarchy {
  display: flex;
  flex-direction: column;
  align-items: center;
}

/* ---- Level labels (Manager / Supervisor / Staff) ---- */
.level-label {
  font-size: 0.78rem;
  font-weight: 700;
  letter-spacing: 1.5px;
  text-transform: uppercase;
  color: var(--muted);
  border: 1px solid var(--border);
  background: rgba(52, 207, 235, 0.08);
  padding: 6px 16px;
  border-radius: 999px;
  margin-bottom: 24px;
}

/* ---- Manager card ---- */
.manager-node {
  width: 100%;
  margin-bottom: 0;
}

.manager-card {
  width: 260px;
  margin-inline: auto;
  text-align: center;
  padding: 32px 24px;
  border-color: rgba(52, 207, 235, 0.5);
  box-shadow: 0 20px 60px rgba(52, 207, 235, 0.25);
}

.avatar {
  width: 76px;
  height: 76px;
  margin: 0 auto 14px;
  border-radius: 50%;
  display: grid;
  place-items: center;
  font-size: 1.4rem;
  font-weight: 800;
  color: #0b1020;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.3);
}

.avatar.sm {
  width: 52px;
  height: 52px;
  font-size: 1rem;
  margin: 0 auto 10px;
}

.manager-card h3 {
  font-size: 1.25rem;
  margin-bottom: 4px;
}

.role {
  color: var(--muted);
  font-size: 0.85rem;
  margin-bottom: 0;
}

/* ---- Connector between levels ---- */
.connector {
  position: relative;
  width: 2px;
  height: 64px;
  background: linear-gradient(
    to bottom,
    rgba(52, 207, 235, 0.9),
    rgba(0, 242, 254, 0.9)
  );
}

.connector-pill {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: var(--dark);
  border: 1px solid var(--border);
  padding: 5px 16px;
  border-radius: 999px;
  font-size: 0.8rem;
  font-weight: 700;
  color: var(--text);
  white-space: nowrap;
  z-index: 1;
}

/* ---- Level row wrapper ---- */
.level-wrapper {
  width: 100%;
}

.level {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 16px;
  width: 100%;
  position: relative;
  padding-top: 48px;
  padding-bottom: 6px;
}

/* horizontal backbone line */
.staff-level::before {
  content: '';
  position: absolute;
  top: 0;
  left: 80px;
  right: 80px;
  height: 2px;
  background: linear-gradient(90deg, rgba(52, 207, 235, 0.9), rgba(0, 242, 254, 0.9));
}

.single-node::before {
  display: none;
}

.node {
  position: relative;
  flex: 0 1 156px;
  width: 156px;
}

/* vertical stem from backbone to card */
.node::before {
  content: '';
  position: absolute;
  top: -48px;
  left: 50%;
  width: 2px;
  height: 48px;
  background: rgba(52, 207, 235, 0.8);
  transform: translateX(-50%);
}

.node-card {
  text-align: center;
  padding: 22px 12px;
}

.node-card h4 {
  font-size: 0.95rem;
  margin-bottom: 4px;
}

.node-card .role {
  font-size: 0.78rem;
  margin-bottom: 0;
  min-height: 2.2em;
}

@media (max-width: 1024px) {
  .staff-level::before {
    display: none;
  }
  .node::before {
    display: none;
  }
  .node {
    flex: 1 1 150px;
    max-width: 200px;
  }
}

@media (max-width: 600px) {
  .manager-card {
    width: 220px;
  }
  .node {
    flex: 1 1 140px;
  }
}
</style>