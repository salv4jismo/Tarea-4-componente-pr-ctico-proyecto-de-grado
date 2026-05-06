# Tarea-4-componente practico-proyecto de grado
Código de la actividad presentada sobre el proyecto seleccionado y desarrollado 

<!-- 
    EQUIPO DE DESARROLLO - LogiTrack
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
    <title>LogiTrack - Aplicación de Seguimiento </title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #1e3c72 0%, #2a5298 100%);
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
            color: #1e3c72;
            border-bottom: 3px solid #1e3c72;
            padding-bottom: 10px;
            margin-bottom: 20px;
            font-size: 1.8rem;
        }

        .section h3 {
            color: #2a5298;
            margin: 15px 0 10px 0;
            font-size: 1.3rem;
        }

        /* Grid de imágenes */
        .gallery-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
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
            height: 180px;
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
            font-size: 0.95rem;
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
            margin: 10px;
            font-size: 0.8rem;
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
        <h1>🚛 LogiTrack - Rutas Seguimiento y pymes</h1>
        
        <div class="info-banner">
            💡 <strong>Consejo:</strong> Haz clic en cualquier imagen para verla en tamaño completo. 
            Asegúrate de que las imágenes estén en la carpeta <strong>"Imagenes"</strong> (en el mismo lugar que este archivo HTML).
        </div>

        <div class="section">
            <h2>🔐 Autenticación y Dashboard</h2>
            <div class="gallery-grid" id="auth-grid"></div>
        </div>

        <div class="section">
            <h2>🚛 Gestión de Flota</h2>
            <div class="gallery-grid" id="flota-grid"></div>
        </div>

        <div class="section">
            <h2>🗺️ Rutas y Seguimiento</h2>
            <div class="gallery-grid" id="rutas-grid"></div>
        </div>

        <div class="section">
            <h2>📊 Reportes</h2>
            <div class="gallery-grid" id="reportes-grid"></div>
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
        const images = [
            // Autenticación y Dashboard
            { src: "Imagenes/login.png", alt: "Pantalla de Login", section: "auth", displayName: "🔐 Login", category: "Autenticación" },
            { src: "Imagenes/dashboard.png", alt: "Dashboard Principal", section: "auth", displayName: "📊 Dashboard", category: "Dashboard" },
            
            // Gestión de Flota - Vehículos y Conductores
            { src: "Imagenes/gestion-vehiculo.png", alt: "Gestión de Vehículos", section: "flota", displayName: "🚛 Gestión de Vehículos", category: "Vehículos" },
            { src: "Imagenes/conductores.png", alt: "Gestión de Conductores", section: "flota", displayName: "👨‍✈️ Conductores", category: "Conductores" },
            
            // Rutas y Seguimiento
            { src: "Imagenes/rutas.png", alt: "Gestión de Rutas", section: "rutas", displayName: "🗺️ Rutas", category: "Rutas" },
            { src: "Imagenes/seguimiento.png", alt: "Seguimiento de Unidades", section: "rutas", displayName: "📍 Seguimiento", category: "Seguimiento" },
            
            // Reportes
            { src: "Imagenes/reportes.png", alt: "Generación de Reportes", section: "reportes", displayName: "📈 Reportes", category: "Reportes" }
        ];

        // Referencias a los grids
        const authGrid = document.getElementById('auth-grid');
        const flotaGrid = document.getElementById('flota-grid');
        const rutasGrid = document.getElementById('rutas-grid');
        const reportesGrid = document.getElementById('reportes-grid');

        // Modal elements
        const modal = document.getElementById('imageModal');
        const modalImg = document.getElementById('modalImage');
        const modalCaption = document.getElementById('modalCaption');
        const closeModal = document.querySelector('.close-modal');

        // Función para crear una tarjeta de imagen
        function createImageCard(imageData) {
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
                errorDiv.innerHTML = '⚠️ Imagen no encontrada<br><small>' + imageData.src + '</small>';
                preview.innerHTML = '';
                preview.appendChild(errorDiv);
                
                // Placeholder
                const placeholder = document.createElement('div');
                placeholder.style.cssText = 'display: flex; flex-direction: column; align-items: center; justify-content: center; height: 100%; color: #999; font-size: 40px;';
                placeholder.innerHTML = '🖼️<br><span style="font-size:12px">' + imageData.displayName + '</span>';
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
            
            modalImg.onerror = function() {
                modalCaption.textContent = title + ' (Imagen no encontrada: ' + src + ')';
                this.style.display = 'none';
                const errorDisplay = document.createElement('div');
                errorDisplay.style.cssText = 'color: white; text-align: center; padding: 20px; background: #333; border-radius: 10px;';
                errorDisplay.innerHTML = '⚠️ No se pudo cargar la imagen<br><small>' + src + '</small>';
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

        // Eventos del modal
        closeModal.addEventListener('click', closeModalHandler);
        modal.addEventListener('click', (e) => {
            if (e.target === modal) {
                closeModalHandler();
            }
        });

        document.addEventListener('keydown', (e) => {
            if (e.key === 'Escape' && modal.classList.contains('active')) {
                closeModalHandler();
            }
        });

        // Renderizar la galería
        function renderGallery() {
            authGrid.innerHTML = '';
            flotaGrid.innerHTML = '';
            rutasGrid.innerHTML = '';
            reportesGrid.innerHTML = '';
            
            images.forEach(img => {
                const card = createImageCard(img);
                switch(img.section) {
                    case 'auth':
                        authGrid.appendChild(card);
                        break;
                    case 'flota':
                        flotaGrid.appendChild(card);
                        break;
                    case 'rutas':
                        rutasGrid.appendChild(card);
                        break;
                    case 'reportes':
                        reportesGrid.appendChild(card);
                        break;
                }
            });
        }
        
        // Inicializar
        renderGallery();
        
        console.log("🚛 LogicTrack - Galería iniciada");
        console.log("📁 Las imágenes deben estar en la carpeta: Imagenes/");
        console.log("📋 Imágenes esperadas: login.png, dashboard.png, gestion-vehiculo.png, conductores.png, rutas.png, seguimiento.png, reportes.png");
    </script>
</body>
</html>
