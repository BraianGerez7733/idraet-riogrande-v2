<template>
  <footer class="site-footer">
    <div class="newsletter">
      <p class="newsletter-text">Dejanos tu mail para recibir novedades</p>
      <form class="newsletter-form" @submit.prevent="subscribe">
        <input
          type="email"
          v-model="email"
          required
          placeholder="Tu email"
          class="newsletter-input"
        />
        <button type="submit" class="newsletter-button">Enviar</button>
      </form>
    </div>
    <div class="footer-columns">
      <div class="column">
        <h4>Medios de pago</h4>
        <ul>
          <li>Mercado Pago</li>
          <li>Visa / MasterCard / Amex</li>
          <li>Naranja / Cabal / Nativa</li>
          <li>RapiPago / Pago Fácil</li>
          <li>Transferencia</li>
        </ul>
      </div>
      <div class="column">
        <h4>Medios de envío</h4>
        <ul>
          <li>Andreani</li>
          <li>Correo Argentino</li>
          <li>Retiro en tienda</li>
        </ul>
      </div>
      <div class="column">
        <h4>Redes sociales</h4>
        <ul class="social-list">
          <li><a href="#" aria-label="Facebook">📘 Facebook</a></li>
          <li><a href="#" aria-label="Instagram">📷 Instagram</a></li>
          <li><a href="#" aria-label="TikTok">🎵 TikTok</a></li>
        </ul>
        <h4>Contacto</h4>
        <ul>
          <li><a href="mailto:idraetrg@gmail.com">idraetrg@gmail.com</a></li>
          <li><a href="#">Botón de arrepentimiento</a></li>
        </ul>
      </div>
    </div>
    <div class="footer-bottom">
      Creado con ❤️ por IDRAET Río Grande | Tierra del Fuego, Argentina
    </div>
  </footer>
</template>

<script setup>
import { ref } from 'vue'

const email = ref('')
function subscribe () {
  // For demonstration we just clear the field
  email.value = ''
  alert('Gracias por suscribirte.')
}
</script>

<style scoped>
.site-footer {
  background-color: var(--secondary-color);
  color: var(--dark-gray);
  margin-top: 2rem;
  border-top: 1px solid var(--light-gray);
}

.newsletter {
  background-color: #000;
  color: #fff;
  padding: 1rem;
  text-align: center;
}

.newsletter-form {
  display: flex;
  justify-content: center;
  margin-top: 0.5rem;
  gap: 0.5rem;
}

.newsletter-input {
  padding: 0.5rem;
  border: none;
  border-radius: 4px;
  min-width: 200px;
}

.newsletter-button {
  background-color: var(--primary-color);
  border: none;
  padding: 0.5rem 1rem;
  color: #fff;
  border-radius: 4px;
  font-weight: 500;
}

.footer-columns {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  padding: 2rem 1rem;
  gap: 1rem;
}

.column h4 {
  margin-bottom: 0.5rem;
  color: var(--text-color);
}

.column ul {
  padding-left: 0;
  line-height: 1.5;
}

.column a {
  color: var(--dark-gray);
}

.social-list li {
  margin-bottom: 0.25rem;
}

.footer-bottom {
  background-color: var(--primary-color);
  color: #fff;
  text-align: center;
  padding: 0.5rem 1rem;
  font-size: 0.9rem;
}
</style>