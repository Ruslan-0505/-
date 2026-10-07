<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Исламская рассрочка - Калькулятор</title>
    <meta name="description" content="Калькулятор исламской рассрочки (мурабаха) без процентов">
    <meta property="og:title" content="Калькулятор исламской рассрочки">
    <meta property="og:description" content="Быстро рассчитайте платежи по системе мурабаха">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        .container {
            background: white;
            border-radius: 25px;
            box-shadow: 0 25px 70px rgba(0,0,0,0.35);
            max-width: 650px;
            width: 100%;
            padding: 45px;
        }

        .header {
            text-align: center;
            margin-bottom: 35px;
        }

        .logo {
            font-size: 40px;
            margin-bottom: 15px;
        }

        .header h1 {
            color: #667eea;
            font-size: 32px;
            margin-bottom: 10px;
            font-weight: 700;
        }

        .header p {
            color: #888;
            font-size: 15px;
            line-height: 1.6;
        }

        .form-group {
            margin-bottom: 28px;
        }

        label {
            display: block;
            color: #333;
            font-weight: 600;
            margin-bottom: 10px;
            font-size: 15px;
            letter-spacing: 0.3px;
        }

        .info-text {
            font-size: 12px;
            color: #aaa;
            margin-top: 5px;
            font-weight: 400;
        }

        input, select {
            width: 100%;
            padding: 14px 16px;
            border: 2px solid #e8e8e8;
            border-radius: 10px;
            font-size: 15px;
            transition: all 0.3s;
            font-family: inherit;
        }

        input:focus, select:focus {
            outline: none;
            border-color: #667eea;
            background: #f8f9ff;
            box-shadow: 0 0 0 4px rgba(102, 126, 234, 0.1);
        }

        .input-wrapper {
            position: relative;
            display: flex;
        }

        .input-wrapper input {
            padding-right: 50px;
        }

        .currency-badge {
            position: absolute;
            right: 15px;
            top: 50%;
            transform: translateY(-50%);
            color: #667eea;
            font-weight: 600;
            pointer-events: none;
        }

        .two-col {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 15px;
        }

        @media (max-width: 600px) {
            .two-col {
                grid-template-columns: 1fr;
            }
        }

        button {
            width: 100%;
            padding: 16px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 16px;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.3s;
            margin-top: 10px;
            letter-spacing: 0.5px;
        }

        button:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 40px rgba(102, 126, 234, 0.4);
        }

        button:active {
            transform: translateY(-1px);
        }

        .results {
            display: none;
            margin-top: 40px;
            padding-top: 40px;
            border-top: 3px solid #f0f0f0;
        }

        .results.show {
            display: block;
            animation: slideIn 0.4s ease-out;
        }

        @keyframes slideIn {
            from {
                opacity: 0;
                transform: translateY(20px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .result-grid {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 18px;
            margin-bottom: 25px;
        }

        @media (max-width: 600px) {
            .result-grid {
                grid-template-columns: 1fr;
            }
        }

        .result-card {
            background: linear-gradient(135deg, #f8fafb 0%, #f0f3f7 100%);
            padding: 25px;
            border-radius: 15px;
            border-left: 5px solid #667eea;
            transition: transform 0.3s;
        }

        .result-card:hover {
            transform: translateY(-5px);
        }

        .result-card.highlight {
            border-left-color: #764ba2;
        }

        .result-label {
            color: #999;
            font-size: 12px;
            text-transform: uppercase;
            letter-spacing: 1px;
            margin-bottom: 8px;
            font-weight: 600;
        }

        .result-value {
            color: #667eea;
            font-size: 28px;
            font-weight: 700;
            line-height: 1.2;
            word-break: break-word;
        }

        .result-card.highlight .result-value {
            color: #764ba2;
        }

        .tabs {
            display: flex;
            gap: 10px;
            margin-bottom: 25px;
            border-bottom: 2px solid #f0f0f0;
        }

        .tab-btn {
            flex: 1;
            padding: 14px 0;
            border: none;
            background: none;
            color: #999;
            border-bottom: 3px solid transparent;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s;
            border-radius: 0;
        }

        .tab-btn.active {
            color: #667eea;
            border-bottom-color: #667eea;
        }

        .tab-content {
            display: none;
        }

        .tab-content.active {
            display: block;
            animation: fadeIn 0.3s ease-out;
        }

        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }

        .table-container {
            overflow-x: auto;
            margin-top: 15px;
            border-radius: 10px;
            border: 1px solid #e8e8e8;
        }

        table {
            width: 100%;
            font-size: 13px;
            border-collapse: collapse;
        }

        th {
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            padding: 15px;
            text-align: left;
            font-weight: 600;
            font-size: 12px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }

        td {
            padding: 12px 15px;
            border-bottom: 1px solid #f0f0f0;
            font-size: 14px;
        }

        tr:nth-child(even) {
            background: #fafafa;
        }

        tr:hover {
            background: #f5f5f5;
        }

        .highlight-box {
            background: linear-gradient(135deg, #fff9e6 0%, #fffbf0 100%);
            padding: 18px;
            border-radius: 10px;
            border-left: 4px solid #ffc107;
            color: #704f1a;
            font-size: 13px;
            margin-top: 20px;
            line-height: 1.7;
            font-weight: 500;
        }

        .islamic-note {
            background: linear-gradient(135deg, #e3f2fd 0%, #f3e5f5 100%);
            border-left: 4px solid #7c3aed;
            padding: 18px;
            border-radius: 10px;
            color: #4338ca;
            font-size: 13px;
            margin-top: 20px;
            line-height: 1.7;
            font-weight: 500;
        }

        .share-section {
            margin-top: 25px;
            padding-top: 25px;
            border-top: 2px solid #f0f0f0;
        }

        .share-buttons {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            justify-content: center;
        }

        .share-btn {
            padding: 10px 16px;
            border-radius: 8px;
            border: 2px solid #e8e8e8;
            background: white;
            color: #667eea;
            font-weight: 600;
            cursor: pointer;
            font-size: 13px;
            transition: all 0.3s;
        }

        .share-btn:hover {
            border-color: #667eea;
            background: #f8f9ff;
        }

        .footer {
            text-align: center;
            margin-top: 30px;
            padding-top: 25px;
            border-top: 2px solid #f0f0f0;
            color: #999;
            font-size: 12px;
        }

        .currency-select {
            width: 100%;
            padding: 12px 10px;
            border: 2px solid #e8e8e8;
            border-radius: 8px;
            margin-bottom: 20px;
            cursor: pointer;
        }

        @media (max-width: 600px) {
            .container {
                padding: 25px;
            }

            .header h1 {
                font-size: 24px;
            }

            .result-value {
                font-size: 22px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <div class="logo">💳</div>
            <h1>Исламская рассрочка</h1>
            <p>Калькулятор мурабахи — справедливая рассрочка без процентов</p>
        </div>

        <div style="text-align: center; margin-bottom: 20px;">
            <select class="currency-select" id="currencySelect" onchange="changeCurrency()">
                <option value="₸">Казахстан (₸)</option>
                <option value="₽">Россия (₽)</option>
                <option value="₼">Азербайджан (₼)</option>
                <option value="сом">Кыргызстан (сом)</option>
                <option value="$">Доллар США ($)</option>
                <option value="€">Евро (€)</option>
            </select>
        </div>

        <form id="calculatorForm">
            <div class="form-group">
                <label>💰 Стоимость товара / услуги</label>
                <div class="input-wrapper">
                    <input type="number" id="productCost" placeholder="100000" min="0" step="0.01" required>
                    <span class="currency-badge" id="currency1">₸</span>
                </div>
            </div>

            <div class="two-col">
                <div class="form-group">
                    <label>📈 Маржа банка (%)</label>
                    <div class="input-wrapper">
                        <input type="number" id="markup" placeholder="10" min="0" max="100" step="0.01" value="10" required>
                        <span class="currency-badge">%</span>
                    </div>
                    <div class="info-text">Обычно 8-15%</div>
                </div>

                <div class="form-group">
                    <label>⏱️ Количество месяцев</label>
                    <select id="months" required>
                        <option value="">Выберите срок</option>
                        <option value="3">3 месяца</option>
                        <option value="6">6 месяцев</option>
                        <option value="12">12 месяцев</option>
                        <option value="18">18 месяцев</option>
                        <option value="24">24 месяца</option>
                        <option value="36">36 месяцев</option>
                        <option value="48">48 месяцев</option>
                        <option value="60">60 месяцев</option>
                    </select>
                </div>
            </div>

            <div class="form-group">
                <label>🛡️ Страховка (опционально, %)</label>
                <div class="input-wrapper">
                    <input type="number" id="insurance" placeholder="0" min="0" step="0.01" value="0">
                    <span class="currency-badge">%</span>
                </div>
                <div class="info-text">Страховка жизни, имущества</div>
            </div>

            <button type="submit">Рассчитать платежи</button>
        </form>

        <div class="results" id="results">
            <div class="tabs">
                <button type="button" class="tab-btn active" onclick="switchTab(event, 'summary')">Итоговая смета</button>
                <button type="button" class="tab-btn" onclick="switchTab(event, 'schedule')">График платежей</button>
            </div>

            <div id="summary" class="tab-content active">
                <div class="result-grid">
                    <div class="result-card">
                        <div class="result-label">Стоимость товара</div>
                        <div class="result-value" id="displayCost">0</div>
                    </div>

                    <div class="result-card highlight">
                        <div class="result-label">Маржа + Страховка</div>
                        <div class="result-value" id="displayMarkup">0</div>
                    </div>
                </div>

                <div class="result-grid">
                    <div class="result-card" style="grid-column: 1 / -1; border-left-color: #10b981;">
                        <div class="result-label">✅ Итоговая сумма к оплате</div>
                        <div class="result-value" style="color: #10b981; font-size: 35px;" id="displayTotal">0</div>
                    </div>
                </div>

                <div class="result-grid">
                    <div class="result-card highlight">
                        <div class="result-label">📅 Ежемесячный платёж</div>
                        <div class="result-value" id="displayMonthly">0</div>
                    </div>

                    <div class="result-card">
                        <div class="result-label">Сроки</div>
                        <div class="result-value" style="color: #667eea; font-size: 22px;" id="displayMonths">0</div>
                    </div>
                </div>

                <div class="highlight-box">
                    <strong>ℹ️ Как это работает:</strong> Банк сообщает стоимость товара, добавляет фиксированную прибыль (маржу), и вы платите равными частями каждый месяц. Без "скрытых" процентов.
                </div>

                <div class="islamic-note">
                    <strong>📖 Исламская основа:</strong> Мурабаха — справедливая система, соответствующая Шариату. Обе стороны знают о расходах и прибыли заранее. Нет обмана и неявных платежей (рибы).
                </div>

                <div class="share-section">
                    <div style="text-align: center; margin-bottom: 12px; color: #999; font-size: 12px; font-weight: 600;">Поделиться результатом:</div>
                    <div class="share-buttons">
                        <button class="share-btn" onclick="shareWhatsApp()">WhatsApp</button>
                        <button class="share-btn" onclick="shareTelegram()">Telegram</button>
                        <button class="share-btn" onclick="copyLink()">Скопировать</button>
                    </div>
                </div>
            </div>

            <div id="schedule" class="tab-content">
                <div class="table-container">
                    <table>
                        <thead>
                            <tr>
                                <th>Месяц</th>
                                <th>Платёж</th>
                                <th>Остаток</th>
                            </tr>
                        </thead>
                        <tbody id="scheduleTable">
                        </tbody>
                    </table>
                </div>
            </div>
        </div>

        <div class="footer">
            <p>💚 Калькулятор исламской рассрочки | Основан на принципах Шариата</p>
            <p style="margin-top: 8px;">Информационный инструмент. Точные условия уточняйте в организации.</p>
        </div>
    </div>

    <script>
        let currentCurrency = '₸';

        function formatCurrency(value, currency = currentCurrency) {
            const formatted = new Intl.NumberFormat('ru-RU', {
                minimumFractionDigits: 2,
                maximumFractionDigits: 2
            }).format(value);
            return formatted + ' ' + currency;
        }

        function changeCurrency() {
            currentCurrency = document.getElementById('currencySelect').value;
            document.querySelectorAll('.currency-badge').forEach(el => {
                el.textContent = currentCurrency;
            });
            
            if (document.getElementById('results').classList.contains('show')) {
                document.getElementById('calculatorForm').dispatchEvent(new Event('submit'));
            }
        }

        function switchTab(e, tabName) {
            e.preventDefault();
            
            document.querySelectorAll('.tab-content').forEach(tab => {
                tab.classList.remove('active');
            });
            document.querySelectorAll('.tab-btn').forEach(btn => {
                btn.classList.remove('active');
            });

            document.getElementById(tabName).classList.add('active');
            e.target.classList.add('active');
        }

        document.getElementById('calculatorForm').addEventListener('submit', function(e) {
            e.preventDefault();

            const productCost = parseFloat(document.getElementById('productCost').value);
            const markup = parseFloat(document.getElementById('markup').value);
            const months = parseInt(document.getElementById('months').value);
            const insurance = parseFloat(document.getElementById('insurance').value) || 0;

            if (!productCost || !months) {
                alert('Заполните все обязательные поля');
                return;
            }

            const markupAmount = productCost * (markup / 100);
            const insuranceAmount = (productCost + markupAmount) * (insurance / 100);
            const totalAmount = productCost + markupAmount + insuranceAmount;
            const monthlyPayment = totalAmount / months;

            document.getElementById('displayCost').textContent = formatCurrency(productCost);
            document.getElementById('displayMarkup').textContent = formatCurrency(markupAmount + insuranceAmount);
            document.getElementById('displayTotal').textContent = formatCurrency(totalAmount);
            document.getElementById('displayMonthly').textContent = formatCurrency(monthlyPayment);
            document.getElementById('displayMonths').textContent = months + ' месяцев';

            let scheduleHTML = '';
            let balance = totalAmount;

            for (let i = 1; i <= months; i++) {
                balance -= monthlyPayment;
                const balanceDisplay = balance < 0.01 ? 0 : balance;

                scheduleHTML += `
                    <tr>
                        <td><strong>${i}</strong></td>
                        <td>${formatCurrency(monthlyPayment)}</td>
                        <td>${formatCurrency(balanceDisplay)}</td>
                    </tr>
                `;
            }

            document.getElementById('scheduleTable').innerHTML = scheduleHTML;

            document.getElementById('results').classList.add('show');
            setTimeout(() => {
                document.getElementById('results').scrollIntoView({ behavior: 'smooth' });
            }, 100);
        });

        function shareWhatsApp() {
            const text = `Проверь калькулятор исламской рассрочки без процентов: ${window.location.href}`;
            window.open(`https://wa.me/?text=${encodeURIComponent(text)}`, '_blank');
        }

        function shareTelegram() {
            const text = `Калькулятор исламской рассрочки без процентов`;
            window.open(`https://t.me/share/url?url=${encodeURIComponent(window.location.href)}&text=${encodeURIComponent(text)}`, '_blank');
        }

        function copyLink() {
            navigator.clipboard.writeText(window.location.href).then(() => {
                alert('✅ Ссылка скопирована!');
            }).catch(() => {
                alert('⚠️ Не удалось скопировать ссылку');
            });
        }
    </script>
</body>
</html>