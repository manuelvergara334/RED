<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>Evaluación de RED | Portafolio de Modelos</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,300;14..32,400;14..32,500;14..32,600;14..32,700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Inter', sans-serif; background: #f8f9fc; color: #1e2a3e; line-height: 1.5; }
        
        .navbar { background: linear-gradient(135deg, #2c3e66 0%, #4a3b6e 100%); color: white; padding: 1rem 2rem; position: sticky; top: 0; z-index: 1000; box-shadow: 0 4px 20px rgba(0,0,0,0.1); }
        .nav-container { max-width: 1400px; margin: 0 auto; display: flex; justify-content: space-between; align-items: center; flex-wrap: wrap; }
        .logo h1 { font-size: 1.3rem; font-weight: 600; }
        .logo p { font-size: 0.75rem; opacity: 0.85; }
        .nav-links { display: flex; gap: 0.5rem; flex-wrap: wrap; align-items: center; }
        .nav-link { color: white; text-decoration: none; font-weight: 500; padding: 0.5rem 1rem; border-radius: 30px; transition: all 0.3s ease; cursor: pointer; background: none; border: none; font-size: 0.95rem; display: inline-block; }
        .nav-link:hover { background: rgba(255,255,255,0.25); transform: translateY(-2px); }
        .dropdown { position: relative; display: inline-block; }
        .dropdown-content { display: none; position: absolute; background: white; min-width: 260px; box-shadow: 0 12px 25px rgba(0,0,0,0.2); border-radius: 16px; z-index: 1001; top: 45px; left: 0; color: #1e2a3e; overflow: hidden; border: 1px solid #e0d6f0; }
        .dropdown-content a { color: #2c3e66; padding: 12px 20px; text-decoration: none; display: block; font-weight: 500; transition: background 0.2s; cursor: pointer; }
        .dropdown-content a:hover { background: #f0e9fc; padding-left: 28px; }
        .dropdown:hover .dropdown-content { display: block; }
        
        .page { display: none; max-width: 1400px; margin: 2rem auto; padding: 2rem; background: white; border-radius: 32px; box-shadow: 0 10px 30px rgba(0,0,0,0.05); animation: fadeIn 0.3s ease; }
        .active-page { display: block; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(10px);} to { opacity: 1; transform: translateY(0);} }
        
        h2 { font-size: 1.8rem; margin-bottom: 1.5rem; border-left: 5px solid #e67e22; padding-left: 1rem; color: #2c3e66; }
        h3 { margin: 1.2rem 0 0.8rem; color: #4a3b6e; font-size: 1.3rem; }
        
        .card-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(340px, 1fr)); gap: 1.5rem; margin: 1.5rem 0; }
        .card { background: #ffffff; border-radius: 20px; padding: 1.5rem; box-shadow: 0 5px 15px rgba(0,0,0,0.05); transition: transform 0.2s, box-shadow 0.2s; border: 1px solid #e0d6f0; }
        .card:hover { transform: translateY(-3px); box-shadow: 0 15px 25px -10px rgba(0,0,0,0.1); border-color: #e67e22; }
        .badge { background: #f0e9fc; color: #4a3b6e; padding: 0.2rem 0.8rem; border-radius: 50px; font-size: 0.75rem; font-weight: 600; display: inline-block; margin-bottom: 0.8rem; }
        .btn-download { background: #e67e22; color: white; border: none; padding: 0.5rem 1rem; border-radius: 40px; font-weight: 500; cursor: pointer; font-size: 0.85rem; margin-top: 1rem; display: inline-flex; align-items: center; gap: 0.5rem; transition: 0.2s; }
        .btn-download:hover { background: #d35400; transform: scale(1.02); }
        
        .table-responsive { overflow-x: auto; margin: 1.5rem 0; }
        table { width: 100%; border-collapse: collapse; font-size: 0.9rem; min-width: 600px; }
        th, td { border: 1px solid #e0d6f0; padding: 12px 14px; text-align: left; vertical-align: top; }
        th { background: #f0e9fc; font-weight: 600; color: #2c3e66; }
        .score-high { background: #d4edda; font-weight: bold; text-align: center; }
        .score-mid { background: #fff3cd; text-align: center; }
        .score-low { background: #f8d7da; text-align: center; }
        
        footer { text-align: center; padding: 2rem; color: #5b6e8c; font-size: 0.85rem; border-top: 1px solid #e0d6f0; margin-top: 2rem; background: rgba(255,255,255,0.7); }
        @media (max-width: 768px) { .nav-container { flex-direction: column; gap: 0.8rem; } .nav-links { justify-content: center; } .page { padding: 1.2rem; } .card-grid { grid-template-columns: 1fr; } }
        .instrument-box { background: #fef9f0; border-left: 4px solid #e67e22; padding: 1rem; margin: 1rem 0; border-radius: 12px; }
        .model-card { margin-bottom: 2rem; border-bottom: 2px solid #e0d6f0; padding-bottom: 1.5rem; }
        .model-card:last-child { border-bottom: none; }
        .video-container { background: linear-gradient(135deg, #2c3e66 0%, #4a3b6e 100%); border-radius: 24px; padding: 1.5rem; margin-top: 2rem; text-align: center; color: white; }
        .video-container h3 { color: white; margin-top: 0; margin-bottom: 0.5rem; }
        .video-container p { margin-bottom: 1rem; font-size: 0.95rem; opacity: 0.9; }
        .video-wrapper { position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 16px; }
        .video-wrapper iframe { position: absolute; top: 0; left: 0; width: 100%; height: 100%; border-radius: 16px; }
        ul, ol { margin-left: 1.5rem; }
        .response-box { background: #f0f4ff; border-radius: 16px; padding: 1.5rem; margin: 1.5rem 0; }
    </style>
</head>
<body>

<div class="navbar">
    <div class="nav-container">
        <div class="logo">
            <h1><i class="fas fa-graduation-cap"></i> Evaluación de RED</h1>
            <p>Marlon David Vergara Lozano | Prof. Eduardo Méndez Bonilla | UDES</p>
        </div>
        <div class="nav-links">
            <button class="nav-link" data-page="inicio"><i class="fas fa-home"></i> Inicio</button>
            <div class="dropdown">
                <button class="nav-link" data-page="modelos-completos"><i class="fas fa-layer-group"></i> Modelos y RED ▼</button>
                <div class="dropdown-content">
                    <a href="#" data-page="seleccion-modelos"><i class="fas fa-check-double"></i> Seleccionar modelo</a>
                    <a href="#" data-page="recursos-red"><i class="fas fa-database"></i> Recursos educativos digitales</a>
                </div>
            </div>
            <button class="nav-link" data-page="rediseno"><i class="fas fa-pencil-ruler"></i> Rediseño</button>
            <button class="nav-link" data-page="aplicacion"><i class="fas fa-clipboard-list"></i> Aplicación</button>
            <button class="nav-link" data-page="referencias"><i class="fas fa-book"></i> Referencias</button>
        </div>
    </div>
</div>

<!-- INICIO -->
<div id="inicio" class="page active-page">
    <h2><i class="fas fa-chalkboard-user"></i> Portafolio de evaluación de Recursos Educativos Digitales</h2>
    <p style="font-size: 1.1rem; margin-bottom: 1rem;"><strong>Autor:</strong> Marlon David Vergara Lozano | <strong>Profesor:</strong> Eduardo Méndez Bonilla</p>
    <p><strong>Universidad de Santander (UDES)</strong></p>
    <div class="card-grid" style="margin-top: 2rem;">
        <div class="card"><i class="fas fa-chart-line" style="font-size: 2rem; color:#e67e22;"></i><h3>6 modelos analizados</h3><p>Revisión de modelos de evaluación: COdA, LORI, EVALUAREED, Marzal, Reeves, Nokelainen.</p></div>
        <div class="card"><i class="fas fa-file-alt" style="font-size: 2rem; color:#e67e22;"></i><h3>3 modelos aplicados</h3><p>Selección de COdA, LORI y EVALUAREED con instrumentos y aplicación a dos RED.</p></div>
        <div class="card"><i class="fas fa-robot" style="font-size: 2rem; color:#e67e22;"></i><h3>Modelo rediseñado</h3><p>Modelo Integral de Evaluación de RED (MIERED) adaptado al contexto universitario y escolar.</p></div>
    </div>
</div>

<!-- 6 MODELOS COMPLETOS -->
<div id="modelos-completos" class="page">
    <h2>📊 6 Modelos de evaluación de RED</h2>
    <div class="card-grid">
        <div class="card"><div class="badge">Modelo 1</div><h3>COdA</h3><p><strong>Descripción:</strong> Herramienta UCM con 10 criterios (5 didácticos + 5 técnicos). Escala 1-5.<br><strong>Criterios:</strong> Objetivos, calidad contenidos, reflexión, interactividad, motivación, formato, usabilidad, accesibilidad, reusabilidad, interoperabilidad.<br><strong>Escala:</strong> 1=mínimo, 5=máximo<br><strong>Metodología:</strong> Autoevaluación o pares con guía detallada.</p></div>
        <div class="card"><div class="badge">Modelo 2</div><h3>LORI</h3><p><strong>Descripción:</strong> Learning Object Review Instrument. 9 criterios pedagógico-técnicos.<br><strong>Criterios:</strong> Calidad contenido, adecuación objetivos, feedback, motivación, diseño, usabilidad, accesibilidad, reusabilidad, estándares.<br><strong>Escala:</strong> 1 a 5<br><strong>Metodología:</strong> Revisión colaborativa por pares.</p></div>
        <div class="card"><div class="badge">Modelo 3</div><h3>EVALUAREED</h3><p><strong>Descripción:</strong> Proyecto español con juicio experto + sonda automática. Checklist 9 dimensiones.<br><strong>Criterios:</strong> Contenido, objetivos, feedback, usabilidad, motivación, accesibilidad, requisitos técnicos, propiedad intelectual, efectividad.</p></div>
        <div class="card"><div class="badge">Modelo 4</div><h3>Marzal, Calzada & Vianello</h3><p><strong>Descripción:</strong> Enfoque en usabilidad alfabetizadora. Tres categorías: Captación, Fidelización, Capacidad alfabetizadora con 23 indicadores.</p></div>
        <div class="card"><div class="badge">Modelo 5</div><h3>Reeves (Pedagógico)</h3><p><strong>Descripción:</strong> 14 dimensiones bipolares (constructivismo vs objetivismo). Análisis cualitativo del diseño instruccional.</p></div>
        <div class="card"><div class="badge">Modelo 6</div><h3>Nokelainen</h3><p><strong>Descripción:</strong> Usabilidad pedagógica con 10 dimensiones y 56 subdimensiones. Base de eValuator.</p></div>
    </div>
</div>

<!-- SELECCIONAR MODELO: 3 MODELOS CON INSTRUMENTOS + VIDEO -->
<div id="seleccion-modelos" class="page">
    <h2>🎯 3 Modelos seleccionados con sus instrumentos de evaluación</h2>
    
    <div class="model-card">
        <div class="badge" style="background:#4a3b6e; color:white;">Modelo 1</div>
        <h3><i class="fas fa-file-alt"></i> COdA (Calidad de Objetos de Aprendizaje)</h3>
        <p><strong>Descripción:</strong> Herramienta desarrollada por la Universidad Complutense de Madrid que evalúa la calidad de los OA mediante 10 criterios (5 didácticos y 5 técnicos). Cada criterio se puntúa de 1 a 5 con una guía detallada de buenas prácticas.</p>
        <p><strong>Criterios:</strong> 1. Objetivos, 2. Calidad contenidos, 3. Reflexión, 4. Interactividad, 5. Motivación, 6. Formato, 7. Usabilidad, 8. Accesibilidad, 9. Reusabilidad, 10. Interoperabilidad</p>
        <div class="instrument-box">
            <strong><i class="fas fa-clipboard-list"></i> Instrumento COdA:</strong> Plantilla con escala 1-5 para cada criterio con subcriterios detallados.
        </div>
        <button class="btn-download" onclick="descargarInstrumento('COdA')"><i class="fas fa-download"></i> Descargar instrumento COdA</button>
    </div>

    <div class="model-card">
        <div class="badge" style="background:#4a3b6e; color:white;">Modelo 2</div>
        <h3><i class="fas fa-file-alt"></i> LORI (Learning Object Review Instrument)</h3>
        <p><strong>Descripción:</strong> Instrumento para revisión colaborativa de objetos de aprendizaje. Evalúa 9 dimensiones clave combinando aspectos pedagógicos y técnicos.</p>
        <p><strong>Criterios:</strong> 1. Calidad contenido, 2. Adecuación objetivos, 3. Feedback, 4. Motivación, 5. Diseño, 6. Usabilidad, 7. Accesibilidad, 8. Reusabilidad, 9. Estándares</p>
        <div class="instrument-box">
            <strong><i class="fas fa-clipboard-list"></i> Instrumento LORI:</strong> Formulario con escala 1-5 + espacio para comentarios cualitativos.
        </div>
        <button class="btn-download" onclick="descargarInstrumento('LORI')"><i class="fas fa-download"></i> Descargar instrumento LORI</button>
    </div>

    <div class="model-card">
        <div class="badge" style="background:#4a3b6e; color:white;">Modelo 3</div>
        <h3><i class="fas fa-file-alt"></i> EVALUAREED</h3>
        <p><strong>Descripción:</strong> Proyecto español que combina juicio de experto con sonda automática. Checklist con 9 dimensiones y 44 indicadores.</p>
        <p><strong>Dimensiones:</strong> 1. Contenido, 2. Objetivos, 3. Feedback, 4. Usabilidad, 5. Motivación, 6. Accesibilidad, 7. Requerimientos técnicos, 8. Propiedad intelectual, 9. Efectividad</p>
        <div class="instrument-box">
            <strong><i class="fas fa-clipboard-list"></i> Instrumento EVALUAREED:</strong> Checklist con 44 indicadores ponderados que genera informe cualitativo y cuantitativo.
        </div>
        <button class="btn-download" onclick="descargarInstrumento('EVALUAREED')"><i class="fas fa-download"></i> Descargar instrumento EVALUAREED</button>
    </div>

    <!-- VIDEO EXPLICATIVO -->
    <div class="video-container">
        <h3><i class="fas fa-video"></i> Video: Análisis de modelos de evaluación de RED</h3>
        <p>En este video se presentan las ventajas y desventajas de los tres modelos seleccionados (COdA, LORI y EVALUAREED), así como la justificación del modelo adaptado para el contexto educativo.</p>
        <div class="video-wrapper">
            <iframe src="https://www.youtube.com/embed/Pki2Ub4G3ng" title="Evaluación de RED - Ventajas y Desventajas de Modelos" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
        </div>
        <p style="margin-top: 0.8rem; font-size: 0.85rem;"><i class="fas fa-clock"></i> Duración: 2 minutos 30 segundos | <i class="fas fa-chalkboard-teacher"></i> Marlon David Vergara Lozano</p>
    </div>
</div>

<!-- RECURSOS EDUCATIVOS DIGITALES -->
<div id="recursos-red" class="page">
    <h2>📚 Recursos Educativos Digitales seleccionados</h2>
    <div class="card-grid">
        <div class="card">
            <div class="badge"><i class="fas fa-code"></i> RED 1</div>
            <h3>Aprendiendo a programar con Scratch</h3>
            <p><strong>Autor:</strong> África Gonzalo Castanedo<br><strong>Nivel:</strong> 1º de ESO | <strong>Área:</strong> Computación y Robótica<br><strong>Repositorio:</strong> Procomún (INTEF)<br><strong>URL:</strong> <a href="https://procomun.intef.es/ode/view/es_2024112212_9190933" target="_blank">https://procomun.intef.es/ode/view/es_2024112212_9190933</a><br><strong>Descripción:</strong> Recurso de programación por bloques con Scratch. Enseña fundamentos de programación, algoritmos, uso del entorno gráfico de Scratch y creación de primeros programas. Incluye actividad final de creación de una historia.<br><strong>Características:</strong> Altamente interactivo, aprendizaje basado en proyectos, incluye autoevaluación.<br><strong>Limitaciones:</strong> Enfocado exclusivamente en Scratch, requiere acompañamiento inicial del docente.</p>
        </div>
        <div class="card">
            <div class="badge"><i class="fas fa-laptop-code"></i> RED 2</div>
            <h3>Aprendiendo a programar (Bachillerato)</h3>
            <p><strong>Autor:</strong> Fuensanta Galiano Sánchez<br><strong>Nivel:</strong> 1º de Bachillerato | <strong>Área:</strong> Informática y Tecnologías de la Información<br><strong>Repositorio:</strong> Procomún (INTEF)<br><strong>URL:</strong> <a href="https://procomun.intef.es/ode/view/es_2025022312_9175716" target="_blank">https://procomun.intef.es/ode/view/es_2025022312_9175716</a><br><strong>Descripción:</strong> Iniciación a la programación para alumnado de 1º de Bachillerato. Conceptos fundamentales de algoritmos y lógica de programación.<br><strong>Características:</strong> ODE con metadatos LOM-ES, estructura didáctica clara.<br><strong>Limitaciones:</strong> Baja interactividad, enfoque mayormente teórico.</p>
        </div>
    </div>
</div>

<!-- REDISEÑO -->
<div id="rediseno" class="page">
    <h2>🛠️ Modelo Integral de Evaluación de Recursos Educativos Digitales (MIERED)</h2>
    
    <div class="card" style="margin-bottom: 2rem;">
        <h3><i class="fas fa-book-open"></i> Referentes</h3>
        <p>Este modelo surge del análisis de los siguientes marcos de evaluación:</p>
        <ul>
            <li><strong>Norma UNE 71362:2017</strong> “Calidad de los materiales educativos digitales”.</li>
            <li><strong>Herramienta COdA</strong> (Fernández-Pampillón et al., 2012).</li>
            <li><strong>LORI-AD</strong> (Adame, 2012).</li>
            <li><strong>Modelo por capas para evaluación de OAs</strong> (Tabares, Duque y Ovalle, 2017).</li>
            <li><strong>Libro Electrónico Multimedial de CVUDES</strong> y otros documentos del módulo.</li>
        </ul>
    </div>

    <div class="card" style="margin-bottom: 2rem;">
        <h3><i class="fas fa-exclamation-triangle"></i> Problemática que motiva el rediseño</h3>
        <ul>
            <li><strong>Fragmentación:</strong> la mayoría de los instrumentos se enfoca en un solo aspecto (didáctica, tecnología o accesibilidad).</li>
            <li><strong>Subjetividad:</strong> escalas basadas en estrellas o valoraciones cualitativas provocan alta variabilidad entre evaluadores.</li>
            <li><strong>Falta de adaptabilidad:</strong> no permiten ajustar los pesos de los criterios según el contexto educativo específico.</li>
            <li><strong>Complejidad para el docente no especialista:</strong> normas como la UNE 71362 son muy exhaustivas y requieren conocimientos técnicos avanzados.</li>
        </ul>
    </div>

    <div class="card" style="margin-bottom: 2rem;">
        <h3><i class="fas fa-list-ol"></i> Criterios de evaluación</h3>
        <p>El modelo MIERED define <strong>ocho criterios</strong> organizados en tres dimensiones:</p>
        
        <h4>Dimensión Didáctica (D)</h4>
        <ul>
            <li><strong>D1. Alineación con objetivos de aprendizaje:</strong> claridad y coherencia entre objetivos, contenidos, actividades y evaluación.</li>
            <li><strong>D2. Calidad del contenido:</strong> veracidad, actualidad, ausencia de sesgos, respeto a la propiedad intelectual, adecuación al nivel.</li>
            <li><strong>D3. Generación de aprendizaje y motivación:</strong> capacidad para estimular la reflexión, la autonomía y mantener el interés.</li>
        </ul>
        
        <h4>Dimensión Tecnológica (T)</h4>
        <ul>
            <li><strong>T1. Diseño, formato y usabilidad:</strong> presentación visual, navegación intuitiva, organización clara, funcionamiento correcto de enlaces.</li>
            <li><strong>T2. Reusabilidad y portabilidad:</strong> modularidad, independencia de plataforma, formatos estándar, posibilidad de adaptación a otros contextos.</li>
            <li><strong>T3. Interactividad y adaptabilidad:</strong> retroalimentación, control del usuario, personalización según respuestas o perfiles.</li>
        </ul>
        
        <h4>Dimensión de Accesibilidad y Metadatos (A)</h4>
        <ul>
            <li><strong>A1. Accesibilidad:</strong> cumplimiento de pautas WCAG 2.0 nivel A/AA, alternativas textuales, navegabilidad por teclado, compatibilidad con lectores de pantalla.</li>
            <li><strong>A2. Metadatos y localización:</strong> presencia de metadatos normalizados (título, autor, licencia, idioma, palabras clave), coherencia con el contenido.</li>
        </ul>
    </div>

    <div class="card" style="margin-bottom: 2rem;">
        <h3><i class="fas fa-weight-scale"></i> Métrica o escala de valoración</h3>
        <p>Escala cuantitativa de <strong>0 a 100</strong> para cada criterio, calculada mediante indicadores verificables:</p>
        <ul>
            <li>Cada criterio se desglosa en entre 3 y 6 subindicadores.</li>
            <li>Los subindicadores objetivos se valoran con <strong>1 (sí) o 0 (no)</strong>.</li>
            <li>Las preguntas de percepción utilizan escala Likert de 1 a 5, normalizada a 0-1.</li>
            <li>Puntuación final del criterio = promedio de subindicadores × 100.</li>
        </ul>
        <p><strong>Tabla de rangos interpretativos:</strong></p>
        <div class="table-responsive">
            <table>
                <tr><th>Puntaje</th><th>Calificación</th></tr>
                <tr><td>90-100</td><td>Excelente</td></tr>
                <tr><td>75-89</td><td>Bueno</td></tr>
                <tr><td>60-74</td><td>Aceptable</td></tr>
                <tr><td>40-59</td><td>Insuficiente</td></tr>
                <tr><td>0-39</td><td>Deficiente</td></tr>
            </table>
        </div>
    </div>

    <div class="card" style="margin-bottom: 2rem;">
        <h3><i class="fas fa-gears"></i> Metodología de aplicación</h3>
        <p>El modelo prevé tres capas de evaluación, que pueden usarse de forma combinada:</p>
        <ol>
            <li><strong>Capa de Autoevaluación (docente/desarrollador):</strong> el creador revisa todos los criterios antes de utilizar o publicar el RED.</li>
            <li><strong>Capa de Revisión por pares o expertos:</strong> un colega o especialista evalúa el mismo recurso con el mismo instrumento.</li>
            <li><strong>Capa de Percepción de usuarios (estudiantes):</strong> encuesta reducida sobre utilidad, facilidad de uso y motivación.</li>
        </ol>
    </div>

    <div class="card" style="margin-bottom: 2rem;">
        <h3><i class="fas fa-clipboard-check"></i> Instrumento de evaluación</h3>
        <p>Matriz de evaluación con los 8 criterios y sus subindicadores. A continuación se muestra un extracto:</p>
        <div class="table-responsive">
            <table>
                <thead>
                    <tr><th>Criterio</th><th>Subindicador</th><th>Cumplimiento</th></tr>
                </thead>
                <tbody>
                    <tr><td rowspan="4"><strong>D1. Alineación</strong></td><td>1. Se declaran explícitamente los objetivos de aprendizaje.</td><td>1/0</td></tr>
                    <tr><td>2. Los contenidos corresponden directamente a los objetivos.</td><td>1/0</td></tr>
                    <tr><td>3. Las actividades propuestas permiten alcanzar los objetivos.</td><td>1/0</td></tr>
                    <tr><td>4. Existe coherencia entre objetivos, contenidos y evaluación.</td><td>1/0</td></tr>
                    <tr><td rowspan="5"><strong>D2. Calidad del contenido</strong></td><td>1. La información es veraz, actualizada y sin errores.</td><td>1/0</td></tr>
                    <tr><td>2. Se citan adecuadamente las fuentes y se respetan los derechos de autor.</td><td>1/0</td></tr>
                    <tr><td>3. El lenguaje y la profundidad son adecuados para la audiencia.</td><td>1/0</td></tr>
                    <tr><td>4. Se evitan sesgos ideológicos o culturales.</td><td>1/0</td></tr>
                    <tr><td>5. Las ideas clave están resaltadas y organizadas.</td><td>1/0</td></tr>
                </tbody>
            </table>
        </div>
        <button class="btn-download" onclick="descargarInstrumento('MIERED')"><i class="fas fa-download"></i> Descargar instrumento MIERED completo</button>
    </div>
</div>

<!-- APLICACIÓN - ACTUALIZADA CON LOS RED SOLICITADOS Y RE-EVALUACIÓN -->
<div id="aplicacion" class="page">
    <h2>📋 Aplicación del modelo MIERED a los RED seleccionados</h2>
    
    <h3>📌 RED 1: Aprendiendo a programar con Scratch (África Gonzalo Castanedo)</h3>
    <p><em>Recurso interactivo de programación por bloques para 1º de ESO. URL: <a href="https://procomun.intef.es/ode/view/es_2024112212_9190933" target="_blank">https://procomun.intef.es/ode/view/es_2024112212_9190933</a></em></p>
    <div class="table-responsive">
        <table>
            <thead>
                <tr><th>Criterio</th><th>Puntaje (0-100)</th><th>Observaciones</th></tr>
            </thead>
            <tbody>
                <tr><td>D1. Alineación</td><td class="score-high">95</td><td>Objetivos claros y bien alineados con las actividades prácticas.</td></tr>
                <tr><td>D2. Calidad del contenido</td><td class="score-high">90</td><td>Contenido correcto y bien estructurado, adecuado para 1º ESO.</td></tr>
                <tr><td>D3. Aprendizaje y motivación</td><td class="score-high">98</td><td>Muy motivador; aprendizaje basado en proyectos y creación de historias.</td></tr>
                <tr><td>T1. Diseño y usabilidad</td><td class="score-high">92</td><td>Interfaz intuitiva y navegación fluida.</td></tr>
                <tr><td>T2. Reusabilidad y portabilidad</td><td class="score-high">85</td><td>Exportable a plataformas compatibles con Scratch.</td></tr>
                <tr><td>T3. Interactividad y adaptabilidad</td><td class="score-high">98</td><td>Altamente interactivo con retroalimentación inmediata.</td></tr>
                <tr><td>A1. Accesibilidad</td><td class="score-mid">70</td><td>Mejorable en contraste y navegación por teclado.</td></tr>
                <tr><td>A2. Metadatos y localización</td><td class="score-mid">75</td><td>Metadatos presentes pero incompletos en cuanto a licencia.</td></tr>
                <tr><td><strong>Promedio simple</strong></td><td class="score-high"><strong>87.9 (Bueno)</strong></td><td></td></tr>
            </tbody>
        </table>
    </div>

    <h3>📌 RED 2: Aprendiendo a programar (Fuensanta Galiano Sánchez)</h3>
    <p><em>Recurso teórico de iniciación a la programación para 1º de Bachillerato. URL: <a href="https://procomun.intef.es/ode/view/es_2025022312_9175716" target="_blank">https://procomun.intef.es/ode/view/es_2025022312_9175716</a></em></p>
    <div class="table-responsive">
        <table>
            <thead>
                <tr><th>Criterio</th><th>Puntaje (0-100)</th><th>Observaciones</th></tr>
            </thead>
            <tbody>
                <tr><td>D1. Alineación</td><td class="score-mid">75</td><td>Objetivos declarados pero sin actividades prácticas asociadas.</td></tr>
                <tr><td>D2. Calidad del contenido</td><td class="score-mid">70</td><td>Contenido correcto pero algo desactualizado; pocos ejemplos.</td></tr>
                <tr><td>D3. Aprendizaje y motivación</td><td class="score-mid">60</td><td>Formato expositivo que no involucra activamente al estudiante.</td></tr>
                <tr><td>T1. Diseño y usabilidad</td><td class="score-mid">68</td><td>Navegación básica; interfaz mejorable.</td></tr>
                <tr><td>T2. Reusabilidad y portabilidad</td><td class="score-mid">65</td><td>Formato propietario con difícil adaptación a otros contextos.</td></tr>
                <tr><td>T3. Interactividad y adaptabilidad</td><td class="score-low">30</td><td>Escasa interactividad; sin retroalimentación.</td></tr>
                <tr><td>A1. Accesibilidad</td><td class="score-low">45</td><td>No cumple con pautas básicas de accesibilidad.</td></tr>
                <tr><td>A2. Metadatos y localización</td><td class="score-low">50</td><td>Metadatos insuficientes y sin información de licencia clara.</td></tr>
                <tr><td><strong>Promedio simple</strong></td><td class="score-mid"><strong>57.9 (Insuficiente)</strong></td><td></td></tr>
            </tbody>
        </table>
    </div>
    
    <div class="instrument-box">
        <strong><i class="fas fa-chart-simple"></i> Conclusión de la evaluación:</strong><br>
        • El RED 1 (Scratch) obtiene una calificación de "Bueno", destacando su alta interactividad, motivación y diseño. Es un recurso altamente recomendable para la enseñanza de programación en ESO.<br>
        • El RED 2 (teórico) obtiene una calificación de "Insuficiente", principalmente por su baja interactividad y falta de adaptabilidad. Requiere una revisión profunda para mejorar su efectividad didáctica.<br>
        • La aplicación del modelo MIERED ha permitido identificar claramente las fortalezas y debilidades de cada recurso, proporcionando una base sólida para la toma de decisiones sobre su uso en el aula.
    </div>

    <h3><i class="fas fa-question-circle"></i> Respuestas a los interrogantes del trabajo</h3>
    
    <div class="response-box">
        <h4>1. ¿De qué manera el modelo rediseñado permite realizar una adecuada evaluación de un RED?</h4>
        <p>MIERED integra las dimensiones didáctica, tecnológica y de accesibilidad en un solo instrumento, con indicadores verificables que reducen la subjetividad. Su estructura por capas permite que tanto el creador como los usuarios finales aporten valoraciones complementarias, ofreciendo una visión holística. La escala cuantitativa de 0 a 100 y los rangos interpretativos facilitan la comparación entre recursos y la identificación de áreas de mejora concretas.</p>
    </div>

    <div class="response-box">
        <h4>2. ¿Qué ventajas tiene el modelo rediseñado frente a otros modelos existentes en el mercado?</h4>
        <ul>
            <li><strong>Integralidad:</strong> a diferencia de COdA, que omite metadatos, o del modelo por capas que no profundiza en la percepción didáctica, MIERED cubre todas las dimensiones relevantes.</li>
            <li><strong>Flexibilidad:</strong> permite asignar pesos diferenciados a los criterios según el contexto (por ejemplo, en un recurso para educación inclusiva, la accesibilidad puede tener mayor peso).</li>
            <li><strong>Simplicidad aplicada:</strong> mantiene un número reducido de criterios (8 frente a los 15 de la UNE 71362) sin perder profundidad, lo que lo hace manejable para docentes no especialistas.</li>
            <li><strong>Enfoque evolutivo:</strong> la evaluación por capas posibilita su uso tanto en la fase de diseño (autoevaluación) como en la de uso real (percepción de estudiantes), algo que modelos como LORI no contemplan de forma estructurada.</li>
        </ul>
    </div>

    <div class="response-box">
        <h4>3. ¿Qué elementos técnicos, pedagógicos y comunicacionales deben ser mejorados en el modelo rediseñado?</h4>
        <ul>
            <li><strong>Técnicos:</strong> se podría automatizar parcialmente la verificación de metadatos y enlaces rotos mediante scripts, como sugiere el artículo de Tabares et al., para aliviar la carga manual.</li>
            <li><strong>Pedagógicos:</strong> sería deseable incorporar un indicador sobre la variedad de estrategias de aprendizaje (visual, auditivo, kinestésico) y otro sobre la alineación con competencias específicas del currículo.</li>
            <li><strong>Comunicacionales:</strong> el instrumento para estudiantes podría beneficiarse de un lenguaje más cercano y de iconos gráficos para facilitar la respuesta. Asimismo, la presentación de resultados debería incluir un dashboard visual (tipo semáforo) que comunique rápidamente las fortalezas y debilidades.</li>
        </ul>
    </div>
</div>

<!-- REFERENCIAS -->
<div id="referencias" class="page">
    <h2>📖 Referencias bibliográficas</h2>
    <ul style="line-height: 1.8;">
        <li>Adame, S. I. (2012). Instrumento para evaluar Recursos Educativos Digitales, LORI-AD.</li>
        <li>Chinchilla, Z. (2015). <em>Recursos Educativos Digitales</em> [LEM]. Centro de Educación Virtual UDES.</li>
        <li>Fernández-Pampillón, A. M. (2017). Norma UNE 71362: Calidad de los materiales educativos digitales. <em>UNE</em>.</li>
        <li>Fernández-Pampillón, A. M., Domínguez, E., & Armas, I. (2012). <em>COdA: Herramienta de evaluación de la calidad de los Objetos de Aprendizaje</em> (V 1.1). Universidad Complutense de Madrid.</li>
        <li>Marzal, M. Á., Calzada-Prado, J., & Ruvalcaba-Burgoa, E. (2015). Objetos de aprendizaje como recursos educativos en programas de alfabetización en información. <em>Investigación Bibliotecológica, 29</em>(66), 139-168.</li>
        <li>Pinto, M., Gómez-Camarero, C., & Fernández-Ramos, A. (2012). Los recursos educativos electrónicos: perspectivas y herramientas de evaluación. <em>Perspectivas em Ciência da Informação, 17</em>(3), 82-99.</li>
        <li>Prieto Taborda, M. A., Bermón Angarita, L. y Ramírez Castañeda, L. A. (2019). Diseño, desarrollo y evaluación de un recurso educativo digital para la introducción a la Administración de Sistemas Informáticos. <em>Revista Virtual Universidad Católica del Norte</em>, (56), 31-51.</li>
        <li>Tabares, V., Duque, N. D., & Ovalle, D. A. (2017). Modelo por capas para evaluación de la calidad de Objetos de Aprendizaje en repositorios. <em>REDIE, 19</em>(3).</li>
        <li>INTEF. Procomún – Repositorio de Recursos Educativos Abiertos. <a href="https://procomun.intef.es/" target="_blank">https://procomun.intef.es/</a></li>
    </ul>
</div>

<footer>
    <i class="fas fa-university"></i> Universidad de Santander<br>
    Marlon David Vergara Lozano | Profesor Eduardo Méndez Bonilla | Evaluación de RED – Portafolio digital
</footer>

<script>
    const pages = document.querySelectorAll('.page');
    function showPage(pageId) {
        pages.forEach(page => page.classList.remove('active-page'));
        const active = document.getElementById(pageId);
        if(active) active.classList.add('active-page');
        localStorage.setItem('currentPage', pageId);
    }
    document.querySelectorAll('.nav-link[data-page]').forEach(btn => {
        btn.addEventListener('click', (e) => {
            const pageId = btn.getAttribute('data-page');
            if(pageId) showPage(pageId);
        });
    });
    document.querySelectorAll('.dropdown-content a[data-page]').forEach(link => {
        link.addEventListener('click', (e) => {
            e.preventDefault();
            const pageId = link.getAttribute('data-page');
            if(pageId) showPage(pageId);
        });
    });

    function descargarInstrumento(nombre) {
        let contenido = '';
        let tipo = 'text/plain;charset=utf-8';
        let extension = '.txt';

        if(nombre === 'COdA') {
            contenido = '=== INSTRUMENTO COdA ===\n\nCRITERIOS (escala 1-5):\n1. Objetivos: ___\n2. Calidad contenidos: ___\n3. Reflexión: ___\n4. Interactividad: ___\n5. Motivación: ___\n6. Formato: ___\n7. Usabilidad: ___\n8. Accesibilidad: ___\n9. Reusabilidad: ___\n10. Interoperabilidad: ___\n\nOBSERVACIONES: ___________________';
        } else if(nombre === 'LORI') {
            contenido = '=== INSTRUMENTO LORI ===\n\nCRITERIOS (escala 1-5):\n1. Calidad contenido: ___\n2. Adecuación objetivos: ___\n3. Feedback: ___\n4. Motivación: ___\n5. Diseño: ___\n6. Usabilidad: ___\n7. Accesibilidad: ___\n8. Reusabilidad: ___\n9. Estándares: ___\n\nCOMENTARIOS: ___________________';
        } else if(nombre === 'EVALUAREED') {
            contenido = '=== INSTRUMENTO EVALUAREED ===\n\n1. Calidad contenido (Sí/No): ___\n2. Objetivos claros (Sí/No): ___\n3. Feedback (Sí/No): ___\n4. Usabilidad (1-5): ___\n5. Motivación (1-5): ___\n6. Accesibilidad (Sí/No): ___\n7. Requerimientos técnicos (Sí/No): ___\n8. Propiedad intelectual: ___\n9. Efectividad (1-5): ___\n\nINFORME: ___________________';
        } else if(nombre === 'MIERED') {
            // Contenido del instrumento interactivo completo
            contenido = `<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Instrumento MIERED - Evaluación de RED</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:opsz,wght@14..32,400;14..32,500;14..32,600;14..32,700&display=swap" rel="stylesheet">
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Inter', sans-serif; background: #f5f7fa; color: #1e2a3e; line-height: 1.5; padding: 2rem; }
        .container { max-width: 1000px; margin: 0 auto; background: white; border-radius: 32px; box-shadow: 0 10px 30px rgba(0,0,0,0.05); padding: 2rem; }
        h1 { font-size: 2rem; margin-bottom: 0.5rem; color: #2c3e66; border-left: 6px solid #e67e22; padding-left: 1rem; }
        .subtitulo { font-size: 1rem; color: #5b6e8c; margin-bottom: 2rem; }
        .criterio { background: #ffffff; border-radius: 20px; box-shadow: 0 5px 15px rgba(0,0,0,0.03); margin-bottom: 1.5rem; border: 1px solid #e0e6ed; overflow: hidden; }
        .criterio-header { background: #2e7d32; color: white; padding: 1rem 1.5rem; display: flex; justify-content: space-between; align-items: center; }
        .criterio-header h3 { font-size: 1.2rem; font-weight: 600; }
        .puntuacion-criterio { background: rgba(255,255,255,0.2); padding: 0.3rem 0.8rem; border-radius: 30px; font-weight: 600; font-size: 0.9rem; }
        .subindicadores { padding: 1rem 1.5rem; }
        .subindicador { display: flex; align-items: center; gap: 1rem; padding: 0.8rem 0; border-bottom: 1px solid #f0f0f0; }
        .subindicador:last-child { border-bottom: none; }
        .subindicador p { flex: 1; margin: 0; font-size: 0.95rem; }
        .checkbox-wrapper { display: flex; align-items: center; gap: 0.3rem; background: #f5f7fa; padding: 0.3rem 0.8rem; border-radius: 20px; }
        .checkbox-wrapper input[type="checkbox"] { width: 1.2rem; height: 1.2rem; accent-color: #2e7d32; cursor: pointer; }
        .checkbox-wrapper label { font-size: 0.85rem; font-weight: 500; color: #2c3e66; cursor: pointer; }
        .resumen { background: #fef9f0; border-left: 6px solid #e67e22; border-radius: 20px; padding: 1.5rem; margin-top: 2rem; }
        .resumen h2 { color: #2c3e66; margin-bottom: 1rem; }
        .resultado { display: flex; justify-content: space-between; flex-wrap: wrap; gap: 1rem; margin-bottom: 1rem; }
        .resultado-item { background: white; padding: 1rem; border-radius: 16px; flex: 1; min-width: 200px; box-shadow: 0 3px 10px rgba(0,0,0,0.03); }
        .resultado-item h4 { font-size: 0.85rem; color: #5b6e8c; margin-bottom: 0.3rem; }
        .resultado-item .valor { font-size: 2rem; font-weight: 700; color: #2e7d32; }
        .calificacion-final { font-size: 1.5rem; font-weight: 700; padding: 0.8rem; border-radius: 30px; text-align: center; margin: 1.5rem 0; }
        .excelente { background: #d4edda; color: #155724; }
        .bueno { background: #d1ecf1; color: #0c5460; }
        .aceptable { background: #fff3cd; color: #856404; }
        .insuficiente { background: #ffeeba; color: #856404; }
        .deficiente { background: #f8d7da; color: #721c24; }
        .botones { display: flex; gap: 1rem; margin-top: 1rem; flex-wrap: wrap; }
        .btn { background: #e67e22; color: white; border: none; padding: 0.8rem 1.5rem; border-radius: 40px; font-weight: 600; cursor: pointer; font-size: 1rem; transition: background 0.2s; display: inline-flex; align-items: center; gap: 0.5rem; }
        .btn:hover { background: #d35400; }
        .btn-outline { background: white; color: #2e7d32; border: 2px solid #2e7d32; }
        .btn-outline:hover { background: #e8f5e9; }
        @media (max-width: 700px) { body { padding: 1rem; } .container { padding: 1.2rem; } }
    </style>
</head>
<body>
    <div class="container">
        <h1>Instrumento MIERED</h1>
        <p class="subtitulo">Modelo Integral de Evaluación de Recursos Educativos Digitales<br>Marque cada subindicador que el recurso cumpla satisfactoriamente. Al final obtendrá una puntuación de 0 a 100 por criterio y una valoración global.</p>
        <!-- Criterios D1..A2 -->
        <div class="criterio">
            <div class="criterio-header"><h3>D1. Alineación con objetivos de aprendizaje</h3><span class="puntuacion-criterio" id="puntD1">-</span></div>
            <div class="subindicadores" id="subD1">
                <div class="subindicador"><p>1. Se declaran explícitamente los objetivos.</p><div class="checkbox-wrapper"><input type="checkbox" id="d1_1"><label for="d1_1">Cumple</label></div></div>
                <div class="subindicador"><p>2. Los contenidos corresponden directamente a los objetivos.</p><div class="checkbox-wrapper"><input type="checkbox" id="d1_2"><label for="d1_2">Cumple</label></div></div>
                <div class="subindicador"><p>3. Las actividades permiten alcanzar los objetivos.</p><div class="checkbox-wrapper"><input type="checkbox" id="d1_3"><label for="d1_3">Cumple</label></div></div>
                <div class="subindicador"><p>4. Coherencia entre objetivos, contenidos y evaluación.</p><div class="checkbox-wrapper"><input type="checkbox" id="d1_4"><label for="d1_4">Cumple</label></div></div>
            </div>
        </div>
        <!-- Los demás criterios se insertan de la misma forma -->
        <div class="criterio">
            <div class="criterio-header"><h3>D2. Calidad del contenido</h3><span class="puntuacion-criterio" id="puntD2">-</span></div>
            <div class="subindicadores" id="subD2">
                <div class="subindicador"><p>1. Información veraz, actualizada y sin errores.</p><div class="checkbox-wrapper"><input type="checkbox" id="d2_1"><label for="d2_1">Cumple</label></div></div>
                <div class="subindicador"><p>2. Cita de fuentes y respeto a propiedad intelectual.</p><div class="checkbox-wrapper"><input type="checkbox" id="d2_2"><label for="d2_2">Cumple</label></div></div>
                <div class="subindicador"><p>3. Lenguaje y profundidad adecuados para la audiencia.</p><div class="checkbox-wrapper"><input type="checkbox" id="d2_3"><label for="d2_3">Cumple</label></div></div>
                <div class="subindicador"><p>4. Ausencia de sesgos ideológicos o culturales.</p><div class="checkbox-wrapper"><input type="checkbox" id="d2_4"><label for="d2_4">Cumple</label></div></div>
                <div class="subindicador"><p>5. Ideas clave resaltadas y organizadas.</p><div class="checkbox-wrapper"><input type="checkbox" id="d2_5"><label for="d2_5">Cumple</label></div></div>
            </div>
        </div>
        <div class="criterio">
            <div class="criterio-header"><h3>D3. Generación de aprendizaje y motivación</h3><span class="puntuacion-criterio" id="puntD3">-</span></div>
            <div class="subindicadores" id="subD3">
                <div class="subindicador"><p>1. Estimula la reflexión y el pensamiento crítico.</p><div class="checkbox-wrapper"><input type="checkbox" id="d3_1"><label for="d3_1">Cumple</label></div></div>
                <div class="subindicador"><p>2. Promueve la autonomía del estudiante.</p><div class="checkbox-wrapper"><input type="checkbox" id="d3_2"><label for="d3_2">Cumple</label></div></div>
                <div class="subindicador"><p>3. Es atractivo y mantiene el interés.</p><div class="checkbox-wrapper"><input type="checkbox" id="d3_3"><label for="d3_3">Cumple</label></div></div>
            </div>
        </div>
        <div class="criterio">
            <div class="criterio-header"><h3>T1. Diseño, formato y usabilidad</h3><span class="puntuacion-criterio" id="puntT1">-</span></div>
            <div class="subindicadores" id="subT1">
                <div class="subindicador"><p>1. Interfaz limpia y navegación intuitiva.</p><div class="checkbox-wrapper"><input type="checkbox" id="t1_1"><label for="t1_1">Cumple</label></div></div>
                <div class="subindicador"><p>2. Enlaces y botones funcionan correctamente.</p><div class="checkbox-wrapper"><input type="checkbox" id="t1_2"><label for="t1_2">Cumple</label></div></div>
                <div class="subindicador"><p>3. Visualización correcta en distintos dispositivos.</p><div class="checkbox-wrapper"><input type="checkbox" id="t1_3"><label for="t1_3">Cumple</label></div></div>
                <div class="subindicador"><p>4. Instrucciones de uso claras (si son necesarias).</p><div class="checkbox-wrapper"><input type="checkbox" id="t1_4"><label for="t1_4">Cumple</label></div></div>
            </div>
        </div>
        <div class="criterio">
            <div class="criterio-header"><h3>T2. Reusabilidad y portabilidad</h3><span class="puntuacion-criterio" id="puntT2">-</span></div>
            <div class="subindicadores" id="subT2">
                <div class="subindicador"><p>1. Estructura modular que permite reutilización.</p><div class="checkbox-wrapper"><input type="checkbox" id="t2_1"><label for="t2_1">Cumple</label></div></div>
                <div class="subindicador"><p>2. Formatos estándar sin dependencia de software propietario.</p><div class="checkbox-wrapper"><input type="checkbox" id="t2_2"><label for="t2_2">Cumple</label></div></div>
                <div class="subindicador"><p>3. Posibilidad de uso en distintos contextos educativos.</p><div class="checkbox-wrapper"><input type="checkbox" id="t2_3"><label for="t2_3">Cumple</label></div></div>
            </div>
        </div>
        <div class="criterio">
            <div class="criterio-header"><h3>T3. Interactividad y adaptabilidad</h3><span class="puntuacion-criterio" id="puntT3">-</span></div>
            <div class="subindicadores" id="subT3">
                <div class="subindicador"><p>1. Retroalimentación inmediata a las acciones del usuario.</p><div class="checkbox-wrapper"><input type="checkbox" id="t3_1"><label for="t3_1">Cumple</label></div></div>
                <div class="subindicador"><p>2. Posibilidad de personalizar el contenido según respuestas.</p><div class="checkbox-wrapper"><input type="checkbox" id="t3_2"><label for="t3_2">Cumple</label></div></div>
                <div class="subindicador"><p>3. Control del usuario sobre el ritmo de aprendizaje.</p><div class="checkbox-wrapper"><input type="checkbox" id="t3_3"><label for="t3_3">Cumple</label></div></div>
            </div>
        </div>
        <div class="criterio">
            <div class="criterio-header"><h3>A1. Accesibilidad</h3><span class="puntuacion-criterio" id="puntA1">-</span></div>
            <div class="subindicadores" id="subA1">
                <div class="subindicador"><p>1. Texto alternativo en imágenes y gráficos.</p><div class="checkbox-wrapper"><input type="checkbox" id="a1_1"><label for="a1_1">Cumple</label></div></div>
                <div class="subindicador"><p>2. Subtítulos en contenidos de audio/video.</p><div class="checkbox-wrapper"><input type="checkbox" id="a1_2"><label for="a1_2">Cumple</label></div></div>
                <div class="subindicador"><p>3. Navegabilidad mediante teclado.</p><div class="checkbox-wrapper"><input type="checkbox" id="a1_3"><label for="a1_3">Cumple</label></div></div>
                <div class="subindicador"><p>4. Contraste adecuado de colores.</p><div class="checkbox-wrapper"><input type="checkbox" id="a1_4"><label for="a1_4">Cumple</label></div></div>
            </div>
        </div>
        <div class="criterio">
            <div class="criterio-header"><h3>A2. Metadatos y localización</h3><span class="puntuacion-criterio" id="puntA2">-</span></div>
            <div class="subindicadores" id="subA2">
                <div class="subindicador"><p>1. Título, autor y licencia claramente visibles.</p><div class="checkbox-wrapper"><input type="checkbox" id="a2_1"><label for="a2_1">Cumple</label></div></div>
                <div class="subindicador"><p>2. Palabras clave y descripción normalizadas.</p><div class="checkbox-wrapper"><input type="checkbox" id="a2_2"><label for="a2_2">Cumple</label></div></div>
                <div class="subindicador"><p>3. Los metadatos describen fielmente el contenido.</p><div class="checkbox-wrapper"><input type="checkbox" id="a2_3"><label for="a2_3">Cumple</label></div></div>
            </div>
        </div>
        <div class="resumen" id="panelResultados">
            <h2>Resultado de la evaluación</h2>
            <div class="resultado">
                <div class="resultado-item"><h4>Promedio obtenido</h4><div class="valor" id="promedioTotal">0</div></div>
                <div class="resultado-item"><h4>Calificación</h4><div class="valor" id="calificacionTexto">-</div></div>
            </div>
            <div id="barraCalificacion" class="calificacion-final">Complete todos los criterios y presione Calcular</div>
            <div class="botones">
                <button class="btn" onclick="calcularPuntuacion()"><i class="fas fa-calculator"></i> Calcular puntuación</button>
                <button class="btn btn-outline" onclick="descargarResultado()"><i class="fas fa-download"></i> Descargar resultado</button>
            </div>
        </div>
    </div>
    <script>
        const criterios = ['D1','D2','D3','T1','T2','T3','A1','A2'];
        const numSubindicadores = { D1:4, D2:5, D3:3, T1:4, T2:3, T3:3, A1:4, A2:3 };
        function calcularPuntuacion() {
            let totalPuntos = 0;
            let totalCriterios = 0;
            criterios.forEach(crit => {
                let cumplidos = 0;
                let total = numSubindicadores[crit];
                for (let i = 1; i <= total; i++) {
                    const checkbox = document.getElementById(crit.toLowerCase()+'_'+i);
                    if (checkbox && checkbox.checked) cumplidos++;
                }
                const puntuacion = total > 0 ? Math.round((cumplidos/total)*100) : 0;
                document.getElementById('punt'+crit).textContent = puntuacion+' pts';
                totalPuntos += puntuacion;
                totalCriterios++;
            });
            const promedio = totalCriterios > 0 ? Math.round(totalPuntos/totalCriterios) : 0;
            document.getElementById('promedioTotal').textContent = promedio;
            let calificacion = '', clase = '';
            if (promedio >= 90) { calificacion = 'Excelente'; clase = 'excelente'; }
            else if (promedio >= 75) { calificacion = 'Bueno'; clase = 'bueno'; }
            else if (promedio >= 60) { calificacion = 'Aceptable'; clase = 'aceptable'; }
            else if (promedio >= 40) { calificacion = 'Insuficiente'; clase = 'insuficiente'; }
            else { calificacion = 'Deficiente'; clase = 'deficiente'; }
            document.getElementById('calificacionTexto').textContent = calificacion;
            const barra = document.getElementById('barraCalificacion');
            barra.textContent = 'Calificación: '+calificacion+' ('+promedio+' puntos)';
            barra.className = 'calificacion-final '+clase;
        }
        function descargarResultado() {
            let texto = 'RESULTADOS DE EVALUACIÓN MIERED\\n\\n';
            criterios.forEach(crit => {
                const punt = document.getElementById('punt'+crit).textContent;
                texto += crit + ': ' + punt + '\\n';
            });
            const prom = document.getElementById('promedioTotal').textContent;
            const calif = document.getElementById('calificacionTexto').textContent;
            texto += '\\nPromedio total: ' + prom + ' puntos\\nCalificación: ' + calif;
            const blob = new Blob([texto], {type: 'text/plain;charset=utf-8'});
            const link = document.createElement('a');
            link.href = URL.createObjectURL(blob);
            link.download = 'resultado_MIERED.txt';
            link.click();
            URL.revokeObjectURL(link.href);
        }
    <\\/script>
</body>
</html>`;
            tipo = 'text/html;charset=utf-8';
            extension = '.html';
        }

        const blob = new Blob([contenido], {type: tipo});
        const link = document.createElement('a');
        link.href = URL.createObjectURL(blob);
        link.download = `Instrumento_${nombre}${extension}`;
        link.click();
        URL.revokeObjectURL(link.href);
    }

    const saved = localStorage.getItem('currentPage');
    if(saved && document.getElementById(saved)) showPage(saved);
    else showPage('inicio');
</script>
</body>
</html>
