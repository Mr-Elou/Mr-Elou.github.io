<html lang="en">
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
            background-color: #f5f5f5; 
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
            color: #4b4b4b; 
            color: #2A2A2A; 
            font-size: 3rem;
            margin-top: 50px;
        }

        p { 
            color: #6b6b6b; 
            color: #555; 
            font-size: 1.2rem;
        }

@@ -36,7 +53,7 @@
        .art-item { 
            margin: 20px; 
            padding: 15px; 
            background: #fff; 
            background: #FFF8F0; /* Beige clair pour le contraste */
            border-radius: 12px; 
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1); 
            width: 250px;
@@ -58,23 +75,25 @@

        .price { 
            font-weight: bold; 
            color: #e63946;
            color: #E63946;
            margin: 10px 0;
        }

        .buy-button { 
            display: block; 
            margin-top: 10px; 
            padding: 12px 18px; 
            background-color: #2a9d8f; 
            background-color: #2A9D8F; /* Vert doux */
            color: #fff; 
            text-decoration: none; 
            border-radius: 8px; 
            font-size: 1rem;
            border: none;
            cursor: pointer;
        }

        .buy-button:hover { 
            background-color: #264653; 
            background-color: #264653; /* Bleu-gris foncé */
        }

        .apple-pay-button { 
@@ -85,14 +104,15 @@
            border-radius: 8px; 
            cursor: pointer; 
            font-size: 1rem;
            border: none;
        }

        .apple-pay-button:hover { 
            background-color: #333; 
        }

        .footer {
            background-color: #4b4b4b;
            background-color: #4B4B4B;
            color: #fff;
            padding: 15px;
            margin-top: 40px;
@@ -124,12 +144,7 @@
            { title: "Dessin 7", image: "images/dessin7.jpg", price: "75€", stripePriceId: "price_7A8B9C0D" },
            { title: "Dessin 8", image: "images/dessin8.jpg", price: "80€", stripePriceId: "price_8A9B0C1D" },
            { title: "Dessin 9", image: "images/dessin9.jpg", price: "60€", stripePriceId: "price_9A0B1C2D" },
            { title: "Dessin 10", image: "images/dessin10.jpg", price: "50€", stripePriceId: "price_10A1B2C3D" },
            { title: "Dessin 11", image: "images/dessin11.jpg", price: "65€", stripePriceId: "price_11A2B3C4D" },
            { title: "Dessin 12", image: "images/dessin12.jpg", price: "55€", stripePriceId: "price_12A3B4C5D" },
            { title: "Dessin 13", image: "images/dessin13.jpg", price: "50€", stripePriceId: "price_13A4B5C6D" },
            { title: "Dessin 14", image: "images/dessin14.jpg", price: "90€", stripePriceId: "price_14A5B6C7D" },
            { title: "Dessin 15", image: "images/dessin15.jpg", price: "80€", stripePriceId: "price_15A6B7C8D" }
            { title: "Dessin 10", image: "images/dessin10.jpg", price: "50€", stripePriceId: "price_10A1B2C3D" }
        ];

        const gallery = document.getElementById("gallery");
@@ -144,7 +159,7 @@
            `;
            gallery.appendChild(div);
        });
        
        function buyWithApplePay(priceId) {
            stripe.redirectToCheckout({
                lineItems: [{ price: priceId, quantity: 1 }]
