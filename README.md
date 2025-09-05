# epistemologias-matematicas
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Epistemologías de las Matemáticas - Organizador Gráfico</title>
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
            max-width: 1400px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(10px);
            overflow: hidden;
        }

        .header {
            background: linear-gradient(135deg, #2c3e50 0%, #3498db 100%);
            color: white;
            padding: 30px;
            text-align: center;
        }

        .header h1 {
            font-size: 2.2em;
            margin-bottom: 10px;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        }

        .header p {
            font-size: 1.1em;
            opacity: 0.9;
        }

        .controls {
            padding: 20px;
            background: rgba(52, 152, 219, 0.1);
            border-bottom: 1px solid rgba(52, 152, 219, 0.2);
            text-align: center;
        }

        .btn {
            background: linear-gradient(135deg, #3498db 0%, #2980b9 100%);
            color: white;
            border: none;
            padding: 12px 24px;
            margin: 0 10px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 14px;
            font-weight: 600;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(52, 152, 219, 0.3);
        }

        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(52, 152, 219, 0.4);
        }

        .btn.active {
            background: linear-gradient(135deg, #e74c3c 0%, #c0392b 100%);
            box-shadow: 0 4px 15px rgba(231, 76, 60, 0.3);
        }

        .visualization-area {
            position: relative;
            height: 900px;
            overflow: hidden;
            background: radial-gradient(circle at center, rgba(255, 255, 255, 0.1) 0%, transparent 70%);
        }

        .central-concept {
            position: absolute;
            width: 320px;
            height: 160px;
            background: linear-gradient(135deg, #2c3e50 0%, #34495e 100%);
            color: white;
            border-radius: 20px;
            padding: 30px;
            cursor: pointer;
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            box-shadow: 0 15px 40px rgba(44, 62, 80, 0.3);
            backdrop-filter: blur(10px);
            z-index: 50;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            border: 4px solid #f39c12;
        }

        .central-concept:hover {
            transform: scale(1.05);
            box-shadow: 0 20px 50px rgba(44, 62, 80, 0.4);
        }

        .central-title {
            font-weight: 700;
            font-size: 18px;
            line-height: 1.3;
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
        }

        .concept-node {
            position: absolute;
            min-width: 220px;
            max-width: 260px;
            background: linear-gradient(135deg, #ffffff 0%, #f8f9fa 100%);
            border: 3px solid;
            border-radius: 15px;
            padding: 20px;
            cursor: pointer;
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(10px);
            z-index: 10;
        }

        .concept-node:hover {
            transform: scale(1.08) translateY(-5px);
            box-shadow: 0 15px 40px rgba(0, 0, 0, 0.2);
            z-index: 20;
        }

        .concept-node.selected {
            transform: scale(1.1);
            box-shadow: 0 20px 50px rgba(0, 0, 0, 0.3);
            z-index: 30;
        }

        .concept-title {
            font-weight: 700;
            font-size: 16px;
            margin-bottom: 12px;
            line-height: 1.3;
        }

        .concept-description {
            font-size: 13px;
            line-height: 1.5;
            color: #555;
            opacity: 0;
            max-height: 0;
            transition: all 0.4s ease;
            overflow: hidden;
        }

        .concept-node:hover .concept-description,
        .concept-node.selected .concept-description {
            opacity: 1;
            max-height: 200px;
            margin-top: 12px;
        }

        .connection-arrow {
            position: absolute;
            z-index: 5;
            pointer-events: none;
        }

        .arrow-line {
            background: linear-gradient(45deg, #3498db, #9b59b6);
            height: 3px;
            transform-origin: left center;
            opacity: 0.8;
            border-radius: 2px;
            transition: all 0.3s ease;
            position: relative;
        }

        .arrow-head {
            position: absolute;
            right: -8px;
            top: -6px;
            width: 0;
            height: 0;
            border-left: 12px solid #9b59b6;
            border-top: 6px solid transparent;
            border-bottom: 6px solid transparent;
        }

        .connection-arrow.active .arrow-line {
            height: 4px;
            opacity: 1;
            box-shadow: 0 0 10px rgba(52, 152, 219, 0.5);
        }

        .connection-arrow.active .arrow-head {
            border-left-color: #3498db;
            filter: drop-shadow(0 0 5px rgba(52, 152, 219, 0.5));
        }

        .legend {
            position: absolute;
            top: 20px;
            right: 20px;
            background: rgba(255, 255, 255, 0.9);
            padding: 15px;
            border-radius: 10px;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(10px);
            min-width: 200px;
        }

        .legend h3 {
            margin-bottom: 10px;
            color: #2c3e50;
            font-size: 14px;
        }

        .legend-item {
            display: flex;
            align-items: center;
            margin-bottom: 8px;
            font-size: 12px;
        }

        .legend-color {
            width: 20px;
            height: 3px;
            margin-right: 8px;
            border-radius: 2px;
        }

        /* Colores para diferentes tipos de conceptos */
        .theoretical { border-color: #e74c3c; }
        .theoretical .concept-title { color: #e74c3c; }

        .methodological { border-color: #3498db; }
        .methodological .concept-title { color: #3498db; }

        .psychological { border-color: #9b59b6; }
        .psychological .concept-title { color: #9b59b6; }

        .pedagogical { border-color: #27ae60; }
        .pedagogical .concept-title { color: #27ae60; }

        .epistemological { border-color: #f39c12; }
        .epistemological .concept-title { color: #f39c12; }

        @keyframes fadeIn {
            from { opacity: 0; transform: scale(0.8); }
            to { opacity: 1; transform: scale(1); }
        }

        @keyframes pulse {
            0%, 100% { transform: scale(1); }
            50% { transform: scale(1.02); }
        }

        .concept-node, .central-concept {
            animation: fadeIn 0.8s ease-out;
        }

        .central-concept {
            animation: fadeIn 0.8s ease-out, pulse 3s ease-in-out infinite;
        }

        @media (max-width: 768px) {
            .header h1 { font-size: 1.6em; }
            .central-concept { width: 280px; height: 140px; padding: 20px; }
            .central-title { font-size: 16px; }
            .concept-node { min-width: 180px; max-width: 220px; padding: 15px; }
            .concept-title { font-size: 14px; }
            .concept-description { font-size: 12px; }
            .legend { position: relative; margin: 20px; }
            .visualization-area { height: 800px; }
        }

        .connection-label {
            position: absolute;
            background: rgba(255, 255, 255, 0.9);
            padding: 4px 8px;
            border-radius: 12px;
            font-size: 11px;
            font-weight: 600;
            color: #666;
            border: 1px solid rgba(0, 0, 0, 0.1);
            opacity: 0;
            transition: opacity 0.3s ease;
            z-index: 15;
            pointer-events: none;
        }

        .connection-arrow:hover .connection-label {
            opacity: 1;
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>Jhon Fredy Sánchez - Miguel Ángel Quintero</h1>
            <p>Epistemologías de las Matemáticas y de la Educación Matemática</p>
        </div>

        <div class="controls">
            <button class="btn" onclick="showAllConnections()">Mostrar Todas las Conexiones</button>
            <button class="btn" onclick="hideAllConnections()">Ocultar Conexiones</button>
            <button class="btn" onclick="animateConnections()">Animación Secuencial</button>
            <button class="btn" onclick="resetView()">Vista Inicial</button>
        </div>

        <div class="visualization-area" id="visualizationArea">
            <div class="legend">
                <h3>Tipos de Conceptos</h3>
                <div class="legend-item">
                    <div class="legend-color theoretical"></div>
                    <span>Teóricos</span>
                </div>
                <div class="legend-item">
                    <div class="legend-color methodological"></div>
                    <span>Metodológicos</span>
                </div>
                <div class="legend-item">
                    <div class="legend-color psychological"></div>
                    <span>Psicológicos</span>
                </div>
                <div class="legend-item">
                    <div class="legend-color pedagogical"></div>
                    <span>Pedagógicos</span>
                </div>
                <div class="legend-item">
                    <div class="legend-color epistemological"></div>
                    <span>Epistemológicos</span>
                </div>
            </div>
        </div>
    </div>

    <script>
        const concepts = [
            {
                id: 1,
                title: "Antropología del Conocimiento",
                description: "Disciplina que estudia cómo las diferentes culturas y contextos sociales influyen en la creación, transmisión y construcción del conocimiento humano.",
                type: "theoretical",
                angle: 0
            },
            {
                id: 2,
                title: "Contrato Didáctico",
                description: "Conjunto de comportamientos, expectativas y reglas implícitas y explícitas que regulan la relación entre el docente, el estudiante y el saber dentro de una situación de enseñanza.",
                type: "pedagogical",
                angle: 45
            },
            {
                id: 3,
                title: "Interaccionismo Social",
                description: "Enfoque que considera que las personas aprenden y dan sentido al mundo a través de las interacciones en las que participan desde que nacen, uniendo ideas cognitivas y humanistas.",
                type: "psychological",
                angle: 90
            },
            {
                id: 4,
                title: "Obstáculo Epistemológico",
                description: "Dificultad o confusión asentada en el proceso de producción de conocimiento científico, como la carencia de teorías que sitúen problemas en perspectiva totalizadora.",
                type: "epistemological",
                angle: 135
            },
            {
                id: 5,
                title: "Reconstrucción Racional",
                description: "Método filosófico y lingüístico que traduce sistemáticamente el conocimiento intuitivo de las reglas a una forma lógica, buscando poner significados adecuados en el lenguaje.",
                type: "methodological",
                angle: 180
            },
            {
                id: 6,
                title: "Situación Didáctica",
                description: "Modelo que busca que los alumnos descubran por sí mismos los métodos de resolución a través de la interacción con el problema.",
                type: "pedagogical",
                angle: 225
            },
            {
                id: 7,
                title: "Transposición Didáctica",
                description: "Proceso mediante el cual los conocimientos de una disciplina académica son transformados y adaptados para ser enseñados en un contexto educativo específico.",
                type: "methodological",
                angle: 270
            },
            {
                id: 8,
                title: "Zona de Desarrollo Próximo",
                description: "Concepto clave de Vygotsky que define el rango de tareas que un aprendiz puede realizar con ayuda de una persona más competente, pero no de manera independiente.",
                type: "psychological",
                angle: 315
            }
        ];

        let connectionsVisible = false;
        let selectedNode = null;

        function createCentralConcept() {
            const area = document.getElementById('visualizationArea');
            const centerX = area.clientWidth / 2 - 160; // 160 = width/2
            const centerY = area.clientHeight / 2 - 80;  // 80 = height/2

            const centralNode = document.createElement('div');
            centralNode.className = 'central-concept';
            centralNode.style.left = centerX + 'px';
            centralNode.style.top = centerY + 'px';
            centralNode.id = 'central-concept';

            centralNode.innerHTML = `
                <div class="central-title">Epistemologías de las Matemáticas y de la Educación Matemática</div>
            `;

            centralNode.addEventListener('click', () => {
                if (connectionsVisible) {
                    hideAllConnections();
                } else {
                    showAllConnections();
                }
            });

            return centralNode;
        }

        function createConceptNode(concept) {
            const area = document.getElementById('visualizationArea');
            const centerX = area.clientWidth / 2;
            const centerY = area.clientHeight / 2;
            const radius = 300;

            const angleRad = (concept.angle * Math.PI) / 180;
            const x = centerX + Math.cos(angleRad) * radius - 130; // 130 = approx width/2
            const y = centerY + Math.sin(angleRad) * radius - 75;  // 75 = approx height/2

            const node = document.createElement('div');
            node.className = `concept-node ${concept.type}`;
            node.style.left = Math.max(10, Math.min(area.clientWidth - 260, x)) + 'px';
            node.style.top = Math.max(10, Math.min(area.clientHeight - 150, y)) + 'px';
            node.dataset.conceptId = concept.id;
            node.dataset.angle = concept.angle;

            node.innerHTML = `
                <div class="concept-title">${concept.title}</div>
                <div class="concept-description">${concept.description}</div>
            `;

            node.addEventListener('click', () => selectNode(concept.id));
            
            return node;
        }

        function createConnectionArrow(fromElement, toElement, label = '') {
            const fromRect = fromElement.getBoundingClientRect();
            const toRect = toElement.getBoundingClientRect();
            const containerRect = document.getElementById('visualizationArea').getBoundingClientRect();

            const fromX = fromRect.left + fromRect.width / 2 - containerRect.left;
            const fromY = fromRect.top + fromRect.height / 2 - containerRect.top;
            const toX = toRect.left + toRect.width / 2 - containerRect.left;
            const toY = toRect.top + toRect.height / 2 - containerRect.top;

            const length = Math.sqrt(Math.pow(toX - fromX, 2) + Math.pow(toY - fromY, 2)) - 20;
            const angle = Math.atan2(toY - fromY, toX - fromX) * 180 / Math.PI;

            const arrow = document.createElement('div');
            arrow.className = 'connection-arrow';
            arrow.style.left = fromX + 'px';
            arrow.style.top = fromY + 'px';

            const arrowLine = document.createElement('div');
            arrowLine.className = 'arrow-line';
            arrowLine.style.width = length + 'px';
            arrowLine.style.transform = `rotate(${angle}deg)`;

            const arrowHead = document.createElement('div');
            arrowHead.className = 'arrow-head';

            arrow.appendChild(arrowLine);
            arrow.appendChild(arrowHead);

            if (label) {
                const connectionLabel = document.createElement('div');
                connectionLabel.className = 'connection-label';
                connectionLabel.textContent = label;
                connectionLabel.style.left = (length / 2) + 'px';
                connectionLabel.style.top = '-20px';
                arrow.appendChild(connectionLabel);
            }

            return arrow;
        }

        function initializeVisualization() {
            const area = document.getElementById('visualizationArea');
            
            // Crear concepto central
            const centralConcept = createCentralConcept();
            area.appendChild(centralConcept);

            // Crear nodos de conceptos
            concepts.forEach(concept => {
                const node = createConceptNode(concept);
                area.appendChild(node);
            });

            // Mostrar conexiones iniciales después de un breve delay
            setTimeout(() => {
                showAllConnections();
            }, 1000);
        }

        function selectNode(conceptId) {
            // Remover selección anterior
            document.querySelectorAll('.concept-node').forEach(node => {
                node.classList.remove('selected');
            });

            // Seleccionar nuevo nodo
            const selectedNodeElement = document.querySelector(`[data-concept-id="${conceptId}"]`);
            if (selectedNodeElement) {
                selectedNodeElement.classList.add('selected');
                selectedNode = conceptId;
                showSingleConnection(conceptId);
            }
        }

        function showSingleConnection(conceptId) {
            clearConnections();
            const fromNode = document.querySelector(`[data-concept-id="${conceptId}"]`);
            const toNode = document.getElementById('central-concept');
            
            if (fromNode && toNode) {
                const concept = concepts.find(c => c.id === conceptId);
                const arrow = createConnectionArrow(fromNode, toNode, concept.title);
                arrow.classList.add('active');
                document.getElementById('visualizationArea').appendChild(arrow);
            }
        }

        function showAllConnections() {
            clearConnections();
            connectionsVisible = true;
            
            const centralNode = document.getElementById('central-concept');
            
            concepts.forEach(concept => {
                const fromNode = document.querySelector(`[data-concept-id="${concept.id}"]`);
                if (fromNode && centralNode) {
                    const arrow = createConnectionArrow(fromNode, centralNode);
                    arrow.classList.add('active');
                    document.getElementById('visualizationArea').appendChild(arrow);
                }
            });
        }

        function hideAllConnections() {
            clearConnections();
            connectionsVisible = false;
        }

        function animateConnections() {
            clearConnections();
            const centralNode = document.getElementById('central-concept');
            
            concepts.forEach((concept, index) => {
                setTimeout(() => {
                    const fromNode = document.querySelector(`[data-concept-id="${concept.id}"]`);
                    if (fromNode && centralNode) {
                        const arrow = createConnectionArrow(fromNode, centralNode);
                        arrow.classList.add('active');
                        arrow.style.opacity = '0';
                        arrow.style.transition = 'opacity 0.5s ease';
                        document.getElementById('visualizationArea').appendChild(arrow);
                        
                        setTimeout(() => {
                            arrow.style.opacity = '1';
                        }, 50);
                    }
                }, index * 300);
            });
            
            connectionsVisible = true;
        }

        function clearConnections() {
            document.querySelectorAll('.connection-arrow').forEach(arrow => arrow.remove());
        }

        function resetView() {
            selectedNode = null;
            document.querySelectorAll('.concept-node').forEach(node => {
                node.classList.remove('selected');
            });
            clearConnections();
            setTimeout(() => showAllConnections(), 500);
        }

        // Inicializar la visualización
        document.addEventListener('DOMContentLoaded', initializeVisualization);

        // Actualizar posiciones y conexiones cuando se redimensiona la ventana
        window.addEventListener('resize', () => {
            // Limpiar y recrear
            document.querySelectorAll('.concept-node, .central-concept, .connection-arrow').forEach(el => el.remove());
            setTimeout(initializeVisualization, 100);
        });
    </script>
</body>
</html>
