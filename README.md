<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Galerie d'Art - Vente de Dessins</title>
    <script src="https://js.stripe.com/v3/"></script>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap" rel="stylesheet">
    <style>
        /* Arrière-plan taupe clair */
        body { 
            font-family: 'Poppins', sans-serif; 
            text-align: center; 
            background-color: #EAE7DC; /* Taupe clair */
            color: #333; 
            margin: 0;
            padding: 0;
            position: relative;
        }

        /* Ajout de points colorés */
        body::before {
            content: "";
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            background-image: radial-gradient(circle at 20% 20%, #E63946 5%, transparent 10%),
                              radial-gradient(circle at 80% 30%, #457B9D 5%, transparent 10%),
                              radial-gradient(circle at 50% 80%, #F4A261 5%, transparent 10%);
            opacity: 0.3;
            z-index: -1;
        }

        h1 { 
            color: #2A2A2A; 
            font-size: 3rem;
            margin-top: 50px;
        }

        p { 
            color: #555; 
            font-size: 1.2rem;
        }

        .gallery { 
            display: flex; 
            flex-wrap: wrap; 
            justify-content: center; 
            margin-top: 30px;
        }

        .art-item { 
            margin: 20px; 
            padding: 15px; 
            background: #FFF8F0; /* Beige clair pour le contraste */
            border-radius: 12px; 
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1); 
            width: 250px;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .art-item:hover { 
            transform: translateY(-10px); 
            box-shadow: 0 15px 25px rgba(0, 0, 0, 0.2); 
        }

        img { 
            width: 100%; 
            height: auto; 
            border-radius: 8px; 
            object-fit: cover; 
            margin-bottom: 10px;
        }

        .price { 
            font-weight: bold; 
            color: #E63946;
            margin: 10px 0;
        }

        .buy-button { 
            display: block; 
            margin-top: 10px; 
            padding: 12px 18px; 
            background-color: #2A9D8F; /* Vert doux */
            color: #fff; 
            text-decoration: none; 
            border-radius: 8px; 
            font-size: 1rem;
            border: none;
            cursor: pointer;
        }

        .buy-button:hover { 
            background-color: #264653; /* Bleu-gris foncé */
        }

        .apple-pay-button { 
            margin-top: 10px; 
            padding: 12px 18px; 
            background-color: #000; 
            color: #fff; 
            border-radius: 8px; 
            cursor: pointer; 
            font-size: 1rem;
            border: none;
        }

        .apple-pay-button:hover { 
            background-color: #333; 
        }

        .footer {
            background-color: #4B4B4B;
            color: #fff;
            padding: 15px;
            margin-top: 40px;
        }
    </style>
</head>
<body>
    <h1>Bienvenue dans ma Galerie</h1>
    <p>Découvrez et achetez mes œuvres uniques.</p>
    
    <div class="gallery" id="gallery">
        <!-- Les œuvres seront ajoutées ici -->
    </div>

    <div class="footer">
        <p>&copy; 2025 Galerie d'Art - Vente de Dessins</p>
    </div>
    
    <script>
        const stripe = Stripe("ton_clé_publique_stripe");

        const artworks = [
            { title: "Géodéon", image: "Géodéon.tiff", price: "50€", stripePriceId: "price_1A2B3C4D" },
            { title: "Pélégrin", image: "Pélégrin.jpg", price: "60€", stripePriceId: "price_5E6F7G8H" },
            { title: "Lucien", image: "Lucien.tiff", price: "55€", stripePriceId: "price_2A3B4C5D" },
            { title: "Vlad", image: "Vlad.jpg", price: "65€", stripePriceId: "price_3A4B5C6D" },
            { title: "Dessin 5", image: "images/dessin5.jpg", price: "45€", stripePriceId: "price_4A5B6C7D" },
            { title: "Dessin 6", image: "images/dessin6.jpg", price: "70€", stripePriceId: "price_6A7B8C9D" },
            { title: "Dessin 7", image: "images/dessin7.jpg", price: "75€", stripePriceId: "price_7A8B9C0D" },
            { title: "Dessin 8", image: "images/dessin8.jpg", price: "80€", stripePriceId: "price_8A9B0C1D" },
            { title: "Dessin 9", image: "images/dessin9.jpg", price: "60€", stripePriceId: "price_9A0B1C2D" },
            { title: "Dessin 10", image: "images/dessin10.jpg", price: "50€", stripePriceId: "price_10A1B2C3D" }
        ];

        const gallery = document.getElementById("gallery");
        artworks.forEach(art => {
            const div = document.createElement("div");
            div.className = "art-item";
            div.innerHTML = `
                <img src="${art.image}" alt="${art.title}">
                <p>${art.title}</p>
                <p class="price">${art.price}</p>
                <button class="apple-pay-button" onclick="buyWithApplePay('${art.stripePriceId}')">Acheter avec Apple Pay</button>
            `;
            gallery.appendChild(div);
        });

        function buyWithApplePay(priceId) {
            stripe.redirectToCheckout({
                lineItems: [{ price: priceId, quantity: 1 }],
                mode: "payment",
                successUrl: "https://tonsite.com/success",
                cancelUrl: "https://tonsite.com/cancel"
            });
        }
    </script>
</body>
</html>
