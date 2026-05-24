<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pratibha's Kitchen - Order Online</title>
    <style>
        * { margin: 0; padding: 0; box-sizing: border-box; font-family: 'Segoe UI', sans-serif; }
        :root {
            --bg: linear-gradient(135deg, #0F172A, #1E1B4B, #312E81);
            --card: linear-gradient(135deg, #1E293B, #334155);
            --text: #fff;
            --text2: #94A3B8;
        }
        body.light {
            --bg: linear-gradient(135deg, #F8FAFC, #E2E8F0, #CBD5E1);
            --card: linear-gradient(135deg, #FFFFFF, #F1F5F9);
            --text: #0F172A;
            --text2: #475569;
        }
        body { background: var(--bg); color: var(--text); min-height: 100vh; transition: 0.3s; }
        .header { background: var(--card); padding: 15px; text-align: center; position: sticky; top: 0; z-index: 100; box-shadow: 0 4px 20px rgba(138,43,226,0.4); }
        .header-btns { display: flex; justify-content: space-between; align-items: center; margin-bottom: 10px; flex-wrap: wrap; gap: 5px; }
        .btn { border: none; color: white; padding: 6px 12px; border-radius: 20px; cursor: pointer; font-weight: 600; font-size: 11px; box-shadow: 0 2px 10px rgba(0,0,0,0.3); }
        .track-btn { background: linear-gradient(45deg, #FF6B6B, #FF8E53); }
        .lang-toggle { background: linear-gradient(45deg, #4ECDC4, #44A08D); padding: 6px 10px; font-size: 10px; }
        .theme-toggle { background: linear-gradient(45deg, #667EEA, #764BA2); }
        .admin-btn { background: linear-gradient(45deg, #FF416C, #FF4B2B); }
        .party-btn { background: linear-gradient(45deg, #F7971E, #FFD200); }
        .chat-btn { background: linear-gradient(45deg, #25D366, #128C7E); }
        .logo-container { margin: 15px 0; position: relative; display: inline-block; }
        .crown { position: absolute; top: -20px; left: 50%; transform: translateX(-50%); font-size: 35px; animation: rotateCrown 3s linear infinite; }
        @keyframes rotateCrown {
            0% { transform: translateX(-50%) rotate(0deg); }
            100% { transform: translateX(-50%) rotate(360deg); }
        }
        .logo-text { font-size: 36px; font-weight: 900; background: linear-gradient(90deg, #FFD700, #FFA500, #FF6347, #FF1493, #8A2BE2, #00CED1); background-size: 200% auto; -webkit-background-clip: text; -webkit-text-fill-color: transparent; animation: glister 3s linear infinite; text-shadow: 0 0 30px rgba(255,215,0,0.5); }
        @keyframes glister {
            0% { background-position: 0% center; }
            100% { background-position: 200% center; }
        }
        .logo-sub { font-size: 16px; color: var(--text2); margin-top: 5px; font-weight: 600; }
        .banner { width: 100%; height: 180px; object-fit: cover; border-radius: 0 0 20px 20px; border: 3px solid; border-image: linear-gradient(45deg, #FF6B6B, #4ECDC4, #45B7D1, #96CEB4, #FFEAA7) 1; margin-top: 10px; }
        .container { padding: 15px; max-width: 700px; margin: auto; }
        .search-bar { width: 100%; padding: 12px; border-radius: 25px; border: 2px solid #475569; background: var(--card); color: var(--text); margin-bottom: 15px; }
        .filter-row { display: flex; gap: 10px; margin-bottom: 15px; flex-wrap: wrap; }
        .filter-btn { padding: 8px 15px; border-radius: 20px; border: none; cursor: pointer; font-weight: 600; }
        .filter-btn.active { box-shadow: 0 15px rgba(255,255,0.5); transform: scale(1.05); }
        .veg-btn { background: #22C55E; color: white; }
        .nonveg-btn { background: #EF4444; color: white; }
        .bestseller-btn { background: linear-gradient(45deg, #F59E0B, #EF4444); color: white; }
        .categories { display: flex; gap: 10px; overflow-x: auto; padding: 10px 0; margin-bottom: 15px; }
        .cat-btn { border: none; color: white; padding: 10px 20px; border-radius: 25px; white-space: nowrap; cursor: pointer; font-weight: 700; transition: 0.3s; }
        .cat-btn[data-cat="all"] { background: linear-gradient(45deg, #FF416C, #FF4B2B); }
        .cat-btn[data-cat="chicken"] { background: linear-gradient(45deg, #F85032, #E73827); }
        .cat-btn[data-cat="rice"] { background: linear-gradient(45deg, #56AB2F, #A8E063); }
        .cat-btn[data-cat="chinese"] { background: linear-gradient(45deg, #F7971E, #FFD200); }
        .cat-btn[data-cat="pizza"] { background: linear-gradient(45deg, #834D9B, #D04ED6); }
        .cat-btn[data-cat="roti"] { background: linear-gradient(45deg, #00C9FF, #92FE9D); }
        .cat-btn[data-cat="snacks"] { background: linear-gradient(45deg, #FC466B, #3F5EFB); }
        .cat-btn[data-cat="maharashtrian"] { background: linear-gradient(45deg, #11998E, #38EF7D); }
        .cat-btn[data-cat="pavbhaji"] { background: linear-gradient(45deg, #FF512F, #F09819); }
        .cat-btn.active { transform: scale(1.1); box-shadow: 0 4px 15px rgba(255,255,0.4); }
        .products { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; min-height: 200px; }
        .product-card { border-radius: 15px; overflow: hidden; box-shadow: 0 4px 15px rgba(0,0,0,0.3); transition: 0.3s; position: relative; }
        .product-card:hover { transform: translateY(-5px); }
        .product-card img { width: 100%; height: 140px; object-fit: cover; }
        .veg-dot { position: absolute; top: 10px; left: 10px; width: 20px; height: 20px; border: 2px solid; background: white; display: flex; align-items: center; justify-content: center; }
        .veg-dot.veg { border-color: #22C55E; }
        .veg-dot.nonveg { border-color: #EF4444; }
        .veg-dot span { width: 10px; height: 10px; border-radius: 50%; }
        .veg-dot.veg span { background: #22C55E; }
        .veg-dot.nonveg span { background: #EF4444; }
        .bestseller { position: absolute; top: 10px; right: 10px; background: linear-gradient(45deg, #F59E0B, #EF4444); color: white; padding: 4px 8px; border-radius: 10px; font-size: 10px; font-weight: 800; }
        .product-info { padding: 12px; }
        .product-name { font-weight: 700; font-size: 15px; margin-bottom: 5px; line-height: 1.2; }
        .product-price { color: #00FF88; font-weight: 800; font-size: 18px; margin-bottom: 5px; text-shadow: 0 0 10px rgba(0,255,136,0.5); }
        .rating { color: #FBBF24; font-size: 12px; margin-bottom: 10px; cursor: pointer; }
        .spice-select { width: 100%; padding: 5px; border-radius: 5px; background: var(--card); color: var(--text); border: 1px solid #475569; margin-bottom: 8px; font-size: 12px; }
        .item-note { width: 100%; padding: 5px; border-radius: 5px; background: var(--card); color: var(--text); border: 1px solid #475569; margin-bottom: 8px; font-size: 11px; }
        .add-btn { width: 100%; background: linear-gradient(45deg, #667EEA, #764BA2); border: none; color: white; padding: 10px; border-radius: 8px; font-weight: 700; cursor: pointer; box-shadow: 0 2px 10px rgba(102,126,234,0.5); }
        .cart-bar { position: fixed; bottom: 0; left: 0; right: 0; background: var(--card); padding: 15px; display: none; justify-content: space-between; align-items: center; box-shadow: 0 -4px 20px rgba(138,43,226,0.4); z-index: 99; border-top: 2px solid; border-image: linear-gradient(90deg, #FF6B6B, #4ECDC4, #45B7D1) 1; }
        .cart-bar.show { display: flex; }
        .view-cart-btn { background: linear-gradient(45deg, #00F260, #0575E6); color: white; border: none; padding: 12px 25px; border-radius: 25px; font-weight: 800; cursor: pointer; box-shadow: 0 2px 15px rgba(0,242,96,0.5); }
        .modal { display: none; position: fixed; top: 0; left: 0; width: 100%; height: 100%; background: rgba(15,23,42,0.95); z-index: 200; justify-content: center; align-items: center; }
        .modal.show { display: flex; }
        .modal-content { background: var(--card); width: 90%; max-width: 600px; max-height: 90vh; border-radius: 20px; padding: 20px; overflow-y: auto; border: 2px solid; border-image: linear-gradient(45deg, #FF6B6B, #4ECDC4, #45B7D1, #96CEB4) 1; }
        .modal-header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 20px; }
        .close-btn { background: linear-gradient(45deg, #FF416C, #FF4B2B); border: none; color: white; font-size: 28px; cursor: pointer; width: 40px; height: 40px; border-radius: 50%; }
        .cart-item { display: flex; justify-content: space-between; align-items: center; margin-bottom: 15px; padding: 10px; border-radius: 10px; background: rgba(255,255,255,0.05); }
        .qty-control { display: flex; align-items: center; gap: 10px; }
        .qty-btn { background: linear-gradient(45deg, #667EEA, #764BA2); border: none; color: white; width: 30px; height: 30px; border-radius: 50%; cursor: pointer; font-weight: 700; }
        .form-input { width: 100%; padding: 12px; border-radius: 10px; border: 2px solid #475569; background: var(--bg); color: var(--text); margin-bottom: 15px; }
        .form-input:focus { border-image: linear-gradient(45deg, #FF6B6B, #4ECDC4) 1; outline: none; }
        .place-order-btn { width: 100%; background: linear-gradient(45deg, #00F260, #0575E6, #764BA2); color: white; border: none; padding: 15px; border-radius: 12px; font-weight: 800; font-size: 18px; cursor: pointer; margin-top: 10px; box-shadow: 0 4px 15px rgba(0,242,96,0.4); }
        .coupon-box { display: flex; gap: 10px; margin: 15px 0; }
        .coupon-box input { flex: 1; margin: 0; }
        .apply-btn { width: auto; padding: 12px 20px; background: linear-gradient(45deg, #F7971E, #FFD200); }
        .discount-text { color: #00FF88; font-weight: 700; margin: 10px 0; text-shadow: 0 0 10px rgba(0,255,136,0.5); }
        .total-row { display: flex; justify-content: space-between; margin: 8px 0; }
        .total-row.final { border-top: 2px solid; border-image: linear-gradient(90deg, #FF6B6B, #4ECDC4) 1; padding-top: 10px; font-size: 20px; font-weight: 800; }
        .cod-text { text-align: center; background: linear-gradient(90deg, #FFD700, #FFA500); -webkit-background-clip: text; -webkit-text-fill-color: transparent; font-weight: 800; margin: 10px 0; font-size: 16px; }
        .loyalty-box { background: linear-gradient(45deg, #F7971E, #FFD200); padding: 10px; border-radius: 10px; text-align: center; margin: 10px 0; color: #0F172A; font-weight: 700; }
        .status-badge { padding: 5px 10px; border-radius: 15px; font-size: 11px; font-weight: 700; }
        .status-Placed { background: #3B82F6; }
        .status-Preparing { background: #F59E0B; }
        .status-Out\ for\ Delivery { background: #8B5CF6; }
        .status-Delivered { background: #10B981; }
        .admin-table { width: 100%; border-collapse: collapse; margin-top: 15px; font-size: 12px; }
        .admin-table th, .admin-table td { padding: 8px; border: 1px solid #475569; text-align: left; }
        .admin-table th { background: #334155; }
        .chart { display: flex; align-items: flex-end; height: 150px; gap: 10px; margin: 20px 0; }
        .bar { flex: 1; background: linear-gradient(180deg, #667EEA, #764BA2); border-radius: 5px 5px 0 0; position: relative; }
        .bar-label { position: absolute; bottom: -20px; width: 100%; text-align: center; font-size: 10px; }
        .min-order-warning { background: #EF4444; color: white; padding: 10px; border-radius: 10px; text-align: center; margin: 10px 0; display: none; }
        .min-order-warning.show { display: block; }
        .combo-builder { background: rgba(139,92,246,0.2); padding: 15px; border-radius: 15px; margin: 15px 0; border: 2px dashed #8B5CF6; }
        .rating-modal { text-align: center; }
        .stars { font-size: 40px; margin: 20px 0; }
        .star { cursor: pointer; color: #475569; }
        .star.active { color: #FBBF24; }
    </style>
</head>
<body>
    <div class="header">
        <div class="header-btns">
            <button class="btn track-btn" onclick="openModal('trackModal')">Track</button>
            <button class="btn lang-toggle" onclick="toggleLang()">मराठी</button>
            <button class="btn theme-toggle" onclick="toggleTheme()">🌙</button>
            <button class="btn party-btn" onclick="openModal('partyModal')">Party Order</button>
            <button class="btn chat-btn" onclick="openChat()">💬 Chat</button>
            <button class="btn admin-btn" onclick="openAdmin()">Admin</button>
        </div>
        <div class="logo-container">
            <div class="crown">👑</div>
            <div class="logo-text">PRATIBHA'S</div>
            <div class="logo-sub">KITCHEN ✨</div>
        </div>
        <img src="https://i.postimg.cc/PJqW3h8f/banner.jpg" class="banner" alt="Banner">
    </div>

    <div class="container">
        <input type="text" class="search-bar" id="searchBar" placeholder="Search dishes..." onkeyup="searchItems()">
        <div class="filter-row">
            <button class="filter-btn veg-btn" onclick="filterVeg(true)">🟢 Veg</button>
            <button class="filter-btn nonveg-btn" onclick="filterVeg(false)">🔴 Non-Veg</button>
            <button class="filter-btn bestseller-btn" onclick="filterBestseller()">🔥 Bestseller</button>
            <button class="filter-btn" style="background:#8B5CF6;color:white" onclick="openModal('comboModal')">🎁 Build Combo</button>
        </div>
        <div id="loyaltyBox" class="loyalty-box" style="display:none"></div>
        <div class="categories" id="categories"></div>
        <div class="products" id="products"></div>
    </div>

    <div class="cart-bar" id="cartBar">
        <div><span id="cartCount">0</span> Items | ₹<span id="cartTotal">0</span></div>
        <button class="view-cart-btn" onclick="openModal('cartModal')">View Cart</button>
    </div>

    <div class="modal" id="cartModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Your Cart</h2>
                <button class="close-btn" onclick="closeModal('cartModal')">&times;</button>
            </div>
            <div id="minOrderWarning" class="min-order-warning">Minimum order Rs 150 for delivery</div>
            <div id="cartItems"></div>
            <div class="coupon-box">
                <input type="text" class="form-input" id="couponCode" placeholder="Coupon / Loyalty Points">
                <button class="apply-btn place-order-btn" onclick="applyCoupon()">Apply</button>
            </div>
            <div id="discountText" class="discount-text"></div>
            <div class="total-row"><span>Subtotal</span><span>Rs <span id="subtotal">0</span></span></div>
            <div class="total-row"><span>Delivery</span><span>Rs 40</span></div>
            <div class="total-row final"><span>Total</span><span>Rs <span id="finalTotal">40</span></span></div>
            <div class="cod-text">💵 Cash on Delivery Only</div>
            <input type="text" class="form-input" id="custName" placeholder="Your Name">
            <input type="text" class="form-input" id="custPhone" placeholder="Phone Number">
            <textarea class="form-input" id="custAddress" placeholder="Full Address" rows="3"></textarea>
            <button class="place-order-btn" onclick="placeOrder()">Place Order on WhatsApp</button>
            <button class="place-order-btn" style="background:linear-gradient(45deg,#3B82F6,#1D4ED8)" onclick="downloadBill()">📄 Download Bill</button>
        </div>
    </div>

    <div class="modal" id="trackModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Track Order / History</h2>
                <button class="close-btn" onclick="closeModal('trackModal')">&times;</button>
            </div>
            <input type="text" class="form-input" id="trackPhone" placeholder="Enter Your Phone Number">
            <button class="place-order-btn" onclick="trackOrder()">Track</button>
            <div id="trackResult" style="margin-top:20px;"></div>
        </div>
    </div>

    <div class="modal" id="partyModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Party/Bulk Order 🎉</h2>
                <button class="close-btn" onclick="closeModal('partyModal')">&times;</button>
            </div>
            <p style="margin-bottom:15px;color:var(--text2)">20+ लोकांसाठी Order? आम्हाला कळवा!</p>
            <input type="text" class="form-input" id="partyName" placeholder="Your Name">
            <input type="text" class="form-input" id="partyPhone" placeholder="Phone Number">
            <input type="number" class="form-input" id="partyCount" placeholder="Number of People (Min 20)">
            <input type="date" class="form-input" id="partyDate">
            <textarea class="form-input" id="partyItems" rows="4" placeholder="कोणते पदार्थ हवेत? अंदाजे Quantity लिहा"></textarea>
            <textarea class="form-input" id="partyAddress" rows="3" placeholder="Delivery Address / Venue"></textarea>
            <button class="place-order-btn" onclick="placePartyOrder()">Send Party Order Request</button>
        </div>
    </div>

    <div class="modal" id="comboModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Build Your Combo 🎁</h2>
                <button class="close-btn" onclick="closeModal('comboModal')">&times;</button>
            </div>
            <p style="margin-bottom:15px;color:var(--text2)">कोणतेही 3 Items निवडा - 10% Off मिळवा!</p>
            <div id="comboItems" style="max-height:300px;overflow-y:auto;"></div>
            <div class="total-row final" style="margin-top:15px;"><span>Combo Total</span><span>Rs <span id="comboTotal">0</span></span></div>
            <button class="place-order-btn" onclick="addComboToCart()">Add Combo to Cart</button>
        </div>
    </div>

    <div class="modal" id="adminModal">
        <div class="modal-content">
            <div class="modal-header">
                <h2>Admin Panel 🔐</h2>
                <button class="close-btn" onclick="closeModal('adminModal')">&times;</button>
            </div>
            <div id="adminLogin">
                <input type="password" class="form-input" id="adminPass" placeholder="Enter Password">
                <button class="place-order-btn" onclick="adminLogin()">Login</button>
            </div>
            <div id="adminPanel" style="display:none">
                <h3 style="margin:15px 0">📊 Analytics</h3>
                <div id="analytics"></div>
                <div class="chart" id="chart"></div>
                <h3 style="margin:15px 0">📦 Orders</h3>
                <div id="adminOrders" style="max-height:200px;overflow-y:auto;"></div>
                <h3 style="margin:15px 0">➕ Add/Edit Item</h3>
                <input type="number" class="form-input" id="editId" placeholder="Item ID (leave blank for new)">
                <input type="text" class="form-input" id="editName" placeholder="Name">
                <input type="text" class="form-input" id="editNameMr" placeholder="नाव (Marathi)">
                <input type="number" class="form-input" id="editPrice" placeholder="Price">
                <input type="text" class="form-input" id="editImg" placeholder="Image URL">
                <select class="form-input" id="editCat">
                    <option value="chicken">Chicken</option>
                    <option value="rice">Rice & Khichdi</option>
                    <option value="chinese">Chinese & Momos</option>
                    <option value="pavbhaji">Pav Bhaji</option>
                    <option value="pizza">Pizza & Pasta</option>
                    <option value="roti">Roti & Paratha</option>
                    <option value="snacks">Snacks</option>
                    <option value="maharashtrian">Maharashtrian</option>
                </select>
                <select class="form-input" id="editVeg">
                    <option value="true">Veg</option>
                    <option value="false">Non-Veg</option>
<script>
    const YOUR_WHATSAPP = "917021581312";
    const YOUR_NAME = "SANTOSH";
    const ADMIN_PASS = "pratibha123";
    const MIN_ORDER = 150;

    let currentLang = 'en';
    let cart = [];
    let activeCategory = 'all';
    let appliedCoupon = null;
    let discountAmount = 0;
    let filterType = 'all';
    let searchQuery = '';
    let comboSelection = [];
    let isDarkMode = true;
    let currentRatingItem = null;
    let currentRating = 0;

    let users = JSON.parse(localStorage.getItem('users')) || {};
    let currentUser = JSON.parse(localStorage.getItem('currentUser')) || null;
    let orders = JSON.parse(localStorage.getItem('orders')) || [];
    let ratings = JSON.parse(localStorage.getItem('ratings')) || {};
    let menuItems = JSON.parse(localStorage.getItem('menuItems')) || [];

    if(menuItems.length === 0) {
        menuItems = [
            { id: 1, name: "Chicken Biryani", nameMr: "चिकन बिर्याणी", price: 250, img: "https://i.postimg.cc/bSYBhqpz/Pratibha-special-thali-jpg.jpg", cat: 'chicken', veg: false, bestseller: true, rating: 4.8, ratingCount: 120 },
            { id: 2, name: "Chicken Curry", nameMr: "चिकन करी", price: 220, img: "https://i.postimg.cc/G8x5V4wn/chicken-curry-jpg.jpg", cat: 'chicken', veg: false, bestseller: false, rating: 4.5, ratingCount: 85 },
            { id: 3, name: "Chicken 65 (200 gm)", nameMr: "चिकन 65 (200 ग्रॅम)", price: 165, img: "https://i.postimg.cc/PPTtCDrC/Chicken-65-jpg.jpg", cat: 'chicken', veg: false, bestseller: true, rating: 4.7, ratingCount: 95 },
            { id: 4, name: "Pratibha Special Chicken Thali", nameMr: "प्रतिभा स्पेशल चिकन थाळी", price: 444, img: "https://i.postimg.cc/bSYBhqpz/Pratibha-special-thali-jpg.jpg", cat: 'chicken', veg: false, bestseller: true, rating: 4.9, ratingCount: 200 },
            { id: 5, name: "Dal Khichdi", nameMr: "डाळ खिचडी", price: 130, img: "https://i.postimg.cc/MMmFNn22/Dal-Khichdi-jpg.jpg", cat: 'rice', veg: true, bestseller: false, rating: 4.3, ratingCount: 60 },
            { id: 6, name: "Veg Fried Rice", nameMr: "व्हेज फ्राईड राईस", price: 150, img: "https://i.postimg.cc/hz156XWB/Chiken-fried-rice.jpg", cat: 'rice', veg: true, bestseller: false, rating: 4.4, ratingCount: 70 },
            { id: 7, name: "Chicken Fried Rice", nameMr: "चिकन फ्राईड राईस", price: 180, img: "https://i.postimg.cc/hz156XWB/Chiken-fried-rice.jpg", cat: 'rice', veg: false, bestseller: false, rating: 4.6, ratingCount: 80 },
            { id: 8, name: "Kadhi Pakoda Rice", nameMr: "कढी पकोडा राईस", price: 110, img: "https://i.postimg.cc/MMmFNn22/Dal-Khichdi-jpg.jpg", cat: 'rice', veg: true, bestseller: false, rating: 4.2, ratingCount: 45 },
            { id: 9, name: "Sabudana Khichdi", nameMr: "साबुदाणा खिचडी", price: 60, img: "https://i.postimg.cc/MMmFNn22/Dal-Khichdi-jpg.jpg", cat: 'rice', veg: true, bestseller: false, rating: 4.1, ratingCount: 40 },
            { id: 10, name: "Sabudana Vada (2 pcs)", nameMr: "साबुदाणा वडा (2 नग)", price: 70, img: "https://i.postimg.cc/ygybtDq5/Sabudana-vada-jpg.jpg", cat: 'rice', veg: true, bestseller: false, rating: 4.3, ratingCount: 55 },
            { id: 11, name: "Veg Chowmein Hakka Noodles", nameMr: "व्हेज चाऊमीन हक्का नुडल्स", price: 120, img: "https://i.postimg.cc/Vdfd3pt3/hakka-noodles-veg-jpg.jpg", cat: 'chinese', veg: true, bestseller: false, rating: 4.4, ratingCount: 65 },
            { id: 12, name: "Veg Manchurian", nameMr: "व्हेज मंचुरियन", price: 99, img: "https://i.postimg.cc/Vdfd3pt3/hakka-noodles-veg-jpg.jpg", cat: 'chinese', veg: true, bestseller: true, rating: 4.6, ratingCount: 90 },
            { id: 13, name: "Steam Veg Momos (8 pcs)", nameMr: "स्टीम व्हेज मोमोज (8 नग)", price: 110, img: "https://i.postimg.cc/Q93zfpz2/fried-momo-jpg.jpg", cat: 'chinese', veg: true, bestseller: false, rating: 4.5, ratingCount: 75 },
            { id: 14, name: "Fry Veg Momos (8 pcs)", nameMr: "फ्राय व्हेज मोमोज (8 नग)", price: 130, img: "https://i.postimg.cc/Q93zfpz2/fried-momo-jpg.jpg", cat: 'chinese', veg: true, bestseller: false, rating: 4.5, ratingCount: 75 },
            { id: 15, name: "Butter Pav Bhaji", nameMr: "बटर पावभाजी", price: 140, img: "https://i.postimg.cc/zbFc6ymQ/pavbhaji-jpg.jpg", cat: 'pavbhaji', veg: true, bestseller: true, rating: 4.7, ratingCount: 150 },
            { id: 16, name: "Cheese Pav Bhaji", nameMr: "चीज पावभाजी", price: 160, img: "https://i.postimg.cc/LYpWxzWG/cheese-pav-bhaji.jpg", cat: 'pavbhaji', veg: true, bestseller: true, rating: 4.8, ratingCount: 160 },
            { id: 17, name: "Extra Pav", nameMr: "एक्स्ट्रा पाव", price: 15, img: "https://i.postimg.cc/zbFc6ymQ/pavbhaji-jpg.jpg", cat: 'pavbhaji', veg: true, bestseller: false, rating: 4.0, ratingCount: 20 },
            { id: 18, name: "Pan Veg Pizza", nameMr: "पॅन व्हेज पिझ्झा", price: 140, img: "https://i.postimg.cc/tZNMws0L/paneer-pan-pizza-jpg.jpg", cat: 'pizza', veg: true, bestseller: false, rating: 4.4, ratingCount: 70 },
            { id: 19, name: "Corn Pizza", nameMr: "कॉर्न पिझ्झा", price: 140, img: "https://i.postimg.cc/nCpDnMy1/corn-pan-pizza.jpg", cat: 'pizza', veg: true, bestseller: false, rating: 4.3, ratingCount: 60 },
            { id: 20, name: "Onion Pizza", nameMr: "कांदा पिझ्झा", price: 99, img: "https://i.postimg.cc/cr0nd6pm/onion-pan-pizza-jpg.jpg", cat: 'pizza', veg: true, bestseller: false, rating: 4.2, ratingCount: 50 },
            { id: 21, name: "Paneer Pizza", nameMr: "पनीर पिझ्झा", price: 170, img: "https://i.postimg.cc/tZNMws0L/paneer-pan-pizza-jpg.jpg", cat: 'pizza', veg: true, bestseller: true, rating: 4.7, ratingCount: 110 },
            { id: 22, name: "Red Sauce Pasta", nameMr: "रेड सॉस पास्ता", price: 120, img: "https://i.postimg.cc/1nrj28xJ/red-sauce-pasta-jpg.jpg", cat: 'pizza', veg: true, bestseller: false, rating: 4.5, ratingCount: 80 },
            { id: 23, name: "Aloo Paratha", nameMr: "आलू पराठा", price: 60, img: "https://i.postimg.cc/kBqb7D0s/Jwari-Bhakri-jpg.jpg", cat: 'roti', veg: true, bestseller: false, rating: 4.4, ratingCount: 65 },
            { id: 24, name: "Cheese Aloo Paratha", nameMr: "चीज आलू पराठा", price: 80, img: "https://i.postimg.cc/kBqb7D0s/Jwari-Bhakri-jpg.jpg", cat: 'roti', veg: true, bestseller: true, rating: 4.6, ratingCount: 85 },
            { id: 25, name: "Chapati (per pc)", nameMr: "चपाती (प्रति नग)", price: 15, img: "https://i.postimg.cc/kBqb7D0s/Jwari-Bhakri-jpg.jpg", cat: 'roti', veg: true, bestseller: false, rating: 4.0, ratingCount: 30 },
            { id: 26, name: "Jowar Bhakri (per pc)", nameMr: "ज्वारीची भाकरी (प्रति नग)", price: 30, img: "https://i.postimg.cc/kBqb7D0s/Jwari-Bhakri-jpg.jpg", cat: 'roti', veg: true, bestseller: false, rating: 4.3, ratingCount: 50 },
            { id: 27, name: "Veg Cheese Sandwich", nameMr: "व्हेज चीज सँडविच", price: 60, img: "https://i.postimg.cc/1nrj28xv/vada-paav.jpg", cat: 'snacks', veg: true, bestseller: false, rating: 4.2, ratingCount: 45 },
            { id: 28, name: "Vada Pav (2 pcs)", nameMr: "वडा पाव (2 नग)", price: 50, img: "https://i.postimg.cc/1nrj28xv/vada-paav.jpg", cat: 'snacks', veg: true, bestseller: true, rating: 4.8, ratingCount: 200 },
            { id: 29, name: "Patties (2 pcs)", nameMr: "पॅटीस (2 नग)", price: 50, img: "https://i.postimg.cc/1nrj28xv/vada-paav.jpg", cat: 'snacks', veg: true, bestseller: false, rating: 4.1, ratingCount: 35 },
            { id: 30, name: "Pohe", nameMr: "पोहे", price: 40, img: "https://i.postimg.cc/MMmFNn22/Dal-Khichdi-jpg.jpg", cat: 'snacks', veg: true, bestseller: false, rating: 4.3, ratingCount: 55 },
            { id: 31, name: "Upma", nameMr: "उप्पीट / उपमा", price: 40, img: "https://i.postimg.cc/MMmFNn22/Dal-Khichdi-jpg.jpg", cat: 'snacks', veg: true, bestseller: false, rating: 4.2, ratingCount: 40 },
            { id: 32, name: "Puri Bhaji", nameMr: "पुरी भाजी", price: 80, img: "https://i.postimg.cc/1nrj28xv/vada-paav.jpg", cat: 'snacks', veg: true, bestseller: false, rating: 4.4, ratingCount: 60 },
            { id: 33, name: "Aamras Puri (Seasonal)", nameMr: "आमरस पुरी (हंगामांनुसार)", price: 150, img: "https://i.postimg.cc/1nrj28xv/vada-paav.jpg", cat: 'snacks', veg: true, bestseller: false, rating: 4.6, ratingCount: 70 },
            { id: 34, name: "Korean Cheese Potato Balls", nameMr: "कोरियन चीज पोटॅटो क्रिस्पी बॉल्स", price: 149, img: "https://i.postimg.cc/WqpHvsTT/korian-cheese-potato-balls.jpg", cat: 'snacks', veg: true, bestseller: true, rating: 4.7, ratingCount: 90 },
            { id: 35, name: "Dahi Dhapathe", nameMr: "दही धपाटे", price: 60, img: "https://i.postimg.cc/kBqb7D0s/Jwari-Bhakri-jpg.jpg", cat: 'maharashtrian', veg: true, bestseller: false, rating: 4.3, ratingCount: 50 },
            { id: 36, name: "Kothimbir Vadi (200 gm)", nameMr: "कोथिंबीर वडी (200 ग्रॅम)", price: 90, img: "https://i.postimg.cc/ygybtDq5/Sabudana-vada-jpg.jpg", cat: 'maharashtrian', veg: true, bestseller: false, rating: 4.4, ratingCount: 60 },
            { id: 37, name: "Methi Vadi (200 gm)", nameMr: "मेथी वडी (200 ग्रॅम)", price: 90, img: "https://i.postimg.cc/ygybtDq5/Sabudana-vada-jpg.jpg", cat: 'maharashtrian', veg: true, bestseller: false, rating: 4.3, ratingCount: 55 },
            { id: 38, name: "Palak Vadi (200 gm)", nameMr: "पालक वडी (200 ग्रॅम)", price: 90, img: "https://i.postimg.cc/ygybtDq5/Sabudana-vada-jpg.jpg", cat: 'maharashtrian', veg: true, bestseller: false, rating: 4.3, ratingCount: 50 },
            { id: 39, name: "Gulab Jamun", nameMr: "गुलाबजाम", price: 60, img: "https://i.postimg.cc/BLBVkjWV/Gulabjam-jpg.jpg", cat: 'snacks', veg: true, bestseller: false, rating: 4.5, ratingCount: 75 }
        ];
        localStorage.setItem('menuItems', JSON.stringify(menuItems));
    }

    const categories = [
        {id: 'all', name: 'All', nameMr: 'सर्व'},
        {id: 'chicken', name: 'Chicken', nameMr: 'चिकन'},
        {id: 'rice', name: 'Rice & Khichdi', nameMr: 'भात खिचडी'},
        {id: 'chinese', name: 'Chinese & Momos', nameMr: 'चायनीज मोमोज'},
        {id: 'pavbhaji', name: 'Pav Bhaji', nameMr: 'पाव भाजी'},
        {id: 'pizza', name: 'Pizza & Pasta', nameMr: 'पिझ्झा पास्ता'},
        {id: 'roti', name: 'Roti & Paratha', nameMr: 'पोळी पराठे'},
        {id: 'snacks', name: 'Snacks', nameMr: 'स्नॅक्स'},
        {id: 'maharashtrian', name: 'Maharashtrian', nameMr: 'महाराष्ट्रीयन'}
    ];

    const cardColors = [
        'linear-gradient(135deg, #667EEA, #764BA2)', 'linear-gradient(135deg, #F093FB, #F5576C)', 'linear-gradient(135deg, #4FACFE, #00F2FE)',
        'linear-gradient(135deg, #43E97B, #38F9D7)', 'linear-gradient(135deg, #FA709A, #FEE140)', 'linear-gradient(135deg, #30CFD0, #330867)',
        'linear-gradient(135deg, #A8EDEA, #FED6E3)', 'linear-gradient(135deg, #F5F7FA, #C3CFE2)', 'linear-gradient(135deg, #E0C3FC, #8EC5FC)',
        'linear-gradient(135deg, #F093FB, #F5576C)', 'linear-gradient(135deg, #FFECD2, #FCB69F)', 'linear-gradient(135deg, #FF9A9E, #FECFEF)'
    ];

    const coupons = { 'FIRST50': { discount: 50, type: 'flat' }, 'SAVE20': { discount: 20, type: 'percent' }, 'POINTS50': { discount: 50, type: 'points' } };

    function init() {
        if(currentUser) {
            document.getElementById('custName').value = currentUser.name;
            document.getElementById('custPhone').value = currentUser.phone;
            updateLoyaltyBox();
        }
        renderCategories();
        renderProducts();
        updateCartBar();
    }

    function renderCategories() {
        const catDiv = document.getElementById('categories');
        catDiv.innerHTML = categories.map(c => `<button class="cat-btn ${c.id === activeCategory? 'active' : ''}" data-cat="${c.id}" onclick="setCategory('${c.id}')">${currentLang === 'en'? c.name : c.nameMr}</button>`).join('');
    }

    function setCategory(id) {
        activeCategory = id;
        renderCategories();
        renderProducts();
    }

    function searchItems() {
        searchQuery = document.getElementById('searchBar').value.toLowerCase();
        renderProducts();
    }

    function filterVeg(isVeg) {
        filterType = isVeg? 'veg' : 'nonveg';
        document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
        event.target.classList.add('active');
        renderProducts();
    }

    function filterBestseller() {
        filterType = 'bestseller';
        document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
        event.target.classList.add('active');
        renderProducts();
    }

    function renderProducts() {
        let filtered = menuItems.filter(item => {
            let match = true;
            if (activeCategory!== 'all') match = item.cat === activeCategory;
            if (filterType === 'veg') match = match && item.veg;
            if (filterType === 'nonveg') match = match &&!item.veg;
            if (filterType === 'bestseller') match = match && item.bestseller;
            if (searchQuery) match = match && (item.name.toLowerCase().includes(searchQuery) || item.nameMr.includes(searchQuery));
            return match;
        });

        const productsDiv = document.getElementById('products');
        productsDiv.innerHTML = filtered.map((item, index) => `
            <div class="product-card" style="background: ${cardColors[index % cardColors.length]}">
                <div class="veg-dot ${item.veg? 'veg' : 'nonveg'}"><span></div>
                ${item.bestseller? '<div class="bestseller">Popular</div>' : ''}
                <img src="${item.img}" alt="${item.name}">
                <div class="product-info">
                    <div class="product-name">${currentLang === 'en'? item.name : item.nameMr}</div>
                    <div class="product-price">Rs ${item.price}</div>
                    <div class="rating" onclick="openRating(${item.id})">⭐ ${item.rating} (${item.ratingCount})</div>
                    <select class="spice-select" id="spice-${item.id}">
                        <option value="">Spice Level</option>
                        <option value="Mild">Mild</option>
                        <option value="Medium">Medium</option>
                        <option value="Hot">Hot</option>
                    </select>
                    <input type="text" class="item-note" id="note-${item.id}" placeholder="Notes: Extra cheese, No onion...">
                    <button class="add-btn" onclick="addToCart(${item.id})">Add to Cart</button>
                </div>
            </div>
        `).join('');
    }

    function addToCart(id) {
        const item = menuItems.find(i => i.id === id);
        const spice = document.getElementById(`spice-${id}`).value;
        const note = document.getElementById(`note-${id}`).value;
        const cartId = `${id}-${spice}-${note}`;
        const existing = cart.find(i => i.cartId === cartId);
        if (existing) { existing.qty++; }
        else { cart.push({...item, qty: 1, spice, note, cartId}); }
        updateCartBar();
    }

    function updateCartBar() {
        const count = cart.reduce((sum, i) => sum + i.qty, 0);
        const total = cart.reduce((sum, i) => sum + (i.price * i.qty), 0);
        document.getElementById('cartCount').textContent = count;
        document.getElementById('cartTotal').textContent = total;
        document.getElementById('cartBar').classList.toggle('show', count > 0);
    }

    function renderCart() {
        document.getElementById('cartItems').innerHTML = cart.map(item => `
            <div class="cart-item">
                <div>
                    <div style="font-weight:700">${currentLang === 'en'? item.name : item.nameMr}</div>
                    ${item.spice? `<div style="font-size:11px;color:var(--text2)">Spice: ${item.spice}</div>` : ''}
                    ${item.note? `<div style="font-size:11px;color:var(--text2)">Note: ${item.note}</div>` : ''}
                    <div style="color:#00FF88">Rs ${item.price}</div>
                </div>
                <div class="qty-control">
                    <button class="qty-btn" onclick="changeQty('${item.cartId}', -1)">-</button>
                    <span>${item.qty}</span>
                    <button class="qty-btn" onclick="changeQty('${item.cartId}', 1)">+</button>
                </div>
            </div>
        `).join('');
        updateTotals();
    }

    function changeQty(cartId, delta) {
        const item = cart.find(i => i.cartId === cartId);
        item.qty += delta;
        if (item.qty <= 0) cart = cart.filter(i => i.cartId!== cartId);
        renderCart();
        updateCartBar();
    }

    function applyCoupon() {
        const code = document.getElementById('couponCode').value.toUpperCase();
        const subtotal = cart.reduce((sum, i) => sum + (i.price * i.qty), 0);

        if (coupons[code]) {
            if(coupons[code].type === 'points') {
                if(!currentUser || currentUser.points < 100) {
                    document.getElementById('discountText').textContent = 'Not enough points! Need 100 points.';
                    return;
                }
                discountAmount = 50;
                appliedCoupon = 'POINTS50';
            } else {
                appliedCoupon = code;
                discountAmount = coupons[code].type === 'flat'? coupons[code].discount : Math.round(subtotal * coupons[code].discount / 100);
            }
            document.getElementById('discountText').textContent = `Coupon Applied! You saved Rs ${discountAmount}`;
        } else {
            document.getElementById('discountText').textContent = 'Invalid Coupon';
            discountAmount = 0;
            appliedCoupon = null;
        }
        updateTotals();
    }

    function updateTotals() {
        const subtotal = cart.reduce((sum, i) => sum + (i.price * i.qty), 0);
        const final = subtotal + 40 - discountAmount;
        document.getElementById('subtotal').textContent = subtotal;
        document.getElementById('finalTotal').textContent = final;
        document.getElementById('minOrderWarning').classList.toggle('show', subtotal < MIN_ORDER);
    }

    function openModal(id) {
        if (id === 'cartModal') renderCart();
        if (id === 'comboModal') renderComboBuilder();
        document.getElementById(id).classList.add('show');
    }

    function closeModal(id) {
        document.getElementById(id).classList.remove('show');
    }

    function placeOrder() {
        const name = document.getElementById('custName').value;
        const phone = document.getElementById('custPhone').value;
        const address = document.getElementById('custAddress').value;
        const subtotal = cart.reduce((sum, i) => sum + (i.price * i.qty), 0);

        if (!name ||!phone ||!address || cart.length === 0) {
            alert('Please fill all details and add items to cart');
            return;
        }
        if (subtotal < MIN_ORDER) {
            alert(`Minimum order amount is Rs ${MIN_ORDER}`);
            return;
        }

        if(!currentUser || currentUser.phone!== phone) {
            currentUser = { name, phone, points: users[phone]?.points || 0 };
            users[phone] = currentUser;
            localStorage.setItem('users', JSON.stringify(users));
            localStorage.setItem('currentUser', JSON.stringify(currentUser));
        }

        if(appliedCoupon === 'POINTS50') {
            currentUser.points -= 100;
            users[phone] = currentUser;
            localStorage.setItem('users', JSON.stringify(users));
            localStorage.setItem('currentUser', JSON.stringify(currentUser));
        }

        const final = subtotal + 40 - discountAmount;
        let msg = `*New Order from ${YOUR_NAME}*\n\n`;
        msg += `*Customer:* ${name}\n*Phone:* ${phone}\n*Address:* ${address}\n\n*Items:*\n`;
        cart.forEach(i => {
            msg += `${i.qty} x ${i.name}`;
            if(i.spice) msg += ` (${i.spice})`;
            if(i.note) msg += ` [${i.note}]`;
            msg += ` = Rs ${i.price * i.qty}\n`;
        });
        msg += `\n*Subtotal:*        const discount = Math.round(total * 0.1);
        const comboName = `Combo: ${comboItems.map(i => i.name).join(' + ')}`;
        cart.push({
            id: Date.now(),
            name: comboName,
            nameMr: 'कॉम्बो',
            price: total - discount,
            img: comboItems[0].img,
            qty: 1,
            spice: '',
            note: 'Combo Discount Applied',
            cartId: 'combo-' + Date.now(),
            veg: comboItems.every(i => i.veg)
        });
        comboSelection = [];
        updateCartBar();
        closeModal('comboModal');
        alert('Combo Added to Cart!');
    }

    function openRating(id) {
        const item = menuItems.find(i => i.id === id);
        currentRatingItem = id;
        document.getElementById('ratingItemName').textContent = item.name;
        setRating(0);
        openModal('ratingModal');
    }

    function setRating(val) {
        currentRating = val;
        document.querySelectorAll('.star').forEach((s, i) => {
            s.classList.toggle('active', i < val);
        });
    }

    function submitRating() {
        if(currentRating === 0) {
            alert('Please select rating');
            return;
        }
        const item = menuItems.find(i => i.id === currentRatingItem);
        const oldTotal = item.rating * item.ratingCount;
        item.ratingCount++;
        item.rating = ((oldTotal + currentRating) / item.ratingCount).toFixed(1);
        localStorage.setItem('menuItems', JSON.stringify(menuItems));
        closeModal('ratingModal');
        renderProducts();
        alert('Thank you for rating!');
    }

    function toggleLang() {
        currentLang = currentLang === 'en'? 'mr' : 'en';
        document.querySelector('.lang-toggle').textContent = currentLang === 'en'? 'मराठी' : 'English';
        renderCategories();
        renderProducts();
        if(document.getElementById('cartModal').classList.contains('show')) renderCart();
    }

    function toggleTheme() {
        isDarkMode =!isDarkMode;
        document.body.classList.toggle('light',!isDarkMode);
        document.querySelector('.theme-toggle').textContent = isDarkMode? '🌙' : '☀️';
    }

    function openChat() {
        const msg = `Hi! I have a query about Pratibha's Kitchen.`;
        window.open(`https://wa.me/${YOUR_WHATSAPP}?text=${encodeURIComponent(msg)}`, '_blank');
    }

    function openAdmin() {
        openModal('adminModal');
    }

    function adminLogin() {
        const pass = document.getElementById('adminPass').value;
        if(pass === ADMIN_PASS) {
            document.getElementById('adminLogin').style.display = 'none';
            document.getElementById('adminPanel').style.display = 'block';
            renderAdminPanel();
        } else {
            alert('Wrong Password!');
        }
    }

    function adminLogout() {
        document.getElementById('adminLogin').style.display = 'block';
        document.getElementById('adminPanel').style.display = 'none';
        document.getElementById('adminPass').value = '';
    }

    function renderAdminPanel() {
        const totalOrders = orders.length;
        const totalRevenue = orders.reduce((sum, o) => sum + o.total, 0);
        const avgOrder = totalOrders > 0? Math.round(totalRevenue / totalOrders) : 0;

        document.getElementById('analytics').innerHTML = `
            <div style="display:grid;grid-template-columns:1fr 1fr 1fr;gap:10px;margin-bottom:15px;">
                <div style="background:var(--bg);padding:15px;border-radius:10px;text-align:center;">
                    <div style="font-size:24px;font-weight:800;color:#00FF88">${totalOrders}</div>
                    <div style="font-size:12px;color:var(--text2)">Total Orders</div>
                </div>
                <div style="background:var(--bg);padding:15px;border-radius:10px;text-align:center;">
                    <div style="font-size:24px;font-weight:800;color:#00FF88">Rs ${totalRevenue}</div>
                    <div style="font-size:12px;color:var(--text2)">Revenue</div>
                </div>
                <div style="background:var(--bg);padding:15px;border-radius:10px;text-align:center;">
                    <div style="font-size:24px;font-weight:800;color:#00FF88">Rs ${avgOrder}</div>
                    <div style="font-size:12px;color:var(--text2)">Avg Order</div>
                </div>
            </div>
        `;

        const last7Days = {};
        for(let i = 6; i >= 0; i--) {
            const d = new Date();
            d.setDate(d.getDate() - i);
            const key = d.toLocaleDateString('en-IN', {day: '2-digit', month: 'short'});
            last7Days[key] = 0;
        }
        orders.forEach(o => {
            const date = new Date(o.date).toLocaleDateString('en-IN', {day: '2-digit', month: 'short'});
            if(last7Days.hasOwnProperty(date)) last7Days[date] += o.total;
        });
        const maxVal = Math.max(...Object.values(last7Days), 1);
        document.getElementById('chart').innerHTML = Object.entries(last7Days).map(([day, val]) => `
            <div class="bar" style="height:${(val/maxVal)*100}%">
                <div class="bar-label">${day}</div>
            </div>
        `).join('');

        document.getElementById('adminOrders').innerHTML = orders.slice().reverse().map(o => `
            <div style="background:var(--bg);padding:10px;border-radius:8px;margin-bottom:8px;">
                <div style="display:flex;justify-content:space-between;margin-bottom:5px;">
                    <b>${o.id}</b>
                    <span class="status-badge status-${o.status}">${o.status}</span>
                </div>
                <div style="font-size:11px">${o.name} - Rs ${o.total}</div>
                <div style="font-size:10px;color:var(--text2)">${o.date}</div>
                <select onchange="updateOrderStatus('${o.id}', this.value)" style="margin-top:5px;width:100%;padding:5px;border-radius:5px;background:var(--card);color:var(--text);border:1px solid #475569;">
                    <option value="Placed" ${o.status==='Placed'?'selected':''}>Placed</option>
                    <option value="Preparing" ${o.status==='Preparing'?'selected':''}>Preparing</option>
                    <option value="Out for Delivery" ${o.status==='Out for Delivery'?'selected':''}>Out for Delivery</option>
                    <option value="Delivered" ${o.status==='Delivered'?'selected':''}>Delivered</option>
                </select>
            </div>
        `).join('') || '<p style="text-align:center;color:var(--text2)">No orders yet</p>';
    }

    function updateOrderStatus(orderId, status) {
        const order = orders.find(o => o.id === orderId);
        order.status = status;
        localStorage.setItem('orders', JSON.stringify(orders));
        renderAdminPanel();
    }

    function saveItem() {
        const id = document.getElementById('editId').value;
        const name = document.getElementById('editName').value;
        const nameMr = document.getElementById('editNameMr').value;
        const price = parseInt(document.getElementById('editPrice').value);
        const img = document.getElementById('editImg').value;
        const cat = document.getElementById('editCat').value;
        const veg = document.getElementById('editVeg').value === 'true';
        const best = document.getElementById('editBest').checked;

        if(!name ||!nameMr ||!price ||!img) {
            alert('Please fill all fields');
            return;
        }

        if(id) {
            const item = menuItems.find(i => i.id === parseInt(id));
            if(item) {
                item.name = name;
                item.nameMr = nameMr;
                item.price = price;
                item.img = img;
                item.cat = cat;
                item.veg = veg;
                item.bestseller = best;
            }
        } else {
            const newId = Math.max(...menuItems.map(i => i.id)) + 1;
            menuItems.push({ id: newId, name, nameMr, price, img, cat, veg, bestseller: best, rating: 4.0, ratingCount: 0 });
        }

        localStorage.setItem('menuItems', JSON.stringify(menuItems));
        renderProducts();
        alert('Item Saved!');

        document.getElementById('editId').value = '';
        document.getElementById('editName').value = '';
        document.getElementById('editNameMr').value = '';
        document.getElementById('editPrice').value = '';
        document.getElementById('editImg').value = '';
        document.getElementById('editBest').checked = false;
    }

    init();
</script>
</body>
</html>
