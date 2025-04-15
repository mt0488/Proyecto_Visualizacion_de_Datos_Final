<script>
  import * as d3 from "d3";
  import { onMount } from "svelte";

onMount(() => {
  const script = document.createElement("script");
  script.src = "https://public.flourish.studio/resources/embed.js";
  script.async = true;
  document.body.appendChild(script);
});

  let paises = [
    { nombre: "Estados Unidos", medallas: 98 },
    { nombre: "China", medallas: 92 },
    { nombre: "Rusia", medallas: 87 },
    { nombre: "Francia", medallas: 77 },
    { nombre: "Reino Unido", medallas: 71 },
    { nombre: "Japón", medallas: 63 },
    { nombre: "Alemania", medallas: 54 },
    { nombre: "Corea del Sur", medallas: 42 },
    { nombre: "Italia", medallas: 33 },
    { nombre: "Brasil", medallas: 24 }
  ];

  const escalaFactor = 4; // Factor de escala para reducir las medallas
  const max = d3.max(paises, d => d.medallas / escalaFactor); // Ajustar el máximo según la escala
  let escalaColumnas = d3.scaleLinear().domain([0, max]).range([0, 500]);
</script>


<main>
  <h1>Juegos Olimpicos</h1>

  <h2>Medallero Paris 2024</h2>

  {#each paises as pais}
    <div class="fila">
      <!-- Mostrar la bandera del país -->
      <div class="etiqueta">
        <img src={`/images/${pais.nombre}.svg`} alt={pais.nombre} class="bandera" />
      </div>
      <div class="medallas" style="width: {escalaColumnas(pais.medallas / escalaFactor)}px">
        {#each Array(Math.floor(pais.medallas / escalaFactor)) as _, i}
          <img src="/images/medalla.svg" alt="medalla" class="medalla" />
        {/each}
      </div>
    </div>
  {/each}

  <section class="historia-section">
    
    <table class="historia-lista tabla-deportes">
      <thead>
        <tr>
          <th>Pais</th>
          <th>Medallas Ganadas</th>
        </tr>
      </thead>
      <tbody>
        <tr><td>Estdos Unidos</td><td>98</td></tr>
        <tr><td>China</td><td>92</td></tr>
        <tr><td>Rusia</td><td>87</td></tr> 
        <tr><td>Francia</td><td>77</td></tr>
        <tr><td>Reino Unido</td><td>71</td></tr>
        <tr><td>Japón</td><td>63</td></tr>
        <tr><td>Alemania</td><td>54</td></tr>
        <tr><td>Corea del Sur</td><td>42</td></tr>
        <tr><td>Italia</td><td>33</td></tr>
        <tr><td>Brasil</td><td>24</td></tr> 
      </tbody>
    </table>
  </section>


  <h2 class="graficos-header">La localía... ¿Ayudó a Francia?</h2>
  <p>Para responder esta pregunta, comparemos la cantidad de medallas entre Francia y Estados Unidos en las anteriores ediciones y luego en la ultima edicion.</p>
  
  
  <section class="graficos-container">
    <!-- Primer gráfico -->
    <div class="flourish-embed flourish-chart" data-src="visualisation/22674075">
      <script src="https://public.flourish.studio/resources/embed.js"></script>
      <noscript>
        <img src="https://public.flourish.studio/visualisation/22674075/thumbnail" width="100%" alt="chart visualization" />
      </noscript>
    </div>
  
    <!-- Segundo gráfico -->
    <div class="flourish-embed flourish-chart" data-src="visualisation/22561745">
      <script src="https://public.flourish.studio/resources/embed.js"></script>
      <noscript>
        <img src="https://public.flourish.studio/visualisation/22561745/thumbnail" width="100%" alt="chart visualization" />
      </noscript>
    </div>
  </section>
  

  

  <footer class="footer">
    <p>© 2025 Juegos Olímpicos - Todos los derechos reservados</p>
    <div class="footer-social">
      <a href="https://facebook.com" target="_blank" class="social-link">Benjamin Sanchez Salas</a>
      <a href="https://twitter.com" target="_blank" class="social-link">Mateo Tejera</a>
    </div>
  </footer>

</main>





<style>


 h1 {
    text-align: center;
    font-family: 'Avenir', sans-serif;
    font-weight: 500;
    color: #000000;
    margin-top: 1rem;
    margin-bottom: 3rem;
  }

 

  :global(body) {
    margin: 0;
    font-family: 'Avenir', sans-serif;
    background-image: url("public/images/Ol.jpg"); /* Ruta de la imagen de fondo */
    background-size: cover; /* Asegura que la imagen cubra toda la pantalla */
    background-position: center; /* Centra la imagen */
    background-repeat: no-repeat; /* Evita que la imagen se repita */
    color: #333;
  }
  
  main {
    position: relative;
    z-index: 1;
    backdrop-filter: blur(4px); /* Difumina el fondo detrás del main */
    background-color: rgba(255, 255, 255, 0.8); /* Fondo blanco con transparencia */
    padding: 2rem;
    border-radius: 12px; /* Bordes redondeados */
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1); /* Sombra para destacar el main */
    max-width: 1200px; /* Ancho máximo del contenido */
    margin: 2rem auto; /* Centra el main horizontalmente */
  }


  h2 {
    font-family: 'Avenir', sans-serif;
    font-weight: 300;
    margin-left: 3rem;
    margin-bottom: 2rem;
    color: #000000;
  }

  .fila {
    display: flex;
    align-items: center;
    margin-bottom: 1.5rem;
  }

  .etiqueta {
    width: 160px;
    margin-right: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .bandera {
    width: 50px; /* Ajusta el tamaño de la bandera */
    height: auto;
  }

  .medallas {
    display: flex;
    flex-wrap: nowrap;
    gap: 1px;
    align-items: center;
  }

  .medalla {
    width: 36px; /* Doble del tamaño original */
    height: 36px; /* Doble del tamaño original */
  }


.tabla-deportes {
    width: 100%;
    border-collapse: separate; /* Cambiar a 'separate' para permitir bordes redondeados */
    border-spacing: 0; /* Eliminar espacios entre celdas */
    font-size: 1.1rem;
    background-color: rgba(255, 255, 255, 0.9); /* Fondo blanco con transparencia */
    border-radius: 12px; /* Bordes redondeados solo en los extremos */
    overflow: hidden; /* Asegura que el contenido no sobresalga de los bordes redondeados */
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1); /* Sombra para destacar la tabla */
  }

  .tabla-deportes thead {
    background-color: #003366; /* Color azul oscuro para encajar con la estética */
    color: white;
  }

  .tabla-deportes th,
  .tabla-deportes td {
    padding: 12px 20px;
    text-align: left;
    border-bottom: 1px solid #ddd;
  }

  .tabla-deportes tbody tr:last-child td {
    border-bottom: none; /* Eliminar el borde inferior de la última fila */;
  }

  .graficos-header {
    margin-top: 5rem;
    font-family: 'Avenir', sans-serif;
    font-weight: 300;
    margin-left: 0;
    margin-bottom: 0;
    color: #000000;
  }

  .graficos-container {
    display: flex;
    justify-content: space-between; /* Espacio entre los gráficos */
    align-items: flex-start; /* Alinear los gráficos al inicio verticalmente */
    gap: 2rem; /* Espaciado entre los gráficos */
    margin-top: 2rem;
    flex-wrap: wrap; /* Permite que los gráficos se ajusten en filas si no hay espacio horizontal */
  }

  .flourish-embed {
    flex: 1; /* Permite que los gráficos se ajusten al espacio disponible */
    max-width: 48%; /* Limita el ancho de cada gráfico */
    height: 400px; /* Altura fija para ambos gráficos */
    box-sizing: border-box; /* Asegura que el padding y el borde no afecten el tamaño */
    overflow: hidden; /* Oculta cualquier contenido que exceda los límites del contenedor */
  }

  .flourish-embed iframe {
    width: 100% !important; /* Asegura que el gráfico ocupe todo el ancho del contenedor */
    height: 100% !important; /* Asegura que el gráfico ocupe toda la altura del contenedor */
    max-width: 100%; /* Evita que el iframe exceda el ancho del contenedor */
    max-height: 100%; /* Evita que el iframe exceda la altura del contenedor */
  }

  
  .footer {
    background-color: #003366; /* Azul oscuro */
    color: white; /* Texto blanco */
    text-align: center; /* Centrar el texto */
    padding: 1rem; /* Espaciado interno */
    margin-top: 3rem; /* Aumenta la separación del contenido anterior */
    font-family: 'Avenir', sans-serif; /* Fuente consistente */
    font-size: 0.9rem; /* Tamaño de fuente */
    border-radius: 0 0 12px 12px; /* Bordes redondeados en la parte inferior */
    clear: both; /* Asegura que el footer no sea afectado por elementos flotantes */
  }


  .footer-social {
    margin-top: 1rem;
  }

  .social-link {
    color: white;
    text-decoration: none;
    margin: 0 0.5rem;
    font-size: 0.9rem;
  }

  .social-link:hover {
    text-decoration: underline;
  }


</style>