<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Galerie d'Art - Vente de Dessins</title>
    <script src="https://js.stripe.com/v3/"></script>
    <style>
        body { font-family: Arial, sans-serif; text-align: center; background-color: #f4f4f4; }
        h1 { color: #333; }
        .gallery { display: flex; flex-wrap: wrap; justify-content: center; }
        .art-item { margin: 15px; padding: 10px; background: white; border-radius: 8px; box-shadow: 0 0 10px rgba(0,0,0,0.1); }
        img { width: 200px; height: auto; border-radius: 5px; }
        .price { font-weight: bold; color: #e63946; }
        .buy-button { display: block; margin-top: 10px; padding: 8px 12px; background: #007bff; color: white; text-decoration: none; border-radius: 5px; }
        .apple-pay-button { margin-top: 10px; padding: 8px 12px; background: black; color: white; border-radius: 5px; cursor: pointer; }
    </style>
</head>
<body>
    <h1>Bienvenue dans ma Galerie</h1>
    <p>Découvrez et achetez mes œuvres uniques.</p>
    
    <div class="gallery" id="gallery">
        <!-- Les œuvres seront ajoutées ici -->
    </div>
    
    <script>
        const stripe = Stripe("ton_clé_publique_stripe");
        
        const artworks = [
            { title: "Dessin 1", image: "images/dessin1.jpg", price: "50€", stripePriceId: "price_1A2B3C4D" },
            { title: "Dessin 2", image: "images/dessin2.jpg", price: "60€", stripePriceId: "price_5E6F7G8H" }
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
