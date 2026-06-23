<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>🐱 Prof Eddie's Redox Lab 🐟</title>
    <style>
        :root {
            --orange-theme: #ffb07c;
            --mint-theme: #e3faf2;
            --cat-orange: #f6ad55;
            --cat-white: #edf2f7;
            --fish-blue: #3182ce;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background-color: #fffaf0;
            color: #2d3748;
            margin: 0;
            padding: 20px;
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .container {
            max-width: 900px;
            width: 100%;
            background: #ffffff;
            padding: 25px;
            border-radius: 20px;
            box-shadow: 0 8px 24px rgba(229, 124, 35, 0.15);
            border: 4px solid var(--orange-theme);
        }

        .header-ui {
            display: flex;
            justify-content: space-between;
            align-items: center;
            background: var(--mint-theme);
            padding: 15px 25px;
            border-radius: 15px;
            margin-bottom: 20px;
            border: 2px dashed #b2f5ea;
        }

        .currency-box {
            font-size: 1.3em;
            font-weight: bold;
            color: var(--fish-blue);
        }

        /* Setup Screen Panels */
        .panel {
            display: none;
        }
        .panel.active {
            display: block;
        }

        .menu-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
            margin: 15px 0;
        }

        .card-btn {
            background: #fff;
            border: 3px solid #e2e8f0;
            border-radius: 12px;
            padding: 20px;
            cursor: pointer;
            text-align: center;
            transition: all 0.2s;
            font-size: 1.1em;
            font-weight: bold;
        }

        .card-btn:hover, .card-btn.selected {
            border-color: var(--cat-orange);
            background: #fffaf0;
            transform: translateY(-2px);
        }

        /* Characters Section */
        .cat-dialogue-box {
            display: flex;
            align-items: center;
            gap: 15px;
            margin-bottom: 20px;
            background: #f7fafc;
            padding: 15px;
            border-radius: 12px;
            border-left: 6px solid var(--cat-orange);
        }

        .cat-avatar-container {
            min-width: 70px;
            max-width: 70px;
            height: 70px;
            border-radius: 50%;
            overflow: hidden;
            background: #e2e8f0;
            display: flex;
            align-items: center;
            justify-content: center;
            border: 2px solid #cbd5e0;
        }

        .cat-avatar-img {
            width: 100%;
            height: 100%;
            object-fit: cover;
        }

        .cat-name {
            font-weight: bold;
            font-size: 0.9em;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 4px;
        }

        .eddie { color: #dd6b20; }
        .xiaobai { color: #4a5568; }

        /* Game UI */
        .equation-box {
            font-size: 1.4em;
            font-family: 'Courier New', Courier, monospace;
            text-align: center;
            margin: 20px 0;
            padding: 20px;
            background: #fcf8f2;
            border-radius: 12px;
            border: 2px solid #fbd38d;
        }

        .equation-box input {
            width: 50px;
            padding: 6px;
            font-size: 0.9em;
            text-align: center;
            border: 2px solid #cbd5e0;
            border-radius: 6px;
            font-weight: bold;
        }

        .bet-box {
            background: #edf2f7;
            padding: 15px;
            border-radius: 10px;
            text-align: center;
            margin-bottom: 20px;
        }

        button.action-btn {
            width: 100%;
            padding: 15px;
            background: var(--cat-orange);
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 1.2em;
            font-weight: bold;
            cursor: pointer;
            box-shadow: 0 4px 0 #c05621;
        }

        button.action-btn:active {
            transform: translateY(4px);
            box-shadow: none;
        }

        /* Shop Styles */
        .shop-tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 15px;
        }
        .tab-btn {
            flex: 1;
            padding: 10px;
            background: #e2e8f0;
            border: none;
            cursor: pointer;
            font-weight: bold;
            border-radius: 5px;
        }
        .tab-btn.active {
            background: var(--cat-orange);
            color: white;
        }
        .shop-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(130px, 1fr));
            gap: 12px;
            max-height: 300px;
            overflow-y: auto;
        }
        .shop-item {
            border: 2px solid #e2e8f0;
            border-radius: 8px;
            padding: 10px;
            text-align: center;
            background: #fff;
        }

        /* Sanctuary Room view */
        .sanctuary-preview {
            background: #feebc8;
            border: 3px solid #fbd38d;
            border-radius: 12px;
            min-height: 150px;
            padding: 15px;
            margin-top: 20px;
        }
        .item-tag {
            display: inline-block;
            background: #fff;
            padding: 4px 8px;
            margin: 4px;
            border-radius: 20px;
            font-size: 0.85em;
            border: 1px solid #cbd5e0;
        }
        sub, sup { font-size: 0.6em; }

        /* --- ANIMATED GACHA MODAL --- */
        .modal-overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0, 0, 0, 0.6);
            backdrop-filter: blur(4px);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }
        .modal-card {
            background: #fff;
            border: 4px solid var(--orange-theme);
            border-radius: 24px;
            padding: 30px;
            max-width: 400px;
            width: 85%;
            text-align: center;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
            transform: scale(0.7);
            opacity: 0;
            transition: all 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
        }
        .modal-overlay.active {
            display: flex;
        }
        .modal-overlay.active .modal-card {
            transform: scale(1);
            opacity: 1;
        }
        .gacha-box-animation {
            font-size: 4em;
            margin: 15px 0;
            animation: bounce 0.6s infinite alternate;
        }
        @keyframes bounce {
            from { transform: translateY(0); }
            to { transform: translateY(-10px); }
        }
        .modal-close-btn {
            margin-top: 20px;
            padding: 10px 25px;
            background: #4cbd93;
            color: white;
            border: none;
            border-radius: 20px;
            font-weight: bold;
            cursor: pointer;
            box-shadow: 0 4px 0 #276749;
        }
        .modal-close-btn:active {
            transform: translateY(2px);
            box-shadow: none;
        }
    </style>
