<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GENERADOR DE MENSAJE DE WHATSAPP DE CUENTAS</title>
    <style>
        body {
            font-family: sans-serif;
            margin: 20px;
        }
        .container {
            max-width: 600px;
            margin: 0 auto;
            text-align: center; /* Centrar el contenedor */
        }
        .header-container {
            display: flex;
            align-items: center;
            justify-content: center;
            margin-bottom: 10px;
        }
        .header-container img {
            max-height: 50px; /* Ajusta el tamaño de los logos */
            margin: 0 10px; /* Espacio entre los logos y el título */
        }
        h2 {
            margin-top: 0;
        }
        textarea {
            width: 100%;
            padding: 10px;
            margin-bottom: 10px;
            box-sizing: border-box;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        button {
            padding: 10px 20px;
            background-color: #25D366; /* Color verde de WhatsApp */
            color: white;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }
        button:hover {
            background-color: #128C7E; /* Verde más oscuro al pasar el mouse */
        }
        #mensaje-generado {
            white-space: pre-wrap; /* Respeta los saltos de línea */
            margin-top: 20px;
            padding: 15px;
            border: 1px solid #eee;
            border-radius: 4px;
            background-color: #f9f9f9;
            text-align: left; /* Alinear el texto del mensaje a la izquierda */
        }
        #frase-motivacional {
            margin-top: 15px;
            font-style: italic;
            color: #555;
            text-align: center; /* Centrar la frase motivacional */
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header-container">
            <img src="https://www.vendeygana.net/assets/img/logo-1.png" alt="Logo Vende y Gana">
            <h2>GENERADOR DE MENSAJE DE WHATSAPP DE CUENTAS</h2>
            <img src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/6b/WhatsApp.svg/2044px-WhatsApp.svg.png" alt="Logo WhatsApp">
        </div>
        <textarea id="datos-cuenta" rows="5" placeholder="DATOS DE SU PANTALLA NETFLIX: CORREO: angiangan17@gcatower.com CLAVE: g1902492 Perfil: 1 PIN: 2064"></textarea>
        <button onclick="generarMensaje()">Generar y Copiar Mensaje</button>
        <div id="mensaje-generado" style="display: none;"></div>
        <div id="frase-motivacional" style="display: none;"></div>
    </div>

    <script>
        const frasesMotivacionales = [
            "El éxito es la suma de pequeños esfuerzos repetidos día tras día.",
            "Cree en ti mismo y en todo lo que eres. Reconoce que hay algo dentro de ti que es más grande que cualquier obstáculo.",
            "No esperes por el momento perfecto, toma el momento y hazlo perfecto.",
            "El único modo de hacer un gran trabajo es amar lo que haces.",
            "Hoy es una nueva oportunidad para alcanzar tus metas. ¡A por ella!",
            "La perseverancia puede transformar el fracaso en un logro extraordinario.",
            "Tu actitud determina tu dirección.",
            "Cada día es un paso hacia tus sueños.",
            "La motivación te impulsa a comenzar, el hábito te permite continuar.",
            "Las oportunidades no ocurren, se crean."
        ];

        function obtenerFraseAleatoria() {
            const indice = Math.floor(Math.random() * frasesMotivacionales.length);
            return frasesMotivacionales[indice];
        }

        function generarMensaje() {
            const datosCuentaTextarea = document.getElementById("datos-cuenta");
            const mensajeGeneradoDiv = document.getElementById("mensaje-generado");
            const fraseMotivacionalDiv = document.getElementById("frase-motivacional");
            const datosCuenta = datosCuentaTextarea.value.trim();

            if (!datosCuenta) {
                alert("Por favor, ingresa los datos de la cuenta.");
                return;
            }

            const lineas = datosCuenta.split(':').map(linea => linea.trim());
            const servicio = lineas[0].split(' ')[4] || "SERVICIO"; // Extrae el servicio
            const correo = lineas[1];
            const clave = lineas[3];
            const perfil = lineas[5];
            const pin = lineas[7];

            const fechaEntrega = new Date();
            const opcionesFecha = { year: 'numeric', month: 'long', day: 'numeric' };
            const fechaEntregaFormateada = fechaEntrega.toLocaleDateString('es-VE', opcionesFecha);

            const proximaRenovacion = new Date();
            proximaRenovacion.setDate(proximaRenovacion.getDate() + 30); // Suponiendo renovación mensual
            const proximaRenovacionFormateada = proximaRenovacion.toLocaleDateString('es-VE', opcionesFecha);
            const diaProximaRenovacion = proximaRenovacion.getDate();
            const mesProximaRenovacion = proximaRenovacion.toLocaleDateString('es-VE', { month: 'long' });
            const añoProximaRenovacion = proximaRenovacion.toLocaleDateString('es-VE', { year: 'numeric' });
            const proximaRenovacionFinal = `${diaProximaRenovacion} de ${mesProximaRenovacion} de ${añoProximaRenovacion}`;

            const mensaje = `*📺 DATOS DE SU PANTALLA ${servicio.toUpperCase()} 📺*\n\n` +
                            `📧 *Correo:* ${correo}\n` +
                            `🔑 *Clave:* ${clave}\n` +
                            `👤 *Perfil activo:* ${perfil}\n` +
                            `🔢 *PIN de seguridad:* ${pin}\n\n` +
                            `📅 *Fecha de entrega:* Hoy, ${fechaEntregaFormateada}\n` +
                            `🔄 *Próxima renovación:* ${proximaRenovacionFinal}\n\n` +
                            `⚠️ *¡ ATENCIÓN!*\n` +
                            `❌ *Solo 1 dispositivo activo a la vez* (si se usa en más, la cuenta se bloquea).\n\n` +
                            `💰 *¡Vende y gana*\n` +
                            `🙌 Gracias por confiar en nosotros. ¡Disfruta tu ${servicio}!`;

            const fraseMotivacional = obtenerFraseAleatoria();

            mensajeGeneradoDiv.textContent = mensaje;
            mensajeGeneradoDiv.style.display = "block";
            fraseMotivacionalDiv.textContent = fraseMotivacional;
            fraseMotivacionalDiv.style.display = "block";

            // Copiar al portapapeles (incluyendo la frase motivacional)
            const mensajeCompleto = mensaje + "\n\n" + fraseMotivacional;
            navigator.clipboard.writeText(mensajeCompleto).then(() => {
                alert("¡Mensaje con ambos logos y frase copiado al portapapeles!");
            }).catch(err => {
                console.error('Error al copiar al portapapeles: ', err);
                alert("No se pudo copiar el mensaje al portapapeles. Por favor, selecciónalo y cópialo manualmente.");
            });
        }
    </script>
</body>
</html>
