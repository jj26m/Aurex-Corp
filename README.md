<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Aurex Corporation</title>
  <style>
    body {
      background-color: black;
      color: white;
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
    }
    .header {
      background-color: red;
      padding: 10px;
      text-align: center;
      font-size: 24px;
      color: black;
    }
    .button {
      background-color: red;
      color: black;
      border: none;
      padding: 10px 20px;
      margin: 10px;
      cursor: pointer;
      font-size: 18px;
    }
    .button:hover {
      opacity: 0.8;
    }
    .hidden {
      display: none;
    }
    .container {
      display: flex;
      justify-content: center;
      flex-direction: column;
      align-items: center;
    }
    .form {
      background-color: #333;
      padding: 20px;
      border-radius: 10px;
      margin-top: 20px;
      width: 300px;
    }
    .form input, .form textarea {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border: 1px solid #fff;
      background-color: #444;
      color: white;
      font-size: 16px;
    }
    .form input[type="file"] {
      padding: 0;
    }
    .form button {
      background-color: red;
      color: black;
      padding: 10px;
      border: none;
      font-size: 18px;
    }
    .form button:hover {
      opacity: 0.8;
    }
    .footer {
      text-align: center;
      margin-top: 50px;
      font-size: 14px;
    }
    .lateral {
      position: absolute;
      top: 0;
      bottom: 0;
      z-index: -1;
    }
    .lateral-left {
      left: 0;
      width: 200px;
    }
    .lateral-right {
      right: 0;
      width: 200px;
    }
  </style>
</head>
<body>

<!-- Imágenes laterales -->
<img src="https://ibb.co/HYYxx84" class="lateral lateral-left" />
<img src="https://ibb.co/88Y1skm" class="lateral lateral-right" />

<div class="header">
  Aurex Corporation
</div>

<div class="container">
  <!-- Botones de Navegación -->
  <button class="button" onclick="showSection('f1Section')">Formula 1</button>
  <button class="button" onclick="showSection('energySection')">Aurex Energy</button>

  <!-- Sección Formula 1 -->
  <div id="f1Section" class="hidden">
    <button class="button" onclick="showForm('teamForm')">Registrar Equipo</button>
    <button class="button" onclick="showForm('pilotForm')">Registrar Piloto</button>
    <button class="button" onclick="showSection('teamsRegistered')">Equipos Registrados</button>
    <button class="button" onclick="showSection('pilotsRegistered')">Pilotos Registrados</button>
  </div>

  <!-- Sección Aurex Energy -->
  <div id="energySection" class="hidden">
    <button class="button" onmouseover="this.innerHTML='Pedir'" onmouseout="this.innerHTML='Tropical Mango (Original)'" onclick="showForm('orderForm')">Tropical Mango (Original)</button>
    <button class="button" onmouseover="this.innerHTML='Pedir'" onmouseout="this.innerHTML='Purple Pulse (Uva)'" onclick="showForm('orderForm')">Purple Pulse (Uva)</button>
  </div>

  <!-- Formularios -->

  <!-- Formulario Registrar Equipo -->
  <div id="teamForm" class="hidden form">
    <h3>Registrar Equipo</h3>
    <input type="text" id="teamName" placeholder="Nombre del Equipo">
    <input type="text" id="owner" placeholder="Dueño (@)">
    <input type="text" id="members" placeholder="Miembros">
    <input type="text" id="color" placeholder="Color">
    <input type="file" id="logo" placeholder="Logo">
    <button onclick="submitForm('team')">Enviar</button>
  </div>

  <!-- Formulario Registrar Piloto -->
  <div id="pilotForm" class="hidden form">
    <h3>Registrar Piloto</h3>
    <input type="text" id="pilotName" placeholder="Nombre IC">
    <input type="text" id="pilotAge" placeholder="Edad IC">
    <input type="text" id="pilotUser" placeholder="User">
    <input type="text" id="pilotNumber" placeholder="Número de Piloto">
    <input type="file" id="pilotPhoto" placeholder="Foto">
    <button onclick="submitForm('pilot')">Enviar</button>
  </div>

  <!-- Formulario Pedir Producto -->
  <div id="orderForm" class="hidden form">
    <h3>Hacer Pedido</h3>
    <input type="text" id="orderName" placeholder="Nombre IC">
    <input type="text" id="orderAddress" placeholder="Domicilio">
    <button onclick="submitForm('order')">Enviar</button>
  </div>

  <!-- Equipos Registrados -->
  <div id="teamsRegistered" class="hidden">
    <h3>Equipos Registrados</h3>
    <div id="teamsList"></div>
  </div>

  <!-- Pilotos Registrados -->
  <div id="pilotsRegistered" class="hidden">
    <h3>Pilotos Registrados</h3>
    <div id="pilotsList"></div>
  </div>