</head>
<body>

<div class="container">
    <div class="header-ui">
        <h2>🔬 Redox Neko Lab 🐾</h2>
        <div class="currency-box">🐟 <span id="fish-count">15</span> Lil' Fishes</div>
    </div>

    <div id="setup-panel" class="panel active">
        <h3>✨ Select Strategy Routine</h3>
        <div class="menu-grid">
            <div class="card-btn selected" id="mode-quick" onclick="setMode('quick')">⚡ Quick Start<br><small style="font-weight:normal;">Exactly 5 Tasks</small></div>
            <div class="card-btn" id="mode-full" onclick="setMode('full')">📚 Full Revision<br><small style="font-weight:normal;">Custom depth session</small></div>
        </div>

        <div id="full-count-select" style="display:none; text-align: center; margin: 15px 0;">
            <label for="q-count"><b>Target Question Capacity:</b></label>
            <select id="q-count" style="padding: 5px; font-size: 1em;">
                <option value="10">10 Questions</option>
                <option value="15">15 Questions</option>
                <option value="20">20 Questions</option>
                <option value="25">25 Questions</option>
            </select>
        </div>

        <h3>🧪 Core Chemistry Core Topic</h3>
        <div class="menu-grid">
            <div class="card-btn selected" id="topic-redox" onclick="setTopic('redox')">🌀 General Half-Eqns & Transfers</div>
            <div class="card-btn" id="topic-disp" onclick="setTopic('disp')">⚔️ Metal Displacements</div>
            <div class="card-btn" id="topic-acid" onclick="setTopic('acid')">🧪 Acid-Base Oxidations</div>
        </div>

        <button class="action-btn" style="margin-top:20px;" onclick="startSession()">Enter the Lab 🐾</button>
    </div>

    <div id="lab-panel" class="panel">
        <div style="display: flex; justify-content: space-between; font-weight: bold; margin-bottom: 10px;">
            <span id="session-topic-display">Topic</span>
            <span id="progress-display">Question 1/5</span>
        </div>

        <div class="cat-dialogue-box">
            <div class="cat-avatar-container">
                <img class="cat-avatar-img" src="Eddie.jpeg" alt="Prof Eddie Portrait">
            </div>
            <div>
                <div class="cat-name eddie">Prof Eddie</div>
                <div id="eddie-text">"Welcome! Let's parse electron densities. Remember, mass balance precedes balancing net systemic charge."</div>
            </div>
        </div>
        
        <div class="cat-dialogue-box" style="border-left-color: #cbd5e0;">
            <div class="cat-avatar-container">
                <img class="cat-avatar-img" src="Xiaobai.jpeg" alt="Xiaobai Portrait">
            </div>
            <div>
                <div class="cat-name xiaobai">Xiaobai</div>
                <div id="xiaobai-text">"*Heavy breathing* Me saw shiny swimming fishies if you write correct numbers in boxes... please do it quickly!!"</div>
            </div>
        </div>

        <div class="equation-box" id="equation-target">
            </div>

        <div class="bet-box">
            <label for="risk-wager"><b>Confidence Pool Wager:</b></label> <span id="wager-val" style="color:var(--fish-blue); font-weight:bold;">2</span> Fishes<br>
            <input type="range" id="risk-wager" min="1" max="10" value="2" style="width:70%; margin-top:8px;" oninput="document.getElementById('wager-val').innerText=this.value">
            <div style="font-size:0.8em; color:#718096; margin-top:4px;">Lose your wager on incorrect submission; win back matching payout on success!</div>
        </div>

        <button class="action-btn" id="submit-btn" onclick="evaluateAnswer()">Verify Balanced Coefficients</button>
        <button class="action-btn" id="next-btn" style="display:none; background:#4a5568; box-shadow:0 4px 0 #2d3748;" onclick="advanceSession()">Next Chemical Challenge</button>
    </div>

    <div id="hub-panel" class="panel">
        <h3 style="text-align: center;">🏁 System Operations Complete!</h3>
        <p id="results-summary" style="text-align:center; font-weight:bold;"></p>
        
        <hr style="border:1px dashed #cbd5e0; margin:25px 0;">
        <h3>🏡 The Cat Tree Sanctuary</h3>
        
        <div class="shop-tabs">
            <button class="tab-btn active" onclick="switchTab('box')">🎁 Blind Boxes</button>
            <button class="tab-btn" onclick="switchTab('furn')">🛋️ Decor & Space</button>
        </div>

        <div id="shop-container" class="shop-grid">
            </div>

        <div class="sanctuary-preview">
            <strong>🏯 Current Territory Portfolio:</strong> <span id="room-expansion-tier">Cozy Cardboard Base</span>
            <div id="inventory-display" style="margin-top:10px;">
                </div>
        </div>

        <button class="action-btn" style="margin-top:20px; background:#4cbd93; box-shadow:0 4px 0 #276749;" onclick="returnToMenu()">Configure New Session</button>
    </div>
