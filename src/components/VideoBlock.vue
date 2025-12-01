<template>
  <section class="video-block">
    <h3>Cómo usar nuestros productos</h3>
    <div class="video-container">
      <iframe
        src="https://www.youtube.com/embed/s2N7cbIswdA"
        title="Cómo usar nuestros productos"
        frameborder="0"
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
        allowfullscreen
      ></iframe>
    </div>
  </section>
</template>

<script setup>
// No logic needed
</script>

<style scoped>
.video-block {
  margin-top: 3rem;
}

.video-block h3 {
  margin-bottom: 1rem;
  color: var(--text-color);
  font-size: 1.3rem;
}

.video-container {
  position: relative;
  width: 100%;
  max-width: 800px;
  margin: 0 auto;
  padding-bottom: 40%;
  overflow: hidden;
  border-radius: 8px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.08);
}

.video-container iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  border: none;
}
</style>