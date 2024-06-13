<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Adriano Peniche Gasque</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }
        header {
            background-color: #333;
            color: #fff;
            padding: 10px 0;
            text-align: center;
        }
        header h1 {
            margin: 0;
            font-size: 2.5em;
        }
        .container {
            display: flex;
            justify-content: space-between;
            padding: 20px;
        }
        .main-content {
            width: 70%;
        }
        .sidebar {
            width: 25%;
            background-color: #ccc;
            padding: 10px;
            border-radius: 5px;
        }
        .post {
            background-color: #fff;
            padding: 20px;
            margin-bottom: 20px;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        .post h2 {
            margin-top: 0;
        }
        .comments {
            margin-top: 20px;
        }
        .comments h3 {
            margin: 0;
            font-size: 1.5em;
        }
        .comments textarea {
            width: 100%;
            height: 100px;
            margin-top: 10px;
            padding: 10px;
            border-radius: 5px;
            border: 1px solid #ccc;
        }
        .comments button {
            display: block;
            margin-top: 10px;
            padding: 10px 20px;
            background-color: #333;
            color: #fff;
            border: none;
            border-radius: 5px;
            cursor: pointer;
        }
        .comments button:hover {
            background-color: #555;
        }
        .ad {
            background-color: #fff;
            padding: 10px;
            margin-bottom: 20px;
            border-radius: 5px;
            text-align: center;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
    </style>
</head>
<body>
    <header>
        <h1>Adriano Peniche Gasque</h1>
    </header>
    <div class="container">
        <div class="main-content">
            <div class="post">
                <h2>Pensamiento del Día</h2>
                <!-- Aquí se mostrará el último pensamiento del día -->
                <div id="latestThought">
                    <p>Este es el espacio donde puedo escribir mis pensamientos, reflexiones, y más. Cada día, compartiré algo nuevo aquí.</p>
                </div>
                <!-- Formulario para ingresar nuevo pensamiento del día -->
                <form id="thoughtForm">
                    <label for="thoughtTitle">Título:</label><br>
                    <input type="text" id="thoughtTitle" name="thoughtTitle" required><br>
                    <label for="thoughtContent">Contenido:</label><br>
                    <textarea id="thoughtContent" name="thoughtContent" rows="5" required></textarea><br>
                    <button type="submit">Publicar Pensamiento del Día</button>
                </form>
            </div>
            <!-- Sección para mostrar pensamientos anteriores (opcional) -->
            <div id="previousThoughts">
                <h2>Pensamientos Anteriores</h2>
                <!-- Aquí puedes agregar pensamientos anteriores si deseas -->
            </div>
            <!-- Sección de comentarios -->
            <div class="comments">
                <h3>Comentarios</h3>
                <textarea id="commentContent" placeholder="Escribe tu comentario aquí..."></textarea>
                <button id="submitComment">Enviar Comentario</button>
                <div id="commentsList">
                    <!-- Aquí se mostrarán los comentarios -->
                </div>
            </div>
        </div>
        <div class="sidebar">
            <div class="ad">
                <p>Espacio publicitario</p>
            </div>
            <div class="ad">
                <p>Espacio publicitario</p>
            </div>
        </div>
    </div>

    <!-- Script para la funcionalidad de comentarios -->
    <script>
        // Función para obtener la fecha actual en formato "YYYY-MM-DD"
        function getCurrentDate() {
            const now = new Date();
            const year = now.getFullYear();
            let month = now.getMonth() + 1;
            if (month < 10) month = `0${month}`;
            let day = now.getDate();
            if (day < 10) day = `0${day}`;
            return `${year}-${month}-${day}`;
        }

        // Datos simulados de pensamientos del día y comentarios (para pruebas)
        let thoughtsData = [
            { id: 1, title: "Primer Pensamiento", content: "Este es mi primer pensamiento del día." }
        ];
        let commentsData = [
            { id: 1, thoughtId: 1, content: "¡Qué gran pensamiento!" }
        ];

        // Función para mostrar el último pensamiento del día
        function showLatestThought() {
            const latestThought = thoughtsData[thoughtsData.length - 1];
            if (latestThought) {
                const latestThoughtHtml = `
                    <p><strong>${latestThought.title}</strong><br>${latestThought.content}</p>
                `;
                document.getElementById('latestThought').innerHTML = latestThoughtHtml;
            }
        }

        // Función para mostrar los comentarios
        function showComments() {
            const commentsList = document.getElementById('commentsList');
            commentsList.innerHTML = '';
            commentsData.forEach(comment => {
                const commentHtml = `
                    <div class="comment">
                        <p>${comment.content}</p>
                    </div>
                `;
                commentsList.innerHTML += commentHtml;
            });
        }

        // Mostrar pensamiento inicial al cargar la página
        showLatestThought();
        showComments();

        // Manejar el envío del formulario de pensamiento del día
        const thoughtForm = document.getElementById('thoughtForm');
        thoughtForm.addEventListener('submit', function(event) {
            event.preventDefault();
            const thoughtTitle = document.getElementById('thoughtTitle').value;
            const thoughtContent = document.getElementById('thoughtContent').value;
            const newThought = {
                id: thoughtsData.length + 1,
                title: thoughtTitle,
                content: thoughtContent,
                date: getCurrentDate()
            };
            thoughtsData.push(newThought);
            showLatestThought();
            thoughtForm.reset();
        });

        // Manejar el envío del formulario de comentarios
        const submitCommentBtn = document.getElementById('submitComment');
        submitCommentBtn.addEventListener('click', function(event) {
            event.preventDefault();
            const commentContent = document.getElementById('commentContent').value;
            const newComment = {
                id: commentsData.length + 1,
                thoughtId: thoughtsData.length, // Aquí podrías usar el ID del pensamiento específico si lo implementas
                content: commentContent,
                date: getCurrentDate()
            };
            commentsData.push(newComment);
            showComments();
            document.getElementById('commentContent').value = '';
        });
    </script>
</body>
</html>
