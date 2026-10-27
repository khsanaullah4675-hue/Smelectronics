Tumhi tumchi mahiti (Telegram Bot API Token ani Chat ID) dili ahe. Tyar anusar, tumhala WhatsApp var order receive karnyasathi ani ti order sidhi Telegram var pathavnyasathi ek landing page tayar karayche ahe.
Khali ek simple, clean ani responsive HTML + JavaScript landing pageachi code dili ahe. Yaa landing page madhe ek form asel, tyat customerchi mahiti (Name, Phone, Address, Quantity) bhrun order dili ki ti WhatsApp var message banun jail (je jevha user WhatsApp button dabel) ani baroberach tumchya Telegram Bot dware suddha tich mahiti tumchya Telegram group/channel (-1003829251913) var auto-forward hoil.
Landing Page Code (index.html):
<!DOCTYPE html>
<html lang="bn">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-data, initial-scale=1.0">
    <title>Order Landing Page</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f7f6;
            margin: 0;
            padding: 20px;
        }
        .container {
            max-width: 500px;
            background: #ffffff;
            padding: 25px;
            margin: auto;
            border-radius: 10px;
            box-shadow: 0px 0px 10px rgba(0,0,0,0.1);
        }
        h2 {
            text-align: center;
            color: #333;
        }
        .form-group {
            margin-bottom: 15px;
        }
        label {
            display: block;
            margin-bottom: 5px;
            color: #666;
        }
        input, textarea {
            width: 100%;
            padding: 10px;
            border: 1px solid #ccc;
            border-radius: 5px;
            box-sizing: border-box;
        }
        button {
            width: 100%;
            background-color: #25D366;
            color: white;
            padding: 12px;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
        }
        button:hover {
            background-color: #1ebe5d;
        }
    </style>
</head>
<body>

<div class="container">
    <h2>Order Form</h2>
    <form id="orderForm">
        <div class="form-group">
            <label for="name">Apke Name:</label>
            <input type="text" id="name" required placeholder="Tumche nav lihika">
        </div>
        <div class="form-group">
            <label for="phone">Phone Number:</label>
            <input type="tel" id="phone" required placeholder="Mobile number">
        </div>
        <div class="form-group">
            <label for="address">Delivery Address:</label>
            <textarea id="address" rows="3" required placeholder="Thikana lihika"></textarea>
        </div>
        <button type="submit">WhatsApp e Order Din</button>
    </form>
</div>

<script>
    const BOT_TOKEN = "8563079348:AAEjHKiPHfmXc3sAHZfMdcDuPZLUtwMpL2w";
    const CHAT_ID = "-1003829251913";
    const WHATSAPP_NUMBER = "8801XXXXXXXXX"; // Yethe tumcha WhatsApp number taka (country code sobat)

    document.getElementById('orderForm').addEventListener('submit', function(e) {
        e.preventDefault();

        const name = document.getElementById('name').value;
        const phone = document.getElementById('phone').value;
        const address = document.getElementById('address').value;

        // 1. Telegram var data pathavnyasathi API call
        const message = `🛍️ New Order Received!\n\n👤 Name: ${name}\n📞 Phone: ${phone}\n📍 Address: ${address}`;
        
        const url = `https://api.telegram.org/bot${BOT_TOKEN}/sendMessage?chat_id=${CHAT_ID}&text=${encodeURIComponent(message)}`;

        fetch(url)
        .then(response => response.json())
        .then(data => {
            console.log("Telegram success", data);
        })
        .catch(error => {
            console.error("Telegram error", error);
        });

        // 2. WhatsApp var redirect karnyasathi
        const whatsappMessage = `Hello, I want to place an order.\nName: ${name}\nPhone: ${phone}\nAddress: ${address}`;
        const whatsappURL = `https://wa.me/${WHATSAPP_NUMBER}?text=${encodeURIComponent(whatsappMessage)}`;
        
        alert("Order successfully submit zali! Aata WhatsApp var redirect hot ahe...");
        window.location.href = whatsappURL;
    });
</script>

</body>
</html>

Kase vaparal pahije?
 * Ya code la copy karun index.html navane save kara.
 * Code madhe WHATSAPP_NUMBER = "8801XXXXXXXXX"; ya thikani tumcha aplyala pahije aslela WhatsApp number country code sobat (uds. 88017XXXXXXXX Bangladesh sathi) takun dya.
 * He file hosting var (Netlify, Vercel ya GitHub Pages sarkhya free platforms var) upload karun tumhi wapru shakta. Customer form bharel tevha to order automatic tumchya Telegram group/channel var yeil ani baroberach WhatsApp var suddha message chalu hoil.
