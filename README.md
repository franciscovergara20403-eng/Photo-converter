# Photo-converter
A dedícate web to convert images into jpg png webp and more!
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Convertidor de Imágenes Online Gratis</title>
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Conversor de Imágenes PNG y JPG</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #ff9a9e, #fecfef, #fad0c4); /* Colores cálidos: rosas y naranjas suaves */
            color: #333;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            min-height: 100vh;
            animation: fadeIn 1s ease-in-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        h1 {
            font-size: 2.5em;
            margin-bottom: 20px;
            text-shadow: 2px 2px 4px rgba(0,0,0,0.1);
            color: #d2691e; /* Marrón cálido */
        }

        .container {
            background: rgba(255, 255, 255, 0.9);
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
            max-width: 500px;
            width: 90%;
            text-align: center;
            transition: transform 0.3s ease;
        }

        .container:hover {
            transform: scale(1.02);
        }

        input[type="file"] {
            margin: 20px 0;
            padding: 10px;
            border: 2px dashed #ff7f50; /* Coral */
            border-radius: 10px;
            background: #fff8dc; /* Crema */
            cursor: pointer;
            transition: border-color 0.3s;
        }

        input[type="file"]:hover {
            border-color: #ffa500; /* Naranja */
        }

        button {
            background: linear-gradient(45deg, #ff6b6b, #ffa500);
            color: white;
            border: none;
            padding: 12px 25px;
            margin: 10px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 1em;
            transition: background 0.3s, transform 0.2s;
            box-shadow: 0 4px 15px rgba(0,0,0,0.2);
        }

        button:hover {
            background: linear-gradient(45deg, #ff5252, #ff8c00);
            transform: translateY(-2px);
        }

        button:active {
            transform: translateY(0);
        }

        .preview {
            margin-top: 20px;
            max-width: 100%;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }

        .message {
            margin-top: 20px;
            font-weight: bold;
            color: #32cd32; /* Verde para éxito */
            animation: bounce 0.5s;
        }

        @keyframes bounce {
            0%, 20%, 50%, 80%, 100% { transform: translateY(0); }
            40% { transform: translateY(-10px); }
            60% { transform: translateY(-5px); }
        }

        footer {
            margin-top: 40px;
            font-size: 0.8em;
            color: #666;
            text-align: center;
        }

        /* Estilo moderno y juguetón */
        .fun-text {
            font-style: italic;
            color: #ff4500; /* Rojo anaranjado */
            margin-bottom: 10px;
        }
    </style>
</head>
<body>
    <h1>Conversor de Imágenes PNG y JPG</h1>
    <div class="container">
        <p class="fun-text">¡Sube tu imagen y conviértela en un instante! Todas las combinaciones posibles: PNG a JPG, JPG a PNG, y más diversión.</p>
        <input type="file" id="fileInput" accept="image/png,image/jpeg">
        <br>
        <button onclick="convertToJPG()">Convertir a JPG</button>
        <button onclick="convertToPNG()">Convertir a PNG</button>
        <div id="previewContainer" style="display: none;">
            <img id="preview" class="preview" alt="Vista previa">
        </div>
        <div id="message" class="message"></div>
    </div>
    <footer>
        Todos los derechos reservados. © 2023 Conversor de Imágenes. Diseñado para mantener la diversión.
    </footer>

    <script>
        let selectedFile = null;

        document.getElementById('fileInput').addEventListener('change', function(event) {
            selectedFile = event.target.files[0];
            if (selectedFile) {
                const reader = new FileReader();
                reader.onload = function(e) {
                    document.getElementById('preview').src = e.target.result;
                    document.getElementById('previewContainer').style.display = 'block';
                    document.getElementById('message').textContent = '¡Imagen cargada! Elige tu conversión.';
                };
                reader.readAsDataURL(selectedFile);
            }
        });

        function convertToJPG() {
            if (!selectedFile) {
                alert('Por favor, selecciona una imagen primero.');
                return;
            }
            convertImage('image/jpeg', 'converted.jpg');
        }

        function convertToPNG() {
            if (!selectedFile) {
                alert('Por favor, selecciona una imagen primero.');
                return;
            }
            convertImage('image/png', 'converted.png');
        }

        function convertImage(mimeType, filename) {
            const img = new Image();
            img.onload = function() {
                const canvas = document.createElement('canvas');
                const ctx = canvas.getContext('2d');
                canvas.width = img.width;
                canvas.height = img.height;
                ctx.drawImage(img, 0, 0);

                canvas.toBlob(function(blob) {
                    const url = URL.createObjectURL(blob);
                    const a = document.createElement('a');
                    a.href = url;
                    a.download = filename;
                    document.body.appendChild(a);
                    a.click();
                    document.body.removeChild(a);
                    URL.revokeObjectURL(url);
                    document.getElementById('message').textContent = '¡Conversión exitosa! Descarga completada. ¡Sigue jugando!';
                }, mimeType);
            };
            img.src = URL.createObjectURL(selectedFile);
        }
    </script>
</body>
</html>
