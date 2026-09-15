<script setup>
import { ref } from 'vue'

const email = ref('')

function onSubmit() {
  if (email.value.trim()) {
    window.location.href = `mailto:fsd-jobs@gnet.com?subject=Minat Bergabung IT FSD&body=Halo IT FSD, aku ingin bergabung! Email: ${email.value}`
  }
}
</script>

<!-- <template>
  <section id="join" class="cta">
    <div class="container">
      <div class="cta-box">
        <span class="eyebrow">Bergabunglah</span>
        <h2>
          Ingin Jadi Bagian dari
          <span class="grad">Departemen Terbaik?</span>
        </h2>
        <p>
          Kirim emaillmu dan siapa tahu, langkah selanjutnya adalah kamu yang
          menulis kisah sukses di IT FSD berikutnya.
        </p>

        <form class="cta-form" @submit.prevent="onSubmit">
          <input v-model="email" type="email" placeholder="email@kamu.com" required />
          <button type="submit" class="btn">Saya Siap! 🚀</button>
        </form>
      </div>
    </div>
  </section>
</template> -->

<style scoped>
.cta {
  padding-bottom: 120px;
}

.cta-box {
  text-align: center;
  padding: 72px 40px;
  border-radius: 24px;
  background:
    radial-gradient(500px 240px at 20% 0%, rgba(52, 207, 235, 0.22), transparent 60%),
    radial-gradient(500px 240px at 80% 100%, rgba(0, 242, 254, 0.18), transparent 60%),
    var(--dark-soft);
  border: 1px solid var(--border);
}

.cta-box h2 {
  font-size: clamp(1.8rem, 4vw, 2.6rem);
  font-weight: 800;
  margin-bottom: 16px;
}

.cta-box p {
  color: var(--muted);
  max-width: 520px;
  margin: 0 auto 32px;
}

.cta-form {
  display: flex;
  gap: 12px;
  justify-content: center;
  flex-wrap: wrap;
}

.cta-form input {
  flex: 1;
  min-width: 260px;
  max-width: 420px;
  padding: 14px 22px;
  border-radius: 999px;
  border: 1px solid var(--border);
  background: rgba(255, 255, 255, 0.04);
  color: var(--text);
  font-size: 0.95rem;
  outline: none;
  transition: border-color 0.2s, box-shadow 0.2s;
}

.cta-form input:focus {
  border-color: var(--primary);
  box-shadow: 0 0 16px rgba(52, 207, 235, 0.25);
}

.cta-form input::placeholder {
  color: var(--muted);
}
</style>