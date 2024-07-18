<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Visualización de Hoja de Cálculo de Google</title>
    <style>
        html, body {
            margin: 0;
            padding: 0;
            height: 100%;
            width: 100%;
            overflow: hidden;
        }
        body {
            display: flex;
            flex-direction: column;
        }
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
            background-color: #f0f0f0;
        }
        iframe {
            flex-grow: 1;
            border: none;
            width: 100%;
            height: calc(100% - 60px); /* Ajusta esto según la altura de tu header */
        }
        #cerrarSesion {
            padding: 10px 20px;
            background-color: #ff4444;
            color: white;
            border: none;
            cursor: pointer;
            border-radius: 5px;
        }
        #mensajeCierre {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0,0,0,0.8);
            color: white;
            font-size: 24px;
            justify-content: center;
            align-items: center;
            z-index: 1000;
            flex-direction: column;
        }
        #mensajeCierre button {
            margin-top: 20px;
            padding: 10px 20px;
            font-size: 18px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="header">
        <h1>GENERAR CERTIFICADO</h1>
        <button id="cerrarSesion" onclick="cerrarSesion()">Cerrar Sesión</button>
    </div>
    <iframe src="https://docs.google.com/spreadsheets/d/17p2V461HVNK8kcA1LjcbNxl4mjcV75unk9WfLie6z4E/edit?gid=1971938965#gid=1971938965&amp;widget=true&amp;headers=false"></iframe>
    <div id="mensajeCierre">
        <p>Se ha cerrado la sesión.</p>
        <p>Por favor, cierre esta ventana manualmente.</p>
        <button onclick="redirigirAInicio()">Ir a la página de inicio</button>
    </div>

    <script>
        // El script permanece sin cambios
        history.replaceState(null, '', 'logged_in');

        function cerrarSesion() {
            sessionStorage.setItem('sesionCerrada', 'true');
            document.getElementById('mensajeCierre').style.display = 'flex';
            document.body.style.pointerEvents = 'none';
            document.getElementById('mensajeCierre').style.pointerEvents = 'auto';
        }

        function redirigirAInicio() {
            window.location.href = "https://www.ccrindustrial.com.co/";
        }

        window.onload = function() {
            if (sessionStorage.getItem('sesionCerrada') === 'true') {
                cerrarSesion();
            }
        }

        window.addEventListener('popstate', function(event) {
            if (sessionStorage.getItem('sesionCerrada') === 'true') {
                cerrarSesion();
            } else {
                history.pushState(null, '', 'logged_in');
            }
        });
    </script>
</body>
</html>
