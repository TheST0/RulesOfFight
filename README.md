<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RulesOfFight (ROF) - Official Website</title>
</head>
<body>
    <h1>Welcome to RulesOfFight (ROF)</h1>
    <div id="rof-price">Loading ROF price...</div>

    <script>
        async function getROFPrice() {
            const url = "https://api.poocoin.app/quotes?tokens=0xb4dc511adc73d47ff5569bd25429ac28435d8243";

            try {
                const response = await fetch(url);
                
                if (!response.ok) {
                    throw new Error(`HTTP error! Status: ${response.status}`);
                }
                
                const data = await response.json();
                
                if (!data || !data.prices || !data.prices["0xb4dc511adc73d47ff5569bd25429ac28435d8243"] || !data.prices["0xb4dc511adc73d47ff5569bd25429ac28435d8243"].price) {
                    throw new Error("Invalid response format or missing price data");
                }
                
                const price = data.prices["0xb4dc511adc73d47ff5569bd25429ac28435d8243"].price;
                document.getElementById("rof-price").innerText = `ROF Price: ${price} USD`;
            } catch (error) {
                console.error("Error fetching ROF price:", error);
                document.getElementById("rof-price").innerText = "ROF Price: Data Unavailable";
            }
        }

        // เรียกใช้ฟังก์ชันทุก 30 วินาทีเพื่ออัปเดตราคา
        setInterval(getROFPrice, 30000);
        getROFPrice();
    </script>
</body>
</html>