</div>

<div id="gacha-modal" class="modal-overlay">
    <div class="modal-card">
        <h2 id="modal-title">🎁 Unboxing...</h2>
        <div id="modal-icon" class="gacha-box-animation">🎁</div>
        <p id="modal-message" style="font-size: 1.1em; font-weight: bold; color: #2d3748; margin: 15px 0;"></p>
        <button class="modal-close-btn" onclick="closeModal()">Sweet! 🎉</button>
    </div>
</div>

<script>
    // System Repositories 
    const DB = {
        redox: [
            { eq: [["Fe2",1],"Fe<sup>2+</sup> &rarr; ",["Fe3",1],"Fe<sup>3+</sup> + ",["e",1],"e<sup>-</sup>"], ans:{Fe2:1,Fe3:1,e:1}, hint:"This oxidation half-reaction balances mass perfectly at 1:1. Check net charge to find the electron count." },
            { eq: [["Cl2",1],"Cl<sub>2</sub> + ",["e",2],"e<sup>-</sup> &rarr; ",["Cl",2],"Cl<sup>-</sup>"], ans:{Cl2:1,e:2,Cl:2}, hint:"Chlorine exists as a diatomic molecule. Balance the chlorine atoms first, then find the charges." },
            { eq: [["MnO4",1],"MnO<sub>4</sub><sup>-</sup> + ",["H",8],"H<sup>+</sup> + ",["e",5],"e<sup>-</sup> &rarr; ",["Mn",1],"Mn<sup>2+</sup> + ",["H2O",4],"H<sub>2</sub>O"], ans:{MnO4:1,H:8,e:5,Mn:1,H2O:4}, hint:"Reduction of permanganate in acid. Make sure your H+ balances the oxygen into water before matching the +2 net charge on both sides." }
        ],
        disp: [
            { eq: [["Zn",1],"Zn + ",["Cu",1],"Cu<sup>2+</sup> &rarr; ",["Zn2",1],"Zn<sup>2+</sup> + ",["CuS",1],"Cu"], ans:{Zn:1,Cu:1,Zn2:1,CuS:1}, hint:"Simple metal displacement. The 2-electron transfer from Zinc to Copper matches natively here." },
            { eq: [["Al",2],"Al + ",["Sn",3],"Sn<sup>2+</sup> &rarr; ",["Al3",2],"Al<sup>3+</sup> + ",["SnS",3],"Sn"], ans:{Al:2,Sn:3,Al3:2,SnS:3}, hint:"Aluminum yields 3 electrons while Tin accepts 2. Find the lowest common denominator (6) to coordinate cross-coefficients." }
        ],
        acid: [
            { eq: [["Mg",1],"Mg + ",["H",2],"H<sup>+</sup> &rarr; ",["Mg2",1],"Mg<sup>2+</sup> + ",["H2",1],"H<sub>2</sub>"], ans:{Mg:1,H:2,Mg2:1,H2:1}, hint:"Acid oxidation of active metal. Track your hydrogen atom count to secure the charge balance." }
        ]
    };

    const SHOP = {
        box: [
            { name: "Common Crate", cost: 5, icon: "📦", roll: () => rollCat(['Standard Tabby (Calm)', 'Black Tuxedo Cat (Sassy)'], ['Rare Ginger Mainecoon (Clumsy)']) },
            { name: "Mega Box", cost: 12, icon: "💎", roll: () => rollCat(['Rare Ginger Mainecoon (Clumsy)', 'Persian Cloud (Lazy)'], ['🌟 Ultra-Rare Male Calico (Hyperactive)', '🌟 Mystic Sphinx (Philosopher)']) }
        ],
        furn: [
            { name: "Scratching Post", cost: 4, icon: "🪵" },
            { name: "Velvet Cushion", cost: 8, icon: "👑" },
            { name: "Expand Sanctuary Room", cost: 20, icon: "🏡", expand: true }
        ]
    };

    // State Variables
    let economy = { fish: 15, inventory: ["Starter Bowl"], spaceTier: 1 };
    let session = { mode: 'quick', topic: 'redox', currentQuestions: [], activeIdx: 0, count: 5 };

    // Custom Modal Display Control
    function showModal(title, icon, message) {
        document.getElementById('modal-title').innerText = title;
        document.getElementById('modal-icon').innerText = icon;
        document.getElementById('modal-message').innerText = message;
        document.getElementById('gacha-modal').classList.add('active');
    }

    function closeModal() {
        document.getElementById('gacha-modal').classList.remove('active');
    }

    function setMode(m) {
        session.mode = m;
        document.getElementById('mode-quick').classList.remove('selected');
        document.getElementById('mode-full').classList.remove('selected');
        document.getElementById('mode-'+m).classList.add('selected');
        document.getElementById('full-count-select').style.display = (m === 'full') ? 'block' : 'none';
    }

    function setTopic(t) {
        session.topic = t;
        ['redox','disp','acid'].forEach(x => document.getElementById('topic-'+x).classList.remove('selected'));
        document.getElementById('topic-'+t).classList.add('selected');
    }

    function startSession() {
        let pool = DB[session.topic];
        session.count = (session.mode === 'quick') ? 5 : parseInt(document.getElementById('q-count').value);
        
        session.currentQuestions = [];
        for(let i=0; i<session.count; i++) {
            session.currentQuestions.push(pool[i % pool.length]);
        }
        
        session.activeIdx = 0;
        document.getElementById('setup-panel').classList.remove('active');
        document.getElementById('lab-panel').classList.add('active');
        renderQuestion();
    }

    function renderQuestion() {
        const q = session.currentQuestions[session.activeIdx];
        document.getElementById('session-topic-display').innerText = "Topic Cluster: " + session.topic.toUpperCase();
        document.getElementById('progress-display').innerText = `Task ${session.activeIdx + 1} of ${session.count}`;
        
        const container = document.getElementById('equation-target');
        container.innerHTML = '';
        
        q.eq.forEach(item => {
            if(Array.isArray(item)) {
                let input = document.createElement('input');
                input.id = "chem-" + item[0];
                input.placeholder = "?";
                container.appendChild(input);
            } else {
                let span = document.createElement('span');
                span.innerHTML = item;
                container.appendChild(span);
            }
        });

        document.getElementById('eddie-text').innerText = '"Analyze carefully. Check the electron flow and balance the coefficients."';
        document.getElementById('xiaobai-text').innerText = '"Please get it right... My belly is rumbling for those yummy fishies!"';
        document.getElementById('submit-btn').style.display = "block";
        document.getElementById('next-btn').style.display = "none";
        document.getElementById('risk-wager').disabled = false;
    }

    function evaluateAnswer() {
        const q = session.currentQuestions[session.activeIdx];
        const wager = parseInt(document.getElementById('risk-wager').value);
        let userPasses = true;

        Object.keys(q.ans).forEach(key => {
            let inputField = document.getElementById("chem-" + key);
            if(inputField) {
                let parsed = parseInt(inputField.value.trim());
                if(parsed !== q.ans[key]) userPasses = false;
            }
        });

        if(userPasses) {
            economy.fish += wager;
            document.getElementById('eddie-text').innerText = '"Magnificent! Perfect atomic and charge parity achieved."';
            document.getElementById('xiaobai-text').innerText = `*Purrs loudly* Yay! You won ${wager} fishes! Crunch crunch... do it again!`;
        } else {
            economy.fish = Math.max(0, economy.fish - wager);
            document.getElementById('eddie-text').innerText = `"Incorrect combination detected. Clue: ${q.hint}"`;
            document.getElementById('xiaobai-text').innerText = `*Cries* Oh no! We lost ${wager} fishies! Xiaobai is starving... please look at the clue!`;
        }

        updateUI();
        document.getElementById('submit-btn').style.display = "none";
        document.getElementById('next-btn').style.display = "block";
        document.getElementById('risk-wager').disabled = true;
    }

    function advanceSession() {
        session.activeIdx++;
        if(session.activeIdx < session.count) {
            renderQuestion();
        } else {
            document.getElementById('lab-panel').classList.remove('active');
            document.getElementById('hub-panel').classList.add('active');
            document.getElementById('results-summary').innerText = `You completed your assignment! Current balance available for upgrades: ${economy.fish} Fishes.`;
            switchTab('box');
        }
    }

    function updateUI() {
        document.getElementById('fish-count').innerText = economy.fish;
        
        const spaceNames = ["Cozy Cardboard Base", "Sunlit Cat Studio", "Deluxe Double-Story Neko Villa", "Galactic Cosmic Cat Castle"];
        document.getElementById('room-expansion-tier').innerText = spaceNames[Math.min(economy.spaceTier - 1, 3)];

        const invContainer = document.getElementById('inventory-display');
        invContainer.innerHTML = '';
        economy.inventory.forEach(i => {
            let tag = document.createElement('span');
            tag.className = 'item-tag';
            tag.innerText = i;
            invContainer.appendChild(tag);
        });
    }

    function switchTab(type) {
        document.querySelectorAll('.tab-btn').forEach((b, idx) => {
            b.classList.toggle('active', (idx === 0 && type === 'box') || (idx === 1 && type === 'furn'));
        });

        const grid = document.getElementById('shop-container');
        grid.innerHTML = '';

        SHOP[type].forEach(item => {
            let div = document.createElement('div');
            div.className = 'shop-item';
            div.innerHTML = `<span style="font-size:2em;">${item.icon}</span><br><strong>${item.name}</strong><br><span style="color:var(--fish-blue);">🐟 ${item.cost}</span><br>`;
            
            let btn = document.createElement('button');
            btn.innerText = "Purchase";
            btn.style.marginTop = "5px";
            btn.onclick = () => buyItem(item, type);
            div.appendChild(btn);
            grid.appendChild(div);
        });
    }

    function buyItem(item, type) {
        if(economy.fish < item.cost) {
            showModal("No Fish! 😿", "❌", "Not enough fishes! Complete more redox questions first to fill your wallet.");
            return;
        }
        
        economy.fish -= item.cost;
        
        if(type === 'box') {
            let obtained = item.roll();
            economy.inventory.push(obtained);
            
            // Trigger visual animated gacha pop up
            showModal("Gacha Pop! 🎉", "🐱", `The egg cracked! You adopted:\n✨ ${obtained} ✨`);
        } else {
            if(item.expand) {
                economy.spaceTier++;
                showModal("Renovation Complete! 🔨", "🏡", "Your territory expanded! There's more space for the fluff balls now!");
            } else {
                economy.inventory.push(item.name);
                showModal("Item Unlocked! 🛋️", item.icon, `You placed the ${item.name} inside your sanctuary room.`);
            }
        }
        updateUI();
        switchTab(type);
    }

    function rollCat(commons, rares) {
        let rng = Math.random();
        if(rng > 0.25) {
            return commons[Math.floor(Math.random() * commons.length)];
        } else {
            return rares[Math.floor(Math.random() * rares.length)];
        }
    }

    function returnToMenu() {
        document.getElementById('hub-panel').classList.remove('active');
        document.getElementById('setup-panel').classList.add('active');
    }

    updateUI();
</script>

</body>
</html>
