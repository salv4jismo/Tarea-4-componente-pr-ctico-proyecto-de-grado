# Tarea-4-componente-pr-ctico-proyecto-de-grado
Código de la actividad presentada sobre el proyecto seleccionado y desarrollado 

<!-- 
    EQUIPO DE DESARROLLO - MATHEMA
    Integrantes:
    - Sergio Andres Aponte 
    - Yohan Sebastian Gaitan
    - David Cifuentes
-->
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Mathema - Galería Interactiva</title>
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
        }

        h1 {
            text-align: center;
            color: white;
            margin-bottom: 30px;
            font-size: 2.5rem;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
        }

        /* Secciones */
        .section {
            background: rgba(255,255,255,0.95);
            border-radius: 20px;
            padding: 25px;
            margin-bottom: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }

        .section h2 {
            color: #667eea;
            border-bottom: 3px solid #667eea;
            padding-bottom: 10px;
            margin-bottom: 20px;
            font-size: 1.8rem;
        }

        .section h3 {
            color: #764ba2;
            margin: 15px 0 10px 0;
            font-size: 1.3rem;
        }

        /* Grid de imágenes */
        .gallery-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
            gap: 20px;
            margin-top: 15px;
        }

        /* Tarjeta de imagen */
        .image-card {
            background: #f8f9fa;
            border-radius: 12px;
            overflow: hidden;
            cursor: pointer;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            box-shadow: 0 2px 8px rgba(0,0,0,0.1);
        }

        .image-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 8px 25px rgba(0,0,0,0.15);
        }

        .image-preview {
            width: 100%;
            height: 150px;
            background-color: #e9ecef;
            display: flex;
            align-items: center;
            justify-content: center;
            position: relative;
            overflow: hidden;
        }

        .image-preview img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            transition: transform 0.3s ease;
        }

        .image-card:hover .image-preview img {
            transform: scale(1.05);
        }

        .no-image {
            color: #adb5bd;
            font-size: 14px;
            text-align: center;
        }

        .image-title {
            padding: 12px;
            text-align: center;
            font-weight: 500;
            color: #495057;
            background: white;
            font-size: 0.9rem;
            border-top: 1px solid #e9ecef;
        }

        /* Modal para imagen grande */
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.9);
            cursor: pointer;
            justify-content: center;
            align-items: center;
        }

        .modal.active {
            display: flex;
        }

        .modal-content {
            max-width: 90%;
            max-height: 90%;
            object-fit: contain;
            border-radius: 8px;
            box-shadow: 0 0 30px rgba(0,0,0,0.5);
        }

        .close-modal {
            position: absolute;
            top: 20px;
            right: 35px;
            color: #f1f1f1;
            font-size: 40px;
            font-weight: bold;
            transition: 0.3s;
            cursor: pointer;
            z-index: 1001;
        }

        .close-modal:hover {
            color: #bbb;
        }

        .modal-caption {
            position: absolute;
            bottom: 20px;
            left: 0;
            right: 0;
            text-align: center;
            color: white;
            font-size: 1.2rem;
            background: rgba(0,0,0,0.7);
            padding: 10px;
            margin: 0 auto;
            width: fit-content;
            border-radius: 8px;
        }

        /* Mensaje de error */
        .error-message {
            background: #f8d7da;
            color: #721c24;
            padding: 10px;
            border-radius: 8px;
            text-align: center;
            margin: 10px 0;
            font-size: 0.85rem;
        }

        /* Mensaje de información */
        .info-banner {
            background: #d1ecf1;
            color: #0c5460;
            padding: 12px 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            text-align: center;
            font-size: 0.95rem;
        }

        @media (max-width: 768px) {
            .gallery-grid {
                grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
                gap: 12px;
            }
            
            h1 {
                font-size: 1.8rem;
            }
            
            .section h2 {
                font-size: 1.4rem;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>📚 Mathema - Galería de la Aplicación</h1>
        
        <div class="info-banner">
            💡 <strong>Consejo:</strong> Haz clic en cualquier imagen para verla en tamaño completo. 
            Asegúrate de que las imágenes estén en una carpeta llamada <strong>"Imagenes"</strong> (con mayúscula inicial).
        </div>

        <div class="section">
            <h2>🔐 Autenticación</h2>
            <div class="gallery-grid" id="auth-grid"></div>
        </div>

        <div class="section">
            <h2>📊 Usuario y Progreso</h2>
            <div class="gallery-grid" id="user-grid"></div>
        </div>

        <div class="section">
            <h2>📚 Módulos de Aprendizaje</h2>
            <div class="gallery-grid" id="modules-grid"></div>
        </div>

        <div class="section">
            <h2>✏️ Ejercicios</h2>
            <h3>Álgebra</h3>
            <div class="gallery-grid" id="algebra-grid"></div>
            
            <h3>Lógica y Respuestas</h3>
            <div class="gallery-grid" id="logic-grid"></div>
        </div>
    </div>

    <!-- Modal para imagen grande -->
    <div id="imageModal" class="modal">
        <span class="close-modal">&times;</span>
        <img class="modal-content" id="modalImage">
        <div id="modalCaption" class="modal-caption"></div>
    </div>

    <script>
        // Definición de todas las imágenes con sus rutas y nombres amigables
        const images = {
            // Autenticación
            login: { src: "Imagenes/login.png", alt: "Pantalla de Login", section: "auth", displayName: "🔐 Login" },
            login2: { src: "Imagenes/login2.png", alt: "Pantalla de Login Alternativa", section: "auth", displayName: "🔐 Login 2" },
            registro: { src: "Imagenes/registro.png", alt: "Pantalla de Registro", section: "auth", displayName: "📝 Registro" },
            registroDatos: { src: "Imagenes/registro-datos.png", alt: "Registro de Datos", section: "auth", displayName: "📋 Registro de Datos" },
            
            // Usuario y Progreso
            dashboard: { src: "Imagenes/dashboard.png", alt: "Dashboard Principal", section: "user", displayName: "📊 Dashboard" },
            progreso: { src: "Imagenes/progreso.png", alt: "Pantalla de Progreso", section: "user", displayName: "📈 Progreso" },
            
            // Módulos
            modulos: { src: "Imagenes/modulos.png", alt: "Módulos Disponibles", section: "modules", displayName: "📚 Módulos" },
            moduloAlgebra: { src: "Imagenes/modulo-algebra.png", alt: "Módulo de Álgebra", section: "modules", displayName: "🧮 Módulo - Álgebra" },
            moduloLogica: { src: "Imagenes/modulo-logica.png", alt: "Módulo de Lógica", section: "modules", displayName: "🧠 Módulo - Lógica" },
            
            // Ejercicios Álgebra
            ejerciciosAlgebra: { src: "Imagenes/ejercicios-algebra.png", alt: "Ejercicios de Álgebra", section: "algebra", displayName: "📝 Ejercicios - Álgebra" },
            ejerciciosAlgebra2: { src: "Imagenes/ejercicios-algebra2.png", alt: "Ejercicios de Álgebra 2", section: "algebra", displayName: "📝 Ejercicios - Álgebra 2" },
            
            // Lógica y Respuestas
            seleccionRespuesta: { src: "Imagenes/seleccion-respuesta.png", alt: "Selección de Respuesta", section: "logic", displayName: "✅ Selección de Respuesta" },
            respuestaCorrecta: { src: "Imagenes/respuesta-correcta.png", alt: "Respuesta Correcta", section: "logic", displayName: "✔️ Respuesta Correcta" },
            respuestaCorrecta2: { src: "Imagenes/respuesta-correcta.png", alt: "Respuesta Correcta", section: "logic", displayName: "✔️ Respuesta Correcta" },
            respuestaIncorrecta: { src: "Imagenes/respuesta-incorrecta.png", alt: "Respuesta Incorrecta", section: "logic", displayName: "❌ Respuesta Incorrecta" }
        };

        // Referencias a los grids
        const authGrid = document.getElementById('auth-grid');
        const userGrid = document.getElementById('user-grid');
        const modulesGrid = document.getElementById('modules-grid');
        const algebraGrid = document.getElementById('algebra-grid');
        const logicGrid = document.getElementById('logic-grid');

        // Modal elements
        const modal = document.getElementById('imageModal');
        const modalImg = document.getElementById('modalImage');
        const modalCaption = document.getElementById('modalCaption');
        const closeModal = document.querySelector('.close-modal');

        // Función para crear una tarjeta de imagen
        function createImageCard(imageKey, imageData) {
            const card = document.createElement('div');
            card.className = 'image-card';
            
            const preview = document.createElement('div');
            preview.className = 'image-preview';
            
            const img = document.createElement('img');
            img.src = imageData.src;
            img.alt = imageData.alt;
            img.loading = "lazy";
            
            // Manejar error de carga de imagen
            img.onerror = function() {
                this.onerror = null;
                this.style.display = 'none';
                const errorDiv = document.createElement('div');
                errorDiv.className = 'error-message';
                errorDiv.innerHTML = '⚠️ Imagen no encontrada<br><small>Verifica la ruta:<br>' + imageData.src + '</small>';
                preview.innerHTML = '';
                preview.appendChild(errorDiv);
                
                // También mostrar un placeholder
                const placeholder = document.createElement('div');
                placeholder.style.cssText = 'display: flex; flex-direction: column; align-items: center; justify-content: center; height: 100%; color: #999;';
                placeholder.innerHTML = '🖼️<br>Imagen faltante';
                preview.appendChild(placeholder);
            };
            
            preview.appendChild(img);
            
            const title = document.createElement('div');
            title.className = 'image-title';
            title.textContent = imageData.displayName;
            
            card.appendChild(preview);
            card.appendChild(title);
            
            // Evento click para abrir modal
            card.addEventListener('click', (e) => {
                e.stopPropagation();
                openModal(imageData.src, imageData.displayName);
            });
            
            return card;
        }

        // Función para abrir el modal
        function openModal(src, title) {
            modal.style.display = 'flex';
            modal.classList.add('active');
            modalImg.src = src;
            modalCaption.textContent = title;
            
            // Si la imagen falla al cargar en el modal, mostrar mensaje
            modalImg.onerror = function() {
                modalCaption.textContent = title + ' (Imagen no encontrada: ' + src + ')';
                this.style.display = 'none';
                // Crear un elemento de error visible
                const errorDisplay = document.createElement('div');
                errorDisplay.style.cssText = 'color: white; text-align: center; padding: 20px; background: #333; border-radius: 10px;';
                errorDisplay.innerHTML = '⚠️ No se pudo cargar la imagen<br><small>' + src + '</small><br><br>💡 Sugerencia: Crea una carpeta "Imagenes" y coloca las capturas allí con los nombres correctos.';
                if (!document.querySelector('.modal-error')) {
                    errorDisplay.className = 'modal-error';
                    modal.appendChild(errorDisplay);
                }
            };
            
            modalImg.onload = function() {
                this.style.display = 'block';
                const existingError = document.querySelector('.modal-error');
                if (existingError) existingError.remove();
            };
        }

        // Función para cerrar modal
        function closeModalHandler() {
            modal.style.display = 'none';
            modal.classList.remove('active');
            modalImg.src = '';
            const existingError = document.querySelector('.modal-error');
            if (existingError) existingError.remove();
        }

        // Cerrar modal al hacer clic fuera o en la X
        closeModal.addEventListener('click', closeModalHandler);
        modal.addEventListener('click', (e) => {
            if (e.target === modal) {
                closeModalHandler();
            }
        });

        // Presionar ESC para cerrar
        document.addEventListener('keydown', (e) => {
            if (e.key === 'Escape' && modal.classList.contains('active')) {
                closeModalHandler();
            }
        });

        // Organizar imágenes por sección y mostrarlas
        function renderGallery() {
            // Limpiar grids
            authGrid.innerHTML = '';
            userGrid.innerHTML = '';
            modulesGrid.innerHTML = '';
            algebraGrid.innerHTML = '';
            logicGrid.innerHTML = '';
            
            // Recorrer todas las imágenes y agregarlas a su grid correspondiente
            Object.entries(images).forEach(([key, img]) => {
                const card = createImageCard(key, img);
                switch(img.section) {
                    case 'auth':
                        authGrid.appendChild(card);
                        break;
                    case 'user':
                        userGrid.appendChild(card);
                        break;
                    case 'modules':
                        modulesGrid.appendChild(card);
                        break;
                    case 'algebra':
                        algebraGrid.appendChild(card);
                        break;
                    case 'logic':
                        logicGrid.appendChild(card);
                        break;
                    default:
                        // Si no tiene sección definida, va a autenticación por defecto
                        authGrid.appendChild(card);
                }
            });
            
            // Mostrar mensajes informativos si algunos grids están vacíos
            checkEmptyGrids();
        }
        
        function checkEmptyGrids() {
            const grids = [
                { element: authGrid, name: "Autenticación", path: "Imagenes/login.png" },
                { element: userGrid, name: "Usuario y Progreso", path: "Imagenes/dashboard.png" },
                { element: modulesGrid, name: "Módulos", path: "Imagenes/modulos.png" },
                { element: algebraGrid, name: "Ejercicios de Álgebra", path: "Imagenes/ejercicios-algebra.png" },
                { element: logicGrid, name: "Lógica y Respuestas", path: "Imagenes/seleccion-respuesta.png" }
            ];
            
            // No agregamos mensajes adicionales porque ya se maneja con los errors en cada tarjeta
        }
        
        // También podemos agregar una función para verificar si la carpeta Imagenes existe
        function checkImagesFolder() {
            console.log("📂 Verificando carpeta de imágenes...");
            console.log("ℹ️ Las imágenes deben estar en la carpeta: Imagenes/");
            console.log("📋 Nombres esperados:");
            Object.values(images).forEach(img => {
                console.log("   - " + img.src);
            });
        }
        
        // Inicializar la galería
        renderGallery();
        checkImagesFolder();
        
        // Añadir estilos adicionales para el modal
        const style = document.createElement('style');
        style.textContent = `
            .modal {
                display: none;
                position: fixed;
                z-index: 1000;
                left: 0;
                top: 0;
                width: 100%;
                height: 100%;
                background-color: rgba(0,0,0,0.9);
                justify-content: center;
                align-items: center;
            }
            .modal.active {
                display: flex !important;
            }
            .modal-content {
                max-width: 90%;
                max-height: 90%;
                object-fit: contain;
            }
            .modal-error {
                background: #721c24;
                color: white;
                padding: 20px;
                border-radius: 10px;
                text-align: center;
            }
        `;
        document.head.appendChild(style);
    </script>
</body>
</html>
