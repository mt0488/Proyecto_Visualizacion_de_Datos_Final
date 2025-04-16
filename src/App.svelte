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

  const escalaFactor = 4;
  const max = d3.max(paises, d => d.medallas / escalaFactor);
  let escalaColumnas = d3.scaleLinear().domain([0, max]).range([0, 500]);
</script>

<main>
  <div class="header-container">
    <img src="/images/logo.png" alt="Logo JJOO" class="logo-jjoo" />
    <h1>Juegos Olimpicos: Paris 2024</h1>
    <img src="/images/paris.png" alt="Logo París 2024" class="logo-paris" />
  </div>

  <p class="intro">Los Juegos Olímpicos de París 2024 marcaron un hito al reunir a más de 10.000 atletas de 204 países en 32 disciplinas
     deportivas, celebradas en escenarios emblemáticos de la capital francesa. Durante 16 días de intensa competencia, se
      vivieron momentos inolvidables que destacaron el espíritu deportivo y la excelencia atlética. A continuacion un breve
    video con lo que fue lo mejor de Paris 2024...</p>


    <div class="video-container">
      <iframe 
        width="1000" 
        height="562" 
        src="https://www.youtube.com/embed/vy6FivZHRjQ" 
        title="YouTube video player" 
        frameborder="0" 
        allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" 
        allowfullscreen>
      </iframe>
    </div>

  

  <h2>Medallero Olimpico</h2>

  {#each paises as pais}
    <div class="fila">
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
  <p>Competir como país anfitrión suele ser una ventaja significativa para los atletas,
     ya que la familiaridad con el entorno, el apoyo del público local y la reducción del 
     estrés logístico pueden mejorar su rendimiento. Sin embargo, esta localía también puede 
     transformarse en una fuente de presión adicional, ya que las expectativas de la nación
     están puestas sobre ellos, lo que puede afectar tanto positiva como negativamente su
     desempeño.¿Fue esto un impulso o una carga para los atletas franceses en París 2024?
     Para responder esta pregunta, vamos a retroceder en el tiempo y analizar
     cómo se ha comportado Francia en comparación con una potencia histórica como Estados Unidos,
     contrastando sus resultados en esta edición con los de los Juegos anteriores.</p>
  
  <section class="graficos-container">
    <div class="flourish-embed flourish-chart" data-src="visualisation/22674075">
      <script src="https://public.flourish.studio/resources/embed.js"></script>
      <noscript>
        <img src="https://public.flourish.studio/visualisation/22674075/thumbnail" width="100%" alt="chart visualization" />
      </noscript>
    </div>
  
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
      <a href="https://www.linkedin.com/in/benja-sanchez-salas-4a8769360/" target="_blank" class="social-link">Benjamin Sanchez Salas</a>
      <a href="http://www.linkedin.com/in/mateo-tejera-089b89270" target="_blank" class="social-link">Mateo Tejera</a>
    </div>
  </footer>
</main>

<style>
  .header-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 3rem; 
  }

  .header-container h1 {
    flex: 1; 
    text-align: center;
    font-family: 'Avenir', sans-serif;
    font-weight: 500;
    color: #000000;
    margin: 0;
  }

  .logo-jjoo,
  .logo-paris {
    width: 100px; 
    height: auto;
  }

  .intro {
    font-family: "Avenir", sans-serif;
    font-weight: 200;
    text-align: justify;
  }

  .video-container {
    display: flex;
    justify-content: center;
    margin-top: 2rem;
    margin-bottom: 7rem;
    
  }

  .video-container iframe {
    width: 100%; 
    max-width: 1000px; 
    height: 562px; 
    border-radius: 12px; 
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1); 
  }

  :global(body) {
    margin: 0;
    font-family: 'Avenir', sans-serif;
    background-image: url("public/images/Ol.jpg");
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    color: #333;
  }
  
  main {
    position: relative;
    z-index: 1;
    backdrop-filter: blur(4px);
    background-color: rgba(255, 255, 255, 0.8);
    padding: 2rem;
    border-radius: 12px;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    max-width: 1200px;
    margin: 2rem auto;
  }

  h2 {
    font-family: 'Avenir', sans-serif;
    font-weight: 300;
    margin-left: 0;
    margin-bottom: 2rem;
    color: #000000;
  }

  .fila {
    display: flex;
    align-items: center;
    margin-bottom: 1.5rem;
    width: 100%; 
    padding: 0; 
    margin-left: 0;
    margin-right: 0; 
  }

  .etiqueta {
    width: 160px;
    margin-right: 10px;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 0;
  }

  .bandera {
    width: 50px;
    height: auto;
  }

  .medallas {
    display: flex;
    flex-wrap: nowrap;
    gap: 1px;
    align-items: center;
    padding: 0;
    margin: 0;
  }

  .medalla {
    width: 36px;
    height: 36px;
  }

  .tabla-deportes {
    margin-top: 7rem;
    width: 100%;
    border-collapse: separate;
    border-spacing: 0;
    font-size: 1.1rem;
    background-color: rgba(255, 255, 255, 0.9);
    border-radius: 12px;
    overflow: hidden;
    box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
    margin-bottom: 7rem;
  }

  .tabla-deportes thead {
    background-color: #003366;
    color: white;
  }

  .tabla-deportes th,
  .tabla-deportes td {
    padding: 12px 20px;
    text-align: left;
    border-bottom: 1px solid #ddd;
  }

  .tabla-deportes tbody tr:last-child td {
    border-bottom: none;
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
    justify-content: space-between;
    align-items: flex-start;
    gap: 2rem;
    margin-top: 2rem;
    flex-wrap: wrap;
  }

  .flourish-embed {
    flex: 1;
    max-width: 48%;
    height: 600px;
    box-sizing: border-box;
    overflow: hidden;
  }


  .footer {
    background-color: #003366;
    color: white;
    text-align: center;
    padding: 1rem;
    margin-top: 3rem;
    font-family: 'Avenir', sans-serif;
    font-size: 0.9rem;
    border-radius: 0 0 12px 12px;
    clear: both;
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