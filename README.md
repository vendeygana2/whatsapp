<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Generador de Mensajes para Cuentas</title>
    <style>
        :root {
            --primary-color: #25D366;
            --secondary-color: #128C7E;
            --dark-color: #075E54;
            --light-color: #DCF8C6;
            --text-color: #333;
            --bg-color: #f5f5f5;
        }
        
        * {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background-color: var(--bg-color);
            color: var(--text-color);
            line-height: 1.6;
            padding: 20px;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            padding: 25px;
            border-radius: 10px;
            box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
        }
        
        h1 {
            color: var(--dark-color);
            text-align: center;
            margin-bottom: 20px;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: var(--dark-color);
        }
        
        input, textarea, select {
            width: 100%;
            padding: 12px;
            border: 1px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
            transition: border 0.3s;
        }
        
        input:focus, textarea:focus, select:focus {
            border-color: var(--primary-color);
            outline: none;
        }
        
        textarea {
            min-height: 150px;
            resize: vertical;
        }
        
        .btn {
            display: inline-block;
            background-color: var(--primary-color);
            color: white;
            border: none;
            padding: 12px 20px;
            font-size: 16px;
            cursor: pointer;
            border-radius: 5px;
            transition: background-color 0.3s;
            text-align: center;
            margin-right: 10px;
            margin-bottom: 10px;
        }
        
        .btn:hover {
            background-color: var(--secondary-color);
        }
        
        .btn-whatsapp {
            background-color: var(--dark-color);
        }
        
        .btn-whatsapp:hover {
            background-color: var(--secondary-color);
        }
        
        .buttons-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            margin-top: 20px;
        }
        
        .result-container {
            margin-top: 30px;
            padding: 20px;
            background-color: var(--light-color);
            border-radius: 5px;
            border-left: 5px solid var(--primary-color);
            white-space: pre-line;
        }
        
        .result-title {
            color: var(--dark-color);
            margin-bottom: 15px;
            text-align: center;
        }
        
        @media (max-width: 600px) {
            .container {
                padding: 15px;
            }
            
            .btn {
                width: 100%;
                margin-right: 0;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Generador de Mensajes para Cuentas</h1>
        
        <div class="form-group">
            <label for="service">Servicio:</label>
            <select id="service">
                <option value="Netflix">Netflix</option>
                <option value="Amazon Prime">Amazon Prime</option>
                <option value="Disney+">Disney+</option>
                <option value="HBO Max">HBO Max</option>
                <option value="Spotify">Spotify</option>
                <option value="YouTube Premium">YouTube Premium</option>
                <option value="Otro">Otro</option>
            </select>
        </div>
        
        <div class="form-group" id="custom-service-group" style="display: none;">
            <label for="custom-service">Especificar servicio:</label>
            <input type="text" id="custom-service" placeholder="Escribe el nombre del servicio">
        </div>
        
        <div class="form-group">
            <label for="account-data">Datos de la cuenta (usuario y contraseña):</label>
            <textarea id="account-data" placeholder="Ejemplo: 
usuario: ejemplo@gmail.com 
contraseña: Clave1234"></textarea>
        </div>
        
        <div class="buttons-container">
            <button id="generate-btn" class="btn">Generar Mensaje</button>
        </div>
        
        <div class="result-container" id="result-container" style="display: none;">
            <h3 class="result-title">MENSAJE GENERADO</h3>
            <div id="generated-message"></div>
            <div class="buttons-container">
                <button id="copy-btn" class="btn">Copiar Mensaje</button>
                <button id="whatsapp-btn" class="btn btn-whatsapp">Compartir por WhatsApp</button>
            </div>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const serviceSelect = document.getElementById('service');
            const customServiceGroup = document.getElementById('custom-service-group');
            const customServiceInput = document.getElementById('custom-service');
            const accountDataInput = document.getElementById('account-data');
            const generateBtn = document.getElementById('generate-btn');
            const resultContainer = document.getElementById('result-container');
            const generatedMessage = document.getElementById('generated-message');
            const copyBtn = document.getElementById('copy-btn');
            const whatsappBtn = document.getElementById('whatsapp-btn');
            
            // Mostrar/ocultar campo para servicio personalizado
            serviceSelect.addEventListener('change', function() {
                if (this.value === 'Otro') {
                    customServiceGroup.style.display = 'block';
                } else {
                    customServiceGroup.style.display = 'none';
                }
            });
            
            // Generar el mensaje
            generateBtn.addEventListener('click', function() {
                if (!accountDataInput.value.trim()) {
                    alert('Por favor ingresa los datos de la cuenta');
                    return;
                }
                
                const service = serviceSelect.value === 'Otro' 
                    ? customServiceInput.value.trim() || 'Servicio no especificado'
                    : serviceSelect.value;
                
                const today = new Date();
                const deliveryDate = formatDate(today);
                
                const expirationDate = new Date(today);
                expirationDate.setDate(expirationDate.getDate() + 30);
                const expirationDateFormatted = formatDate(expirationDate);
                
                const message = `📋 *DATOS DE LA CUENTA* 📋\n\n` +
                                 `🔹 *Servicio:* ${getServiceEmoji(service)} ${service}\n\n` +
                                 `🔑 *Datos de acceso:*\n${formatAccountData(accountDataInput.value)}\n\n` +
                                 `📅 *Fechas importantes:*\n` +
                                 `   🚀 Entrega: ${deliveryDate}\n` +
                                 `   ⏳ Vencimiento: ${expirationDateFormatted}\n\n` +
                                 `⚠️ *Indicaciones importantes:*\n` +
                                 `   📱 Usar en un solo dispositivo o pierde la cuenta.\n` +
                                 `   🙏 Gracias por preferirnos.\n` +
                                 `   💰 Vende y gana.\n\n` +
                                 `🔒 Por seguridad, no compartas estos datos con terceros.`;
                
                generatedMessage.textContent = message;
                resultContainer.style.display = 'block';
                
                // Desplazarse al resultado
                resultContainer.scrollIntoView({ behavior: 'smooth' });
            });
            
            // Copiar mensaje al portapapeles
            copyBtn.addEventListener('click', function() {
                const range = document.createRange();
                range.selectNode(generatedMessage);
                window.getSelection().removeAllRanges();
                window.getSelection().addRange(range);
                document.execCommand('copy');
                window.getSelection().removeAllRanges();
                
                // Cambiar texto temporalmente para confirmar
                const originalText = copyBtn.textContent;
                copyBtn.textContent = '¡Copiado! ✅';
                setTimeout(() => {
                    copyBtn.textContent = originalText;
                }, 2000);
            });
            
            // Compartir por WhatsApp
            whatsappBtn.addEventListener('click', function() {
                const message = generatedMessage.textContent;
                const encodedMessage = encodeURIComponent(message);
                window.open(`https://wa.me/?text=${encodedMessage}`, '_blank');
            });
            
            // Función para formatear la fecha
            function formatDate(date) {
                const day = date.getDate();
                const month = date.getMonth() + 1;
                const year = date.getFullYear();
                return `${day < 10 ? '0' + day : day}/${month < 10 ? '0' + month : month}/${year}`;
            }
            
            // Función para obtener emoji según el servicio
            function getServiceEmoji(service) {
                const emojis = {
                    'Netflix': '🎬',
                    'Amazon Prime': '🛒',
                    'Disney+': '🏰',
                    'HBO Max': '🍿',
                    'Spotify': '🎵',
                    'YouTube Premium': '▶️',
                    'default': '📺'
                };
                
                for (const [key, emoji] of Object.entries(emojis)) {
                    if (service.includes(key)) return emoji;
                }
                return emojis.default;
            }
            
            // Función para formatear los datos de la cuenta
            function formatAccountData(data) {
                // Separar en líneas y agregar emoji de bullet point
                return data.split('\n')
                    .filter(line => line.trim() !== '')
                    .map(line => `   • ${line.trim()}`)
                    .join('\n');
            }
        });
    </script>
</body>
</html># whatsapp
