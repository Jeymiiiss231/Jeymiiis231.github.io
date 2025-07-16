<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Event Tickets - Buy with Bitcoin</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            line-height: 1.6;
            margin: 0;
            padding: 0;
            color: #333;
            background-color: #f5f5f5;
        }
        .container {
            width: 85%;
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        header {
            background-color: #2c3e50;
            color: white;
            padding: 20px 0;
            text-align: center;
        }
        .event-card {
            background: white;
            border-radius: 8px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            margin: 20px 0;
            padding: 20px;
            display: flex;
            flex-wrap: wrap;
            justify-content: space-between;
        }
        .event-image {
            width: 30%;
            min-width: 250px;
        }
        .event-image img {
            width: 100%;
            border-radius: 5px;
        }
        .event-details {
            width: 65%;
            min-width: 250px;
        }
        .ticket-options {
            margin: 20px 0;
        }
        .ticket-type {
            display: flex;
            justify-content: space-between;
            padding: 10px;
            border-bottom: 1px solid #eee;
        }
        .sold-out {
            color: #e74c3c;
            font-weight: bold;
        }
        .available {
            color: #2ecc71;
            font-weight: bold;
        }
        .buy-btn {
            background-color: #3498db;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 4px;
            cursor: pointer;
        }
        .buy-btn:hover {
            background-color: #2980b9;
        }
        .payment-modal {
            display: none;
            position: fixed;
            z-index: 1;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            overflow: auto;
            background-color: rgba(0,0,0,0.4);
        }
        .modal-content {
            background-color: #fefefe;
            margin: 15% auto;
            padding: 20px;
            border: 1px solid #888;
            width: 80%;
            max-width: 500px;
            border-radius: 8px;
        }
        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
            cursor: pointer;
        }
        .close:hover {
            color: black;
        }
        .bitcoin-payment {
            margin-top: 20px;
            padding: 15px;
            background-color: #f8f9fa;
            border-radius: 5px;
        }
        .bitcoin-address {
            word-break: break-all;
            font-family: monospace;
            background-color: #eee;
            padding: 10px;
            border-radius: 4px;
            margin: 10px 0;
        }
        .qr-code {
            text-align: center;
            margin: 15px 0;
        }
        footer {
            background-color: #2c3e50;
            color: white;
            text-align: center;
            padding: 20px 0;
            margin-top: 30px;
        }
    </style>
</head>
<body>
    <header>
        <div class="container">
            <h1>Event Tickets Marketplace</h1>
            <p>Buy tickets with Bitcoin - Fast, Secure, Decentralized</p>
        </div>
    </header>

    <div class="container">
        <div class="event-card">
            <div class="event-image">
                <img src="https://via.placeholder.com/400x300" alt="Concert Image">
            </div>
            <div class="event-details">
                <h2>Summer Music Festival 2023</h2>
                <p><strong>Date:</strong> August 15-17, 2023</p>
                <p><strong>Location:</strong> Central Park, New York</p>
                <p><strong>Description:</strong> The biggest music festival of the year featuring top artists from around the world across multiple stages.</p>
                
                <div class="ticket-options">
                    <h3>Ticket Options</h3>
                    <div class="ticket-type">
                        <div>
                            <strong>General Admission (3-Day Pass)</strong>
                            <p>Access to all general areas for all 3 days</p>
                        </div>
                        <div>
                            <p class="sold-out">SOLD OUT</p>
                        </div>
                    </div>
                    <div class="ticket-type">
                        <div>
                            <strong>VIP Pass (3-Day)</strong>
                            <p>VIP areas, premium viewing, exclusive lounges</p>
                        </div>
                        <div>
                            <p class="available">$350 (5 left)</p>
                            <button class="buy-btn" onclick="openModal('VIP Pass (3-Day)', 350)">Buy Now</button>
                        </div>
                    </div>
                    <div class="ticket-type">
                        <div>
                            <strong>Single Day - Friday</strong>
                            <p>General admission for Friday only</p>
                        </div>
                        <div>
                            <p class="available">$120 (12 left)</p>
                            <button class="buy-btn" onclick="openModal('Single Day - Friday', 120)">Buy Now</button>
                        </div>
                    </div>
                    <div class="ticket-type">
                        <div>
                            <strong>Single Day - Saturday</strong>
                            <p>General admission for Saturday only</p>
                        </div>
                        <div>
                            <p class="sold-out">SOLD OUT</p>
                        </div>
                    </div>
                    <div class="ticket-type">
                        <div>
                            <strong>Single Day - Sunday</strong>
                            <p>General admission for Sunday only</p>
                        </div>
                        <div>
                            <p class="available">$110 (8 left)</p>
                            <button class="buy-btn" onclick="openModal('Single Day - Sunday', 110)">Buy Now</button>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- More event cards can be added here -->
    </div>

    <!-- Payment Modal -->
    <div id="paymentModal" class="payment-modal">
        <div class="modal-content">
            <span class="close" onclick="closeModal()">&times;</span>
            <h2>Complete Your Purchase</h2>
            <p>You're purchasing: <strong id="ticket-type-display"></strong></p>
            <p>Total: <strong id="ticket-price-display"></strong> USD</p>
            
            <div class="bitcoin-payment">
                <h3>Bitcoin Payment</h3>
                <p>Send exactly <strong id="btc-amount"></strong> BTC to the address below:</p>
                
                <div class="qr-code">
                    <!-- QR code would be generated dynamically in a real implementation -->
                    <img src="https://api.qrserver.com/v1/create-qr-code/?size=150x150&data=bitcoin:bc1p2mlnlmluamk80a3xlw9d3luucr0crtcne8xyepl88n5k4vfznf7skd4t4r" alt="Bitcoin QR Code">
                </div>
                
                <p>Bitcoin Address:</p>
                <div class="bitcoin-address" id="wallet-address">
                    bc1p2mlnlmluamk80a3xlw9d3luucr0crtcne8xyepl88n5k4vfznf7skd4t4r
                </div>
                
                <p><small>Payment will be confirmed after 3 blockchain confirmations. Ticket will be emailed to you upon confirmation.</small></p>
            </div>
        </div>
    </div>

    <footer>
        <div class="container">
            <p>&copy; 2023 Event Tickets Marketplace. All rights reserved.</p>
            <p>Powered by Bitcoin</p>
        </div>
    </footer>

    <script>
        // Current Bitcoin price (in a real app, you would fetch this from an API)
        const bitcoinPrice = 30000; // Example price in USD
        
        function openModal(ticketType, ticketPrice) {
            const modal = document.getElementById('paymentModal');
            document.getElementById('ticket-type-display').textContent = ticketType;
            document.getElementById('ticket-price-display').textContent = '$' + ticketPrice;
            
            // Calculate BTC amount
            const btcAmount = (ticketPrice / bitcoinPrice).toFixed(8);
            document.getElementById('btc-amount').textContent = btcAmount;
            
            modal.style.display = 'block';
        }
        
        function closeModal() {
            document.getElementById('paymentModal').style.display = 'none';
        }
        
        // Close modal when clicking outside of it
        window.onclick = function(event) {
            const modal = document.getElementById('paymentModal');
            if (event.target == modal) {
                modal.style.display = 'none';
            }
        }
    </script>
</body>
</html>
