<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Polémica Intuicionismo-Formalismo</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #2c3e50, #34495e);
            color: white;
            padding: 30px;
            text-align: center;
        }

        .header h1 {
            font-size: 2.5rem;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        }

        .header p {
            font-size: 1.1rem;
            opacity: 0.9;
        }

        .timeline-container {
            padding: 40px 20px;
            position: relative;
            overflow-x: auto;
        }

        .timeline {
            position: relative;
            display: flex;
            flex-direction: column;
            gap: 40px;
        }

        .timeline::before {
            content: '';
            position: absolute;
            left: 50%;
            top: 0;
            bottom: 0;
            width: 4px;
            background: linear-gradient(to bottom, #3498db, #9b59b6, #e74c3c);
            transform: translateX(-50%);
            z-index: 1;
        }

        .timeline-item {
            position: relative;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .timeline-item:nth-child(odd) .event-card {
            margin-right: 60%;
            text-align: right;
        }

        .timeline-item:nth-child(even) .event-card {
            margin-left: 60%;
            text-align: left;
        }

        .event-card {
            background: white;
            border-radius: 15px;
            padding: 25px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            border: 2px solid transparent;
            transition: all 0.3s ease;
            cursor: pointer;
            position: relative;
            max-width: 400px;
            width: 100%;
        }

        .event-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.15);
            border-color: #3498db;
        }

        .event-card.ancient {
            border-left: 5px solid #e67e22;
        }

        .event-card.modern {
            border-left: 5px solid #27ae60;
        }

        .event-card.debate {
            border-left: 5px solid #e74c3c;
        }

        .event-card.resolution {
            border-left: 5px solid #9b59b6;
        }

        .timeline-dot {
            position: absolute;
            left: 50%;
            top: 50%;
            transform: translate(-50%, -50%);
            width: 20px;
            height: 20px;
            background: white;
            border: 4px solid #3498db;
            border-radius: 50%;
            z-index: 2;
        }

        .timeline-item:nth-child(even) .timeline-dot {
            border-color: #e74c3c;
        }

        .date {
            font-size: 1.4rem;
            font-weight: bold;
            color: #2c3e50;
            margin-bottom: 10px;
        }

        .title {
            font-size: 1.2rem;
            font-weight: bold;
            color: #34495e;
            margin-bottom: 15px;
            line-height: 1.3;
        }

        .description {
            color: #7f8c8d;
            line-height: 1.6;
            margin-bottom: 15px;
        }

        .author {
            font-style: italic;
            color: #95a5a6;
            font-size: 0.9rem;
        }

        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.8);
            backdrop-filter: blur(5px);
        }

        .modal-content {
            background-color: white;
            margin: 5% auto;
            padding: 40px;
            border-radius: 20px;
            width: 90%;
            max-width: 700px;
            max-height: 80vh;
            overflow-y: auto;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.3);
        }

        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
            cursor: pointer;
            transition: color 0.3s;
        }

        .close:hover {
            color: #e74c3c;
        }

        .legend {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin-bottom: 40px;
            flex-wrap: wrap;
        }

        .legend-item {
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .legend-color {
            width: 20px;
            height: 4px;
            border-radius: 2px;
        }

        .controls {
            text-align: center;
            margin-bottom: 30px;
        }

        .filter-btn {
            background: linear-gradient(45deg, #3498db, #2980b9);
            color: white;
            border: none;
            padding: 10px 20px;
            margin: 0 5px;
            border-radius: 25px;
            cursor: pointer;
            transition: all 0.3s ease;
        }

        .filter-btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(52, 152, 219, 0.4);
        }

        .filter-btn.active {
            background: linear-gradient(45deg, #e74c3c, #c0392b);
        }

        @media (max-width: 768px) {
            .timeline::before {
                left: 30px;
            }

            .timeline-item:nth-child(odd) .event-card,
            .timeline-item:nth-child(even) .event-card {
                margin-left: 80px;
                margin-right: 0;
                text-align: left;
            }

            .timeline-dot {
                left: 30px;
            }

            .header h1 {
                font-size: 2rem;
            }

            .legend {
                flex-direction: column;
                align-items: center;
                gap: 15px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>La Polémica Intuicionismo-Formalismo</h1>
            <p>Historia de los Fundamentos Matemáticos (Siglos IV a.C. - XX d.C.)</p>
            <div style="margin-top: 20px; font-size: 1rem; opacity: 0.8;">
                <strong>Autores:</strong> Jhon Fredy Sánchez - Miguel Ángel Quintero
            </div>
        </div>

        <div class="timeline-container">
            <div class="legend">
                <div class="legend-item">
                    <div class="legend-color" style="background-color: #e67e22;"></div>
                    <span>Período Clásico</span>
                </div>
                <div class="legend-item">
                    <div class="legend-color" style="background-color: #27ae60;"></div>
                    <span>Desarrollo Moderno</span>
                </div>
                <div class="legend-item">
                    <div class="legend-color" style="background-color: #e74c3c;"></div>
                    <span>Debate 1920s</span>
                </div>
                <div class="legend-item">
                    <div class="legend-color" style="background-color: #9b59b6;"></div>
                    <span>Resolución</span>
                </div>
            </div>

            <div class="controls">
                <button class="filter-btn active" onclick="filterEvents('all')">Todos</button>
                <button class="filter-btn" onclick="filterEvents('ancient')">Clásico</button>
                <button class="filter-btn" onclick="filterEvents('modern')">Moderno</button>
                <button class="filter-btn" onclick="filterEvents('debate')">Debate</button>
                <button class="filter-btn" onclick="filterEvents('resolution')">Resolución</button>
            </div>

            <div class="timeline" id="timeline">
                <!-- Eventos serán agregados aquí por JavaScript -->
            </div>
        </div>
    </div>

    <!-- Modal -->
    <div id="eventModal" class="modal">
        <div class="modal-content">
            <span class="close">&times;</span>
            <div id="modalContent"></div>
        </div>
    </div>

    <script>
        const events = [
            {
                date: "~300 a.C.",
                title: "Los Elementos de Euclides",
                description: "Establecimiento de los fundamentos axiomáticos de la geometría clásica.",
                details: "Euclides sistematiza el conocimiento geométrico de su época en 13 libros, estableciendo un modelo axiomático que influenciará las matemáticas durante más de 2000 años. Los postulados euclidianos se convertirán en el paradigma de rigor matemático.",
                author: "Euclides de Alejandría",
                category: "ancient"
            },
            {
                date: "1874",
                title: "Inicio de la Teoría de Conjuntos",
                description: "Cantor inicia la exposición de su teoría de conjuntos, revolucionando las matemáticas.",
                details: "Georg Cantor introduce conceptos revolucionarios como diferentes clases de infinito, ordinales y cardinales transfinitos. Establece que las únicas condiciones para incorporar un nuevo concepto matemático son: 1) que no sea contradictorio, 2) que se defina en función de conceptos previamente aceptados.",
                author: "Georg Cantor",
                category: "modern"
            },
            {
                date: "1879",
                title: "Begriffsschrift de Frege",
                description: "Nacimiento de la lógica matemática moderna con el lenguaje simbólico universal.",
                details: "Gottlob Frege publica 'Conceptografía', desarrollando un lenguaje universal lógico-simbólico para eliminar malentendidos del lenguaje natural. Representa el primer avance sustancial en lógica desde Aristóteles.",
                author: "Gottlob Frege",
                category: "modern"
            },
            {
                date: "1897-1902",
                title: "Las Paradojas de la Teoría de Conjuntos",
                description: "Descubrimiento de contradicciones fundamentales en los principios cantorianos.",
                details: "Cesare Burali-Forti (1897), Cantor (1899) y Bertrand Russell (1902) descubren paradojas que amenazan los fundamentos de las matemáticas. La paradoja de Russell: '¿El conjunto de todos los conjuntos que no son miembros de sí mismos pertenece a sí mismo?' tiene un efecto devastador.",
                author: "Burali-Forti, Cantor, Russell",
                category: "modern"
            },
            {
                date: "1900",
                title: "Los 23 Problemas de Hilbert",
                description: "Hilbert plantea los grandes desafíos matemáticos del siglo XX en París.",
                details: "David Hilbert presenta su famosa lista de 23 problemas matemáticos, expresando su convicción de que 'todo problema ha de tener su solución basada en la pura razón'. Establece las bases del programa formalista con el ideal axiomático.",
                author: "David Hilbert",
                category: "modern"
            },
            {
                date: "1907",
                title: "Tesis Doctoral de Brouwer",
                description: "'Sobre los fundamentos de las matemáticas' - Primer acto del intuicionismo.",
                details: "Luitzen Brouwer presenta su tesis doctoral, declarando que 'No pueden existir matemáticas, si no han sido construidas intuitivamente'. Establece los tres temas centrales: La construcción de las matemáticas, Matemáticas y experiencia, y Matemáticas y lógica.",
                author: "L.E.J. Brouwer",
                category: "modern"
            },
            {
                date: "1908",
                title: "Axiomatización de Zermelo",
                description: "Primera axiomatización sistemática de la teoría de conjuntos (ZFC).",
                details: "Ernst Zermelo publica la primera axiomatización de la Teoría de Conjuntos que, con las posteriores aportaciones de Fraenkel y Skolem, se conoce como sistema ZFC. Supera las paradojas conocidas pero utiliza el controvertido axioma de elección.",
                author: "Ernst Zermelo",
                category: "modern"
            },
            {
                date: "1910-1913",
                title: "Principia Mathematica",
                description: "Russell y Whitehead continúan el programa logicista con la teoría de tipos.",
                details: "Publicación en tres volúmenes de los Principia Mathematica. Russell y Whitehead desarrollan la teoría de tipos (simple o ramificada) para sortear las paradojas, creando una jerarquía acumulativa donde definen los números como clases de clases.",
                author: "Russell y Whitehead",
                category: "modern"
            },
            {
                date: "1912",
                title: "Conferencia de Brouwer en la Academia Holandesa",
                description: "Primera explicación detallada de intuicionismo vs. formalismo.",
                details: "Brouwer pronuncia su conferencia de admisión en la Academia Holandesa, donde explica las diferencias entre ambas concepciones: 'Los intuicionistas dicen que la exactitud matemática reside en la mente; los formalistas, en el papel'.",
                author: "L.E.J. Brouwer",
                category: "debate"
            },
            {
                date: "1918-1919",
                title: "Desarrollos Iniciales del Debate",
                description: "Primeras publicaciones sistemáticas de ambas escuelas.",
                details: "Weyl publica 'El Continuo' y Hilbert 'Pensamiento Axiomático'. Brouwer publica 'Teoría de Conjuntos Intuicionista', rechazando el Principio de Tercio Excluso como herramienta de demostración, afirmando que solo tiene valor heurístico.",
                author: "Weyl, Hilbert, Brouwer",
                category: "debate"
            },
            {
                date: "1921",
                title: "La 'Deserción' de Weyl",
                description: "Weyl publica 'Sobre la nueva Crisis de Fundamentos', defendiendo parcialmente a Brouwer.",
                details: "Hermann Weyl, alumno de Hilbert, causa sorpresa al publicar un artículo defendiendo (aunque no totalmente) las tesis de Brouwer. Hilbert considera esto una deserción. Weyl propone excluir el PTE solo de proposiciones existenciales y universales.",
                author: "Hermann Weyl",
                category: "debate"
            },
            {
                date: "1921",
                title: "¿Debe tener todo número real una expresión decimal?",
                description: "Brouwer responde negativamente, basándose en el conocimiento incompleto de π.",
                details: "En el Congreso de Científicos alemanes, Brouwer presenta su famoso argumento sobre los números reales y las expansiones decimales, utilizando π como ejemplo de nuestro conocimiento incompleto del desarrollo decimal.",
                author: "L.E.J. Brouwer",
                category: "debate"
            },
            {
                date: "1923",
                title: "Primer Contraejemplo contra el PTE",
                description: "Brouwer presenta el contraejemplo contra la ley de tricotomía.",
                details: "En los congresos de Amberes y Marburgo, Brouwer presenta su primer contraejemplo formal contra el Principio de Tercio Excluso, violando la ley de tricotomía (para todo x, y: x < y ∨ x = y ∨ x > y) mediante una construcción basada en la secuencia de π.",
                author: "L.E.J. Brouwer",
                category: "debate"
            },
            {
                date: "1925",
                title: "'Sobre el Infinito' - Respuesta de Hilbert",
                description: "Hilbert introduce proposiciones ideales para mantener las leyes de la lógica clásica.",
                details: "Hilbert publica su respuesta fundamental, proponiendo la introducción de 'proposiciones ideales' para salvar las leyes aristotélicas, similar a como √-1 salvó las leyes del álgebra. Introduce axiomas transfinitos derivables del axioma de elección.",
                author: "David Hilbert",
                category: "debate"
            },
            {
                date: "1927",
                title: "Contraejemplo 'Fuerte' de Brouwer",
                description: "Brouwer demuestra propiedades especiales del continuo intuicionista.",
                details: "En 'Sobre los dominios de definición de las funciones', Brouwer demuestra que toda función completa es uniformemente continua y que no es posible separar el continuo en dos subconjuntos disjuntos no vacíos. Establece la teoría intuicionista del continuo.",
                author: "L.E.J. Brouwer",
                category: "debate"
            },
            {
                date: "1927",
                title: "Ataque Final de Hilbert",
                description: "Hilbert compara quitar el PTE con 'prohibir el telescopio al astrónomo'.",
                details: "En 'Los Fundamentos de las Matemáticas', Hilbert hace su ataque más duro: 'Quitarle el Principio de Tercio Excluso al matemático es lo mismo que prohibirle al astrónomo el telescopio o al boxeador usar sus puños'. Incluye un argumento ad hominem contra Brouwer.",
                author: "David Hilbert",
                category: "debate"
            },
            {
                date: "1928",
                title: "Expulsión de Brouwer y 'Guerra de Sapos y Ratones'",
                description: "Hilbert expulsa a Brouwer del consejo editorial de Mathematische Annalen.",
                details: "El debate trasciende lo académico. Hilbert, mediante una maniobra poco limpia, disuelve el consejo editorial completo de Mathematische Annalen para reconstituirlo sin Brouwer. Einstein lo califica como 'guerra de sapos y ratones' y renuncia junto con Carathéodory.",
                author: "David Hilbert vs L.E.J. Brouwer",
                category: "debate"
            },
            {
                date: "1931",
                title: "Teoremas de Incompletitud de Gödel",
                description: "Gödel demuestra la imposibilidad del programa formalista de Hilbert.",
                details: "Kurt Gödel publica sus teoremas de incompletitud, demostrando que es imposible demostrar la consistencia de un sistema axiomático dentro del propio sistema. Esto representa un golpe mortal al programa formalista de Hilbert, aunque abre nuevos desarrollos en teoría de la demostración.",
                author: "Kurt Gödel",
                category: "resolution"
            },
            {
                date: "1930s-presente",
                title: "Formalización del Intuicionismo",
                description: "El intuicionismo se desarrolla como sistema lógico formal paradójicamente.",
                details: "Bajo el liderazgo de Heyting y sus discípulos, el intuicionismo entra en una dinámica 'formalista', estableciendo nuevos sistemas lógicos y conectando con lógicas no clásicas y polivalentes. Sin embargo, no ha tenido influencias decisivas en desarrollos matemáticos recientes.",
                author: "Arend Heyting y seguidores",
                category: "resolution"
            }
        ];

        let currentFilter = 'all';

        function renderTimeline() {
            const timeline = document.getElementById('timeline');
            timeline.innerHTML = '';

            const filteredEvents = currentFilter === 'all' 
                ? events 
                : events.filter(event => event.category === currentFilter);

            filteredEvents.forEach((event, index) => {
                const timelineItem = document.createElement('div');
                timelineItem.className = 'timeline-item';
                timelineItem.style.display = 'flex';

                timelineItem.innerHTML = `
                    <div class="event-card ${event.category}" onclick="openModal('${index}')">
                        <div class="date">${event.date}</div>
                        <div class="title">${event.title}</div>
                        <div class="description">${event.description}</div>
                        <div class="author">${event.author}</div>
                    </div>
                    <div class="timeline-dot"></div>
                `;

                timeline.appendChild(timelineItem);
            });
        }

        function filterEvents(category) {
            currentFilter = category;
            
            // Update active button
            document.querySelectorAll('.filter-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            event.target.classList.add('active');

            renderTimeline();
        }

        function openModal(index) {
            const modal = document.getElementById('eventModal');
            const modalContent = document.getElementById('modalContent');
            
            const filteredEvents = currentFilter === 'all' 
                ? events 
                : events.filter(event => event.category === currentFilter);
            
            const event = filteredEvents[index];

            modalContent.innerHTML = `
                <h2 style="color: #2c3e50; margin-bottom: 20px;">${event.title}</h2>
                <p style="font-size: 1.2rem; color: #3498db; font-weight: bold; margin-bottom: 15px;">${event.date}</p>
                <p style="color: #34495e; line-height: 1.6; margin-bottom: 20px;">${event.details}</p>
                <p style="color: #7f8c8d; font-style: italic;">— ${event.author}</p>
            `;

            modal.style.display = 'block';
        }

        // Modal close functionality
        document.querySelector('.close').onclick = function() {
            document.getElementById('eventModal').style.display = 'none';
        }

        window.onclick = function(event) {
            const modal = document.getElementById('eventModal');
            if (event.target === modal) {
                modal.style.display = 'none';
            }
        }

        // Initialize timeline
        renderTimeline();
    </script>
</body>
</html>
