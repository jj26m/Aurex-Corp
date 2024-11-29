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
        }
        .header {
            background-color: red;
            color: black;
            padding: 20px;
            text-align: center;
        }
        .button {
            background-color: red;
            color: black;
            padding: 15px 30px;
            border: none;
            margin: 10px;
            cursor: pointer;
            font-size: 18px;
        }
        .button:hover {
            background-color: darkred;
        }
        .hidden {
            display: none;
        }
        .content {
            text-align: center;
            margin-top: 20px;
        }
        .footer {
            position: fixed;
            bottom: 0;
            width: 100%;
            text-align: center;
            padding: 10px;
            background-color: black;
            color: white;
        }
        #form-container {
            margin-top: 20px;
        }
        form {
            background-color: #333;
            padding: 20px;
            border-radius: 10px;
        }
        input, textarea, select {
            margin-bottom: 10px;
            padding: 10px;
            width: 100%;
            border: 1px solid #444;
            border-radius: 5px;
        }
        button[type="submit"] {
            background-color: red;
            color: black;
            padding: 15px;
            border: none;
            width: 100%;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <!-- Header -->
    <div class="header">
        <h1>Aurex Corporation</h1>
    </div>

    <!-- Main Buttons -->
    <div class="content">
        <button class="button" id="formula1-btn">Formula 1</button>
        <button class="button" id="aurexenergy-btn">Aurex Energy</button>
    </div>

    <!-- Formula 1 Buttons -->
    <div id="formula1-buttons" class="hidden">
        <button class="button" id="register-team-btn">Registrar Equipo</button>
        <button class="button" id="register-driver-btn">Registrar Piloto</button>
        <button class="button" id="teams-registered-btn">Equipos Registrados</button>
        <button class="button" id="drivers-registered-btn">Pilotos Registrados</button>
    </div>

    <!-- Aurex Energy Buttons -->
    <div id="aurexenergy-buttons" class="hidden">
        <button class="button" id="tropical-mango-btn">Tropical Mango (Original)</button>
        <button class="button" id="purple-pulse-btn">Purple Pulse (Uva)</button>
    </div>

    <!-- Forms Section -->
    <div id="form-container" class="hidden">
        <!-- Registrar Equipo Form -->
        <div id="register-team-form" class="hidden">
            <h2>Registrar Equipo</h2>
            <form id="team-form">
                <label for="team-name">Nombre del Equipo</label>
                <input type="text" id="team-name" name="team-name" required>

                <label for="owner">Dueño</label>
                <input type="text" id="owner" name="owner" required>

                <label for="members">Miembros</label>
                <textarea id="members" name="members" required></textarea>

                <label for="color">Color</label>
                <input type="text" id="color" name="color" required>

                <label for="logo">Logo (Imagen)</label>
                <input type="file" id="logo" name="logo" required>

                <button type="submit">Enviar</button>
            </form>
        </div>

        <!-- Registrar Piloto Form -->
        <div id="register-driver-form" class="hidden">
            <h2>Registrar Piloto</h2>
            <form id="driver-form">
                <label for="driver-name">Nombre IC</label>
                <input type="text" id="driver-name" name="driver-name" required>

                <label for="age">Edad IC</label>
                <input type="number" id="age" name="age" required>

                <label for="user">Usuario</label>
                <input type="text" id="user" name="user" required>

                <label for="driver-number">Número de Piloto</label>
                <input type="number" id="driver-number" name="driver-number" required>

                <label for="driver-photo">Foto de Roblox</label>
                <input type="file" id="driver-photo" name="driver-photo" required>

                <button type="submit">Enviar</button>
            </form>
        </div>

        <!-- Hacer Pedido Form -->
        <div id="order-form" class="hidden">
            <h2>Hacer Pedido</h2>
            <form id="order-form">
                <label for="ic-name">Nombre IC</label>
                <input type="text" id="ic-name" name="ic-name" required>

                <label for="address">Domicilio</label>
                <input type="text" id="address" name="address" required>

                <label for="flavor">Sabor</label>
                <select id="flavor" name="flavor" required>
                    <option value="Tropical Mango">Tropical Mango (Original)</option>
                    <option value="Purple Pulse">Purple Pulse (Uva)</option>
                </select>

                <button type="submit">Enviar</button>
            </form>
        </div>
    </div>

    <!-- Footer -->
    <div class="footer">
        <p>Desarrollado por: jj26m</p>
    </div>

    <script>
        // Funcionalidad de botones
        document.getElementById("formula1-btn").onclick = function() {
            document.getElementById("formula1-buttons").classList.toggle("hidden");
        };

        document.getElementById("aurexenergy-btn").onclick = function() {
            document.getElementById("aurexenergy-buttons").classList.toggle("hidden");
        };

        document.getElementById("register-team-btn").onclick = function() {
            document.getElementById("register-team-form").classList.toggle("hidden");
        };

        document.getElementById("register-driver-btn").onclick = function() {
            document.getElementById("register-driver-form").classList.toggle("hidden");
        };

        document.getElementById("tropical-mango-btn").onclick = function() {
            document.getElementById("order-form").classList.toggle("hidden");
            document.getElementById("order-form").querySelector("#flavor").value = "Tropical Mango";
        };

        document.getElementById("purple-pulse-btn").onclick = function() {
            document.getElementById("order-form").classList.toggle("hidden");
            document.getElementById("order-form").querySelector("#flavor").value = "Purple Pulse";
        };

        // Webhook submission
        function submitForm(formData, webhookURL) {
            fetch(webhookURL, {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                },
                body: JSON.stringify(formData),
            }).then(response => response.json())
              .then(data => console.log("Form sent successfully:", data))
              .catch(error => console.error("Error:", error));
        }

        // Form submit handlers
        document.getElementById("team-form").onsubmit = function(event) {
            event.preventDefault();
            const formData = {
                "Nombre de Equipo": document.getElementById("team-name").value,
                "Dueño": document.getElementById("owner").value,
                "Miembros": document.getElementById("members").value,
                "Color": document.getElementById("color").value,
                "Logo": document.getElementById("logo").files[0].name,
            };
            submitForm(formData, "https://discord.com/api/webhooks/1311859474004312064/FsFuWn6JBkIbK8bDkdr0ZQugA6LoRqvr0FYJQqa3x7V-I8YGz2QMhn-hrCSNxo19iS3G"); 
        };

        document.getElementById("driver-form").onsubmit = function(event) {
            event.preventDefault();
            const formData = {
                "Nombre IC": document.getElementById("driver-name").value,
                "Edad IC": document.getElementById("age").value,
                "Número": document.getElementById("driver-number").value,
                "Equipo": document.getElementById("user").value,
                "Foto": document.getElementById("driver-photo").files[0].name,
            };
            submitForm(formData, "https://discord.com/api/webhooks/1311858886243778560/bNo814xfHYVQR6v-yJLpagg1gZovujZXMPFGVOPhQ8O4QmslJNskOKJDTchfOPpp8XET"); 
        };

        document.getElementById("order-form").onsubmit = function(event) {
            event.preventDefault();
            const formData = { 
            "Nombre IC": document.getElementById("ic-name").value,
                "Domicilio": document.getElementById("address").value,
                };
                submitForm(formData, "https://discord.com/api/webhooks/1311859093954101312/mS4MkrzJn2cxgq1l8o0Piiz7AWmBLmLi6MjNnGMkaGRY_2zr2F9BXc-t33FlDFdC6kkk"); 
