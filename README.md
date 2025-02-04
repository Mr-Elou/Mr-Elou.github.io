/* Fichier CSS commun : style.css */

body {
    font-family: 'Poppins', sans-serif;
    text-align: center;
    background-color: #EAE7DC;
    color: #333;
    margin: 0;
    padding: 0;
}

nav {
    background: #2A2A2A;
    padding: 15px;
    text-align: center;
}

nav a {
    color: white;
    text-decoration: none;
    margin: 0 15px;
    font-size: 1.2rem;
    font-weight: 600;
}

nav a:hover {
    color: #E63946;
}

.container {
    padding: 20px;
}

/* Fichier HTML : index.html */
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Accueil - Galerie d'Art</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <nav>
        <a href="index.html">Home</a>
        <a href="drawings.html">Drawings</a>
        <a href="contact.html">Contact</a>
    </nav>
    <div class="container">
        <h1>Bienvenue sur ma Galerie d'Art</h1>
        <p>Découvrez un univers unique à travers mes œuvres artistiques.</p>
        <img src="images/illustration1.jpg" alt="Illustration 1" width="300">
        <img src="images/illustration2.jpg" alt="Illustration 2" width="300">
    </div>
</body>
</html>

/* Fichier HTML : drawings.html (Galerie) */
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Galerie d'Art - Dessins</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <nav>
        <a href="index.html">Home</a>
        <a href="drawings.html">Drawings</a>
        <a href="contact.html">Contact</a>
    </nav>
    <div class="container">
        <h1>Mes Œuvres</h1>
        <div class="gallery" id="gallery"></div>
    </div>
    <script>
        const artworks = [
            { title: "Dessin 1", image: "images/dessin1.jpg", price: "50€" },
            { title: "Dessin 2", image: "images/dessin2.jpg", price: "60€" }
        ];
        const gallery = document.getElementById("gallery");
        artworks.forEach(art => {
            const div = document.createElement("div");
            div.innerHTML = `<img src="${art.image}" alt="${art.title}"><p>${art.title}</p><p>${art.price}</p>`;
            gallery.appendChild(div);
        });
    </script>
</body>
</html>

/* Fichier HTML : contact.html (Formulaire) */
<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Contact</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <nav>
        <a href="index.html">Home</a>
        <a href="drawings.html">Drawings</a>
        <a href="contact.html">Contact</a>
    </nav>
    <div class="container">
        <h1>Contactez-moi</h1>
        <form action="submit_form.php" method="post">
            <input type="text" name="nom" placeholder="Nom" required><br>
            <input type="text" name="prenom" placeholder="Prénom" required><br>
            <input type="email" name="email" placeholder="Email" required><br>
            <textarea name="message" placeholder="Votre message" required></textarea><br>
            <button type="submit">Envoyer</button>
        </form>
    </div>
</body>
</html>
