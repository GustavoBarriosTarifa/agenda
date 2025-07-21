<template>
  <section class="hero">
    <div class="container">
      <h2>Administrar Agenda de Contactos</h2>      
      <a href="/contactos" class="btn">Ver Contactos</a>
    </div>
  </section>

  
  <section id="beneficios" class="beneficios">
    <div class="container">
      <h3>¿Por qué elegirnos?</h3>
      <ul>
        <li>✔️ Informacion correcta de los contactos</li>
        <li>✔️ disponibilidad de infomracion verifica</li>
        <li>✔️ acceso rapido</li>        
      </ul>
    </div>
  </section>
  
</template>

<script>
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'HomeView',
  components: {
    HelloWorld
  }
}
</script>


<style>

.hero {
  background: #eee;
  text-align: center;
  padding: 4rem 1rem;
}

.hero h2 {
  font-size: 2rem;
  margin-bottom: 1rem;
}

.hero .btn {
  display: inline-block;
  background: #000;
  color: #fff;
  padding: 0.8rem 1.5rem;
  text-decoration: none;
  margin-top: 1rem;
  border-radius: 5px;
}



/* Beneficios */
.beneficios ul {
  list-style: none;
  padding: 1rem 0;
}

.beneficios li {
  margin-bottom: 0.5rem;
}

/* Testimonios */
.testimonios blockquote {
  background: #f9f9f9;
  padding: 1rem;
  margin: 1rem 0;
  border-left: 5px solid #ccc;
}

/* Footer */
footer {
  background: #f0f0f0;
  text-align: center;
  padding: 2rem 1rem;
  font-size: 0.9rem;
}

/* ====== RESPONSIVE ====== */
@media (max-width: 768px) {

  .hero h2 {
    font-size: 1.5rem;
  }

  .autos .grid {
    flex-direction: column;
  }

  .card {
    flex: 1 1 100%;
  }

  .beneficios ul {
    padding-left: 1rem;
  }

  .testimonios blockquote {
    font-size: 0.95rem;
  }
}
</style>