# Photo-converter
A dedícate web to convert images into jpg png webp and more!
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Convertidor de Imágenes Online Gratis</title>

    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background: linear-gradient(45deg, #667eea, #764ba2, #f093fb, #f5576c);
            background-size: 400% 400%;
            animation: gradientShift 10s ease infinite;
            color: white;
            display: flex;
            flex-direction: column;
            align-items: center;
            min-height: 100vh;
            text-align: center;
        }

        @keyframes gradientShift {
            0% { background-position: 0% 50%; }
            50% { background-position: 100% 50%; }
            100% { background-position: 0% 50%; }
        }

        h1 {
            margin-top: 30px;
            font-size: 2.5em;
        }

        .ad-placeholder {
            width: 100%;
            max-width: 728px;
            height: 90px;
            background: rgba(255,255,255,0.15);
            border-radius: 10px;
            margin: 20px 0;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 0.9em;
            opacity: 0.7;
        }

        .container {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 8px 32px rgba(0,0,0,0.3);
            max-width: 600px;
            width: 90%;
        }

        input[type="file"] {
            margin: 20px 0;
            padding: 10px;
            border-radius: 10px;
        }

        button {
            background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
            border: none;
            color: white;
            padding: 12px 25px;
            margin: 6px;
            border-radius: 25px;
            font-size: 1em;
            cursor: pointer;
        }

        #preview {
            max-width: 100%;
            max-height: 300px;
            margin: 20px 0;
            border-radius: 10px;
        }

        .seo-text {
            max-width: 600px;
            margin-top: 30px;
            background: rgba(0,0,0,0.2);
            padding: 20px;
            border-radius: 15px;
            text-align: left;
        }

        footer {
            margin: 40px 0 20px;
            font-size: 0.9em;
        }

        footer a {
            color: white;
            margin: 0 5px;
            text-decoration: underline;
        }
    </style>
</head>

<body>

    <!-- AD TOP -->
    <div class="ad-placeholder">
        Espacio para anuncio
    </div>

    <h1>Convertidor de Imágenes Online</h1>

    <div class="container">
        <p>Sube una imagen y conviértela a otro formato gratis.</p>

        <input type="file" id="imageInput" accept="image/*">

        <img id="preview" style="display:none;" alt="Vista previa">

        <div>
            <button onclick="convertTo('png')">PNG</button>
            <button onclick="convertTo('jpg')">JPG</button>
            <button onclick="convertTo('webp')">WEBP</button>
            <button onclick="convertTo('bmp')">BMP</button>
            <button onclick="convertTo('gif')">GIF</button>
        </div>

        <div id="status"></div>
    </div>

    <!-- SEO TEXT -->
    <section class="seo-text">
        <h2>Convierte Imágenes Gratis y Sin Registro</h2>
        <p>
            Este convertidor de imágenes online te permite cambiar el formato de tus archivos
            JPG, PNG, WEBP, BMP y GIF de forma rápida y gratuita.
        </p>
        <p>
            Todo el proceso se realiza directamente en tu navegador, sin subir archivos a servidores,
            garantizando privacidad y velocidad.
        </p>
    </section>

    <!-- AD BOTTOM -->
    <div class="ad-placeholder">
        Espacio para anuncio
    </div>

    <!-- FOOTER -->
    <footer>
        <a href="privacy.html">Política de Privacidad</a> |
        <a href="terms.html">Términos</a> |
        <a href="contact.html">Contacto</a>
    </footer>

    <script>
        let imageFile = null;

        document.getElementById('imageInput').addEventListener('change', function(e) {
            imageFile = e.target.files[0];
            if (!imageFile) return;

            const reader = new FileReader();
            reader.onload = function(ev) {
                const img = document.getElementById('preview');
                img.src = ev.target.result;
                img.style.display = 'block';
                document.getElementById('status').textContent = 'Imagen cargada';
            };
            reader.readAsDataURL(imageFile);
        });

        function convertTo(format) {
            if (!imageFile) {
                document.getElementById('status').textContent = 'Sube una imagen primero';
                return;
            }

            const canvas = document.createElement('canvas');
            const ctx = canvas.getContext('2d');
            const img = new Image();

            img.onload = function() {
                canvas.width = img.width;
                canvas.height = img.height;
                ctx.drawImage(img, 0, 0);

                canvas.toBlob(function(blob) {
                    const link = document.createElement('a');
                    link.href = URL.createObjectURL(blob);
                    link.download = `imagen.${format}`;
                    link.click();
                }, `image/${format}`);
            };

            img.src = URL.createObjectURL(imageFile);
        }
    </script>

</body>
</html>