</div>

<!-- Footer -->
<div class="footer">
  Desarrollado por: jj26m
</div>

<script>
  // Mostrar y ocultar secciones
  function showSection(sectionId) {
    const sections = ['f1Section', 'energySection', 'teamsRegistered', 'pilotsRegistered'];
    sections.forEach(id => document.getElementById(id).classList.add('hidden'));
    document.getElementById(sectionId).classList.remove('hidden');
  }

  function showForm(formId) {
    const forms = ['teamForm', 'pilotForm', 'orderForm'];
    forms.forEach(id => document.getElementById(id).classList.add('hidden'));
    document.getElementById(formId).classList.remove('hidden');
  }

  // Enviar formularios a Webhook de Discord
  function submitForm(formType) {
    let webhookUrl = '';
    let data = {};
    
    if (formType === 'team') {
      webhookUrl = '--[Webhook Registrar Equipo]--';
      data = {
        teamName: document.getElementById('teamName').value,
        owner: document.getElementById('owner').value,
        members: document.getElementById('members').value,
        color: document.getElementById('color').value,
        logo: document.getElementById('logo').files[0]
      };
    } else if (formType === 'pilot') {
      webhookUrl = '--[Webhook Registrar Piloto]--';
      data = {
        pilotName: document.getElementById('pilotName').value,
        pilotAge: document.getElementById('pilotAge').value,
        pilotUser: document.getElementById('pilotUser').value,
        pilotNumber: document.getElementById('pilotNumber').value,
        pilotPhoto: document.getElementById('pilotPhoto').files[0]
      };
    } else if (formType === 'order') {
      webhookUrl = '--[Webhook Hacer Pedido]--';
      data = {
        orderName: document.getElementById('orderName').value,
        orderAddress: document.getElementById('orderAddress').value,
        flavor: formType === 'order' ? 'Tropical Mango' : 'Purple Pulse'
      };
    }

    // Enviar a Discord Webhook
    const formData = new FormData();
    formData.append('content', `**${formType === 'team' ? 'Nombre de Equipo' : formType === 'pilot' ? 'Nombre IC' : 'Nombre IC'}:** ${data[formType + 'Name']}\n**Dueño:** ${data.owner}\n**Miembros:** ${data.members}\n**Color:** ${data.color}\n**Logo:** ${data.logo ? 'Archivo adjunto' : 'No disponible'}`);

    fetch(webhookUrl, {
      method: 'POST',
      body: formData
    })
    .then(response => response.json())
    .then(data => console.log('Formulario enviado con éxito', data))
    .catch(error => console.error('Error al enviar formulario:', error));
 Aquí tienes el código HTML completo para el sitio web de **Aurex Corporation** que incluye la estructura de las secciones solicitadas, formularios y botones. También he integrado los webhooks, aunque tendrás que completar las partes con los webhooks reales donde se indica `--[Webhook...]--`.

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Aurex Corporation</title>
  <style>
    body {
      background-color: black;
      color: white;
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
    }
    .header {
      background-color: red;
      padding: 10px;
      text-align: center;
      font-size: 24px;
      color: black;
    }
    .button {
      background-color: red;
      color: black;
      border: none;
      padding: 10px 20px;
      margin: 10px;
      cursor: pointer;
      font-size: 18px;
    }
    .button:hover {
      opacity: 0.8;
    }
    .hidden {
      display: none;
    }
    .container {
      display: flex;
      justify-content: center;
      flex-direction: column;
      align-items: center;
    }
    .form {
      background-color: #333;
      padding: 20px;
      border-radius: 10px;
      margin-top: 20px;
      width: 300px;
    }
    .form input, .form textarea {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border: 1px solid #fff;
      background-color: #444;
      color: white;
      font-size: 16px;
    }
    .form input[type="file"] {
      padding: 0;
    }
    .form button {
      background-color: red;
      color: black;
      padding: 10px;
      border: none;
      font-size: 18px;
    }
    .form button:hover {
      opacity: 0.8;
    }
    .footer {
      text-align: center;
      margin-top: 50px;
      font-size: 14px;
    }
    .lateral {
      position: absolute;
      top: 0;
      bottom: 0;
      z-index: -1;
    }
    .lateral-left {
      left: 0;
      width: 200px;
    }
    .lateral-right {
      right: 0;
      width: 200px;
    }
  </style>
</head>
<body>

<!-- Imágenes laterales -->
<img src="https://ibb.co/HYYxx84" class="lateral lateral-left" />
<img src="https://ibb.co/88Y1skm" class="lateral lateral-right" />

<div class="header">
  Aurex Corporation
</div>

<div class="container">
  <!-- Botones de Navegación -->
  <button class="button" onclick="showSection('f1Section')">Formula 1</button>
  <button class="button" onclick="showSection('energySection')">Aurex Energy</button>

  <!-- Sección Formula 1 -->
  <div id="f1Section" class="hidden">
    <button class="button" onclick="showForm('teamForm')">Registrar Equipo</button>
    <button class="button" onclick="showForm('pilotForm')">Registrar Piloto</button>
    <button class="button" onclick="showSection('teamsRegistered')">Equipos Registrados</button>
    <button class="button" onclick="showSection('pilotsRegistered')">Pilotos Registrados</button>
  </div>

  <!-- Sección Aurex Energy -->
  <div id="energySection" class="hidden">
    <button class="button" onmouseover="this.innerHTML='Pedir'" onmouseout="this.innerHTML='Tropical Mango (Original)'" onclick="showForm('orderForm')">Tropical Mango (Original)</button>
    <button class="button" onmouseover="this.innerHTML='Pedir'" onmouseout="this.innerHTML='Purple Pulse (Uva)'" onclick="showForm('orderForm')">Purple Pulse (Uva)</button>
  </div>

  <!-- Formularios -->

  <!-- Formulario Registrar Equipo -->
  <div id="teamForm" class="hidden form">
    <h3>Registrar Equipo</h3>
    <input type="text" id="teamName" placeholder="Nombre del Equipo">
    <input type="text" id="owner" placeholder="Dueño (@)">
    <input type="text" id="members" placeholder="Miembros">
    <input type="text" id="color" placeholder="Color">
    <input type="file" id="logo" placeholder="Logo">
    <button onclick="submitForm('team')">Enviar</button>
  </div>

  <!-- Formulario Registrar Piloto -->
  <div id="pilotForm" class="hidden form">
    <h3>Registrar Piloto</h3>
    <input type="text" id="pilotName" placeholder="Nombre IC">
    <input type="text" id="pilotAge" placeholder="Edad IC">
    <input type="text" id="pilotUser" placeholder="User">
    <input type="text" id="pilotNumber" placeholder="Número de Piloto">
    <input type="file" id="pilotPhoto" placeholder="Foto">
    <button onclick="submitForm('pilot')">Enviar</button>
  </div>

  <!-- Formulario Pedir Producto -->
  <div id="orderForm" class="hidden form">
    <h3>Hacer Pedido</h3>
    <input type="text" id="orderName" placeholder="Nombre IC">
    <input type="text" id="orderAddress" placeholder="Domicilio">
    <button onclick="submitForm('order')">Enviar</button>
  </div>

  <!-- Equipos Registrados -->
  <div id="teamsRegistered" class="hidden">
    <h3>Equipos Registrados</h3>
    <div id="teamsList"></div>
  </div>

  <!-- Pilotos Registrados -->
  <div id="pilotsRegistered" class="hidden">
    <h3>Pilotos Registrados</h3>
    <div id="pilotsList"></div>
  </div>
</div>

<!-- Footer -->
<div class="footer">
  Desarrollado por: jj26m
</div>

<script>
  // Mostrar y ocultar secciones
  function showSection(sectionId) {
    const sections = ['f1Section', 'energySection', 'teamsRegistered', 'pilotsRegistered'];
    sections.forEach(id => document.getElementById(id).classList.add('hidden'));
    document.getElementById(sectionId).classList.remove('hidden');
  }

  function showForm(formId) {
    const forms = ['teamForm', 'pilotForm', 'orderForm'];
    forms.forEach(id => document.getElementById(id).classList.add('hidden'));
    document.getElementById(formId).classList.remove('hidden');
  }

  // Enviar formularios a Webhook de Discord
  function submitForm(formType) {
    let webhookUrl = '';
    let data = {};
    
    if (formType === 'team') {
      webhookUrl = '--[Webhook Registrar Equipo]--';
      data = {
        teamName: document.getElementById('teamName').value,
        owner: document.getElementById('owner').value,
        members: document.getElementById('members').value,
        color: document.getElementById('color').value,
        logo: document.getElementById('logo').files[0]
      };
    } else if (formType === 'pilot') {
      webhookUrl = '--[Webhook Registrar Piloto]--';
      data = {
        pilotName: document.getElementById('pilotName').value,
        pilotAge: document.getElementById('pilotAge').value,
        pilotUser: document.getElementById('pilotUser').value,
        pilotNumber: document.getElementById('pilotNumber').value,
        pilotPhoto: document.getElementById('pilotPhoto').files[0]
      };
    } else if (formType === 'order') {
      webhookUrl = '--[Webhook Hacer Pedido]--';
      data = {
        orderName: document.getElementById('orderName').value,
        orderAddress: document.getElementById('orderAddress').value,
        flavor: formType === 'order' ? 'Tropical Mango' : 'Purple Pulse'
      };
    }

    // Enviar a Discord Webhook
    const formData = new FormData();
    formData.append('content', `**${formType === 'team' ? 'Nombre de Equipo' : formType === 'pilot' ? 'Nombre IC' : 'Nombre IC'}:** ${data[formType + 'Name']}\n**Dueño:** ${data.owner}\n**Miembros:** ${data.members}\n**Color:** ${data.color}\n**Logo:** ${data.logo ? 'Archivo adjunto' : 'No disponible'}`);

    fetch(webhookUrl, {
      method: 'POST',
      body: formData
    })
    .then(response => response.json())
    .then(data => console.log('Formulario enviado con éxito', data))
    .catch(error => console.error('Error al enviar formularioAquí tienes el código para la página web completa, incluyendo la estructura con los formularios y las imágenes laterales. He integrado las secciones como "Formula 1" y "Aurex Energy", así como la funcionalidad de formularios que se envían a los webhooks. Los webhooks deben ser reemplazados con las URLs reales en los lugares indicados. 

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Aurex Corporation</title>
  <style>
    body {
      background-color: black;
      color: white;
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
    }
    .header {
      background-color: red;
      padding: 10px;
      text-align: center;
      font-size: 24px;
      color: black;
    }
    .button {
      background-color: red;
      color: black;
      border: none;
      padding: 10px 20px;
      margin: 10px;
      cursor: pointer;
      font-size: 18px;
    }
    .button:hover {
      opacity: 0.8;
    }
    .hidden {
      display: none;
    }
    .container {
      display: flex;
      justify-content: center;
      flex-direction: column;
      align-items: center;
    }
    .form {
      background-color: #333;
      padding: 20px;
      border-radius: 10px;
      margin-top: 20px;
      width: 300px;
    }
    .form input, .form textarea {
      width: 100%;
      padding: 10px;
      margin: 10px 0;
      border: 1px solid #fff;
      background-color: #444;
      color: white;
      font-size: 16px;
    }
    .form input[type="file"] {
      padding: 0;
    }
    .form button {
      background-color: red;
      color: black;
      padding: 10px;
      border: none;
      font-size: 18px;
    }
    .form button:hover {
      opacity: 0.8;
    }
    .footer {
      text-align: center;
      margin-top: 50px;
      font-size: 14px;
    }
    .lateral {
      position: absolute;
      top: 0;
      bottom: 0;
      z-index: -1;
    }
    .lateral-left {
      left: 0;
      width: 200px;
    }
    .lateral-right {
      right: 0;
      width: 200px;
    }
  </style>
</head>
<body>

<!-- Imágenes laterales -->
<img src="https://ibb.co/HYYxx84" class="lateral lateral-left" />
<img src="https://ibb.co/88Y1skm" class="lateral lateral-right" />

<div class="header">
  Aurex Corporation
</div>

<div class="container">
  <!-- Botones de Navegación -->
  <button class="button" onclick="showSection('f1Section')">Formula 1</button>
  <button class="button" onclick="showSection('energySection')">Aurex Energy</button>

  <!-- Sección Formula 1 -->
  <div id="f1Section" class="hidden">
    <button class="button" onclick="showForm('teamForm')">Registrar Equipo</button>
    <button class="button" onclick="showForm('pilotForm')">Registrar Piloto</button>
    <button class="button" onclick="showSection('teamsRegistered')">Equipos Registrados</button>
    <button class="button" onclick="showSection('pilotsRegistered')">Pilotos Registrados</button>
  </div>

  <!-- Sección Aurex Energy -->
  <div id="energySection" class="hidden">
    <button class="button" onmouseover="this.innerHTML='Pedir'" onmouseout="this.innerHTML='Tropical Mango (Original)'" onclick="showForm('orderForm')">Tropical Mango (Original)</button>
    <button class="button" onmouseover="this.innerHTML='Pedir'" onmouseout="this.innerHTML='Purple Pulse (Uva)'" onclick="showForm('orderForm')">Purple Pulse (Uva)</button>
  </div>

  <!-- Formularios -->

  <!-- Formulario Registrar Equipo -->
  <div id="teamForm" class="hidden form">
    <h3>Registrar Equipo</h3>
    <input type="text" id="teamName" placeholder="Nombre del Equipo">
    <input type="text" id="owner" placeholder="Dueño (@)">
    <input type="text" id="members" placeholder="Miembros">
    <input type="text" id="color" placeholder="Color">
    <input type="file" id="logo" placeholder="Logo">
    <button onclick="submitForm('team')">Enviar</button>
  </div>

  <!-- Formulario Registrar Piloto -->
  <div id="pilotForm" class="hidden form">
    <h3>Registrar Piloto</h3>
    <input type="text" id="pilotName" placeholder="Nombre IC">
    <input type="text" id="pilotAge" placeholder="Edad IC">
    <input type="text" id="pilotUser" placeholder="User">
    <input type="text" id="pilotNumber" placeholder="Número de Piloto">
    <input type="file" id="pilotPhoto" placeholder="Foto">
    <button onclick="submitForm('pilot')">Enviar</button>
  </div>

  <!-- Formulario Pedir Producto -->
  <div id="orderForm" class="hidden form">
    <h3>Hacer Pedido</h3>
    <input type="text" id="orderName" placeholder="Nombre IC">
    <input type="text" id="orderAddress" placeholder="Domicilio">
    <button onclick="submitForm('order')">Enviar</button>
  </div>

  <!-- Equipos Registrados -->
  <div id="teamsRegistered" class="hidden">
    <h3>Equipos Registrados</h3>
    <div id="teamsList"></div>
  </div>

  <!-- Pilotos Registrados -->
  <div id="pilotsRegistered" class="hidden">
    <h3>Pilotos Registrados</h3>
    <div id="pilotsList"></div>
  </div>
</div>

<!-- Footer -->
<div class="footer">
  Desarrollado por: jj26m
</div>

<script>
  // Mostrar y ocultar secciones
  function showSection(sectionId) {
    const sections = ['f1Section', 'energySection', 'teamsRegistered', 'pilotsRegistered'];
    sections.forEach(id => document.getElementById(id).classList.add('hidden'));
    document.getElementById(sectionId).classList.remove('hidden');
  }

  function showForm(formId) {
    const forms = ['teamForm', 'pilotForm', 'orderForm'];
    forms.forEach(id => document.getElementById(id).classList.add('hidden'));
    document.getElementById(formId).classList.remove('hidden');
  }

  // Enviar formularios a Webhook de Discord
  function submitForm(formType) {
    let webhookUrl = '';
    let data = {};
    
    if (formType === 'team') {
      webhookUrl = 'https://discord.com/api/webhooks/1311859474004312064/FsFuWn6JBkIbK8bDkdr0ZQugA6LoRqvr0FYJQqa3x7V-I8YGz2QMhn-hrCSNxo19iS3G';
      data = {
        teamName: document.getElementById('teamName').value,
        owner: document.getElementById('owner').value,
        members: document.getElementById('members').value,
        color: document.getElementById('color').value,
        logo: document.getElementById('logo').files[0]
      };
    } else if (formType === 'pilot') {
      webhookUrl = 'https://discord.com/api/webhooks/1311858886243778560/bNo814xfHYVQR6v-yJLpagg1gZovujZXMPFGVOPhQ8O4QmslJNskOKJDTchfOPpp8XET';
      data = {
        pilotName: document.getElementById('pilotName').value,
        pilotAge: document.getElementById('pilotAge').value,
        pilotUser: document.getElementById('pilotUser').value,
        pilotNumber: document.getElementById('pilotNumber').value,
        pilotPhoto: document.getElementById('pilotPhoto').files[0]
      };
    } else if (formType === 'order') {
      webhookUrl = 'https://discord.com/api/webhooks/1311859093954101312/mS4MkrzJn2cxgq1l8o0Piiz7AWmBLmLi6MjNnGMkaGRY_2zr2F9BXc-t33FlDFdC6kkk';
      data = {
        orderName: document.getElementById('orderName').value,
        orderAddress: document.getElementById('orderAddress').value,
        flavor: formType === 'order' ? 'Tropical Mango' : 'Purple Pulse'
      };
    }

    // Enviar a Discord Webhook
    const formData = new FormData();
    formData.append('content', `**${formType === 'team' ? 'Nombre de Equipo' : formType === 'pilot' ? 'Nombre IC' : 'Nombre IC'}:** ${data[formType + 'Name']}\n**Dueño:** ${data.owner}\n**Miembros:** ${data.members}\n**Color:** ${data.color}\n**Logo:** ${data.logo ? 'Archivo adjunto' : 'No disponible'}`);

    fetch(webhookUrl, {
      method: 'POST',
      body: formData
    })
    .then(response => response.json())
    .then(data => console.log('Formulario enviado conThe HTML code you provided is well-structured, offering a clean and functional interface for **Aurex Corporation**. It includes:

1. **Navigation buttons** that toggle between sections for Formula 1 and Aurex Energy.
2. **Forms** for team registration, pilot registration, and product orders, with file uploads and input fields for user data.
3. **Images** on the sides of the page, which can be used for branding or visual effects.

To ensure that the forms send data to your Discord server, replace the placeholder webhook URLs (`--[Webhook Registrar Equipo]--`, etc.) with the actual webhook URLs from your Discord server.

A few improvements to consider:
- **Security**: Ensure that the data is sanitized properly before sending to the webhook to prevent any malicious inputs.
- **UI enhancements**: You could add more interactive feedback after form submissions (e.g., a success/error message).
- **Mobile responsiveness**: The layout should work well on mobile devices, but testing across various screen sizes is essential for ensuring it adapts well.
  
If you're ready to implement the code or need any help with the next steps, feel free to ask!
