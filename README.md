<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Galerie d'Art - Vente de Dessins</title>
    <script src="https://js.stripe.com/v3/"></script>
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap" rel="stylesheet">
    <style>
        body { 
            font-family: 'Poppins', sans-serif; 
            text-align: center; 
            background-color: #f5f5f5; 
            color: #333; 
            margin: 0;
            padding: 0;
        }

        h1 { 
            color: #4b4b4b; 
            font-size: 3rem;
            margin-top: 50px;
        }

        p { 
            color: #6b6b6b; 
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
            background: #fff; 
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
            color: #e63946;
            margin: 10px 0;
        }

        .buy-button { 
            display: block; 
            margin-top: 10px; 
            padding: 12px 18px; 
            background-color: #2a9d8f; 
            color: #fff; 
            text-decoration: none; 
            border-radius: 8px; 
            font-size: 1rem;
        }

        .buy-button:hover { 
            background-color: #264653; 
        }

        .apple-pay-button { 
            margin-top: 10px; 
            padding: 12px 18px; 
            background-color: #000; 
            color: #fff; 
            border-radius: 8px; 
            cursor: pointer; 
            font-size: 1rem;
        }

        .apple-pay-button:hover { 
            background-color: #333; 
        }

        .footer {
            background-color: #4b4b4b;
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
            { title: "Dessin 1", image: "images/dessin1.jpg", price: "50€", stripePriceId: "price_1A2B3C4D" },
            { title: "Dessin 2", image: "images/dessin2.jpg", price: "60€", stripePriceId: "price_5E6F7G8H" },
            { title: "Dessin 3", image: "images/dessin3.jpg", price: "55€", stripePriceId: "price_2A3B4C5D" },
            { title: "Dessin 4", image: "images/dessin4.jpg", price: "65€", stripePriceId: "price_3A4B5C6D" },
            { title: "Dessin 5", image: "images/dessin5.jpg", price: "45€", stripePriceId: "price_4A5B6C7D" },
            { title: "Dessin 6", image: "images/dessin6.jpg", price: "70€", stripePriceId: "price_6A7B8C9D" },
            { title: "Dessin 7", image: "images/dessin7.jpg", price: "75€", stripePriceId: "price_7A8B9C0D" },
            { title: "Dessin 8", image: "images/dessin8.jpg", price: "80€", stripePriceId: "price_8A9B0C1D" },
            { title: "Dessin 9", image: "images/dessin9.jpg", price: "60€", stripePriceId: "price_9A0B1C2D" },
            { title: "Dessin 10", image: "images/dessin10.jpg", price: "50€", stripePriceId: "price_10A1B2C3D" },
            { title: "Dessin 11", image: "images/dessin11.jpg", price: "65€", stripePriceId: "price_11A2B3C4D" },
            { title: "Dessin 12", image: "images/dessin12.jpg", price: "55€", stripePriceId: "price_12A3B4C5D" },
            { title: "Dessin 13", image: "images/dessin13.jpg", price: "50€", stripePriceId: "price_13A4B5C6D" },
            { title: "Dessin 14", image: "images/dessin14.jpg", price: "90€", stripePriceId: "price_14A5B6C7D" },
            { title: "Dessin 15", image: "images/dessin15.jpg", price: "80€", stripePriceId: "price_15A6B7C8D" }
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
