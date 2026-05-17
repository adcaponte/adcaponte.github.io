# adcaponte.github.io
App finanças
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Finanças Pessoais</title>
    <style>
        :root {
            --bg: #0f0f1a;
            --surface: #1a1a2e;
            --surface-light: #252540;
            --primary: #00d4aa;
            --primary-dark: #00b894;
            --danger: #ff6b6b;
            --danger-dark: #ee5a5a;
            --warning: #ffd93d;
            --text: #e8e8f0;
            --text-secondary: #a0a0b8;
            --text-muted: #6c6c8a;
            --border: #2a2a45;
            --shadow: 0 8px 32px rgba(0,0,0,0.4);
            --radius: 20px;
            --radius-sm: 12px;
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            -webkit-tap-highlight-color: transparent;
        }

        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            background: var(--bg);
            color: var(--text);
            min-height: 100vh;
            overflow-x: hidden;
            display: flex;
            justify-content: center;
        }

        .app-container {
            width: 100%;
            max-width: 430px;
            min-height: 100vh;
            background: var(--bg);
            position: relative;
            overflow-x: hidden;
        }

        /* Header */
        .header {
            padding: 20px 20px 10px;
            display: flex;
            justify-content: space-between;
            align-items: center;
            position: sticky;
            top: 0;
            background: var(--bg);
            z-index: 100;
            backdrop-filter: blur(20px);
        }

        .month-nav {
            display: flex;
            align-items: center;
            gap: 12px;
        }

        .month-btn {
            width: 36px;
            height: 36px;
            border-radius: 50%;
            border: none;
            background: var(--surface);
            color: var(--text);
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.2s;
            font-size: 18px;
        }

        .month-btn:active {
            transform: scale(0.9);
            background: var(--surface-light);
        }

        .month-title {
            font-size: 18px;
            font-weight: 700;
            text-transform: capitalize;
            min-width: 140px;
            text-align: center;
        }

        .settings-btn {
            width: 36px;
            height: 36px;
            border-radius: 50%;
            border: none;
            background: var(--surface);
            color: var(--text);
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
        }

        /* Cards */
        .cards-container {
            padding: 10px 20px;
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 12px;
        }

        .card {
            background: var(--surface);
            border-radius: var(--radius-sm);
            padding: 16px;
            border: 1px solid var(--border);
            transition: transform 0.2s;
        }

        .card:active {
            transform: scale(0.98);
        }

        .card.full-width {
            grid-column: 1 / -1;
        }

        .card-label {
            font-size: 11px;
            color: var(--text-secondary);
            text-transform: uppercase;
            letter-spacing: 0.5px;
            margin-bottom: 6px;
            display: flex;
            align-items: center;
            gap: 6px;
        }

        .card-value {
            font-size: 22px;
            font-weight: 700;
            letter-spacing: -0.5px;
        }

        .card-value.positive { color: var(--primary); }
        .card-value.negative { color: var(--danger); }
        .card-value.warning { color: var(--warning); }

        .card-sub {
            font-size: 12px;
            color: var(--text-muted);
            margin-top: 4px;
        }

        /* Balance comparison */
        .comparison-bar {
            height: 8px;
            background: var(--surface-light);
            border-radius: 4px;
            margin-top: 10px;
            overflow: hidden;
            position: relative;
        }

        .comparison-fill {
            height: 100%;
            border-radius: 4px;
            transition: width 0.5s ease;
            position: relative;
        }

        .comparison-fill.expected {
            background: var(--primary);
            opacity: 0.3;
            position: absolute;
            width: 100%;
        }

        .comparison-fill.real {
            background: var(--warning);
        }

        /* Tabs */
        .tabs {
            display: flex;
            padding: 0 20px;
            margin-top: 20px;
            gap: 8px;
            overflow-x: auto;
            scrollbar-width: none;
        }

        .tabs::-webkit-scrollbar { display: none; }

        .tab {
            padding: 10px 20px;
            border-radius: 20px;
            border: none;
            background: var(--surface);
            color: var(--text-secondary);
            font-size: 14px;
            font-weight: 600;
            cursor: pointer;
            white-space: nowrap;
            transition: all 0.2s;
        }

        .tab.active {
            background: var(--primary);
            color: var(--bg);
        }

        .tab:active {
            transform: scale(0.95);
        }

        /* Content area */
        .content {
            padding: 20px;
            padding-bottom: 100px;
        }

        .section-title {
            font-size: 16px;
            font-weight: 700;
            margin-bottom: 16px;
            display: flex;
            justify-content: space-between;
            align-items: center;
        }

        .section-title button {
            background: var(--primary);
            color: var(--bg);
            border: none;
            width: 32px;
            height: 32px;
            border-radius: 50%;
            font-size: 20px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        /* Transaction list */
        .transaction-list {
            display: flex;
            flex-direction: column;
            gap: 10px;
        }

        .transaction-item {
            background: var(--surface);
            border-radius: var(--radius-sm);
            padding: 14px 16px;
            display: flex;
            align-items: center;
            gap: 14px;
            border: 1px solid var(--border);
            animation: slideIn 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        @keyframes slideIn {
            from { opacity: 0; transform: translateX(-20px); }
            to { opacity: 1; transform: translateX(0); }
        }

        .transaction-icon {
            width: 44px;
            height: 44px;
            border-radius: 12px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 20px;
            flex-shrink: 0;
        }

        .transaction-icon.income {
            background: rgba(0, 212, 170, 0.15);
        }

        .transaction-icon.expense {
            background: rgba(255, 107, 107, 0.15);
        }

        .transaction-info {
            flex: 1;
            min-width: 0;
        }

        .transaction-title {
            font-weight: 600;
            font-size: 15px;
            white-space: nowrap;
            overflow: hidden;
            text-overflow: ellipsis;
        }

        .transaction-date {
            font-size: 12px;
            color: var(--text-muted);
            margin-top: 2px;
        }

        .transaction-amount {
            font-weight: 700;
            font-size: 16px;
            flex-shrink: 0;
        }

        .transaction-amount.income { color: var(--primary); }
        .transaction-amount.expense { color: var(--danger); }

        .delete-btn {
            position: absolute;
            right: -60px;
            top: 0;
            bottom: 0;
            width: 60px;
            background: var(--danger);
            border: none;
            color: white;
            font-size: 20px;
            cursor: pointer;
            transition: right 0.2s;
            display: flex;
            align-items: center;
            justify-content: center;
        }

        .transaction-item.swiped .delete-btn {
            right: 0;
        }

        .transaction-item.swiped {
            transform: translateX(-60px);
        }

        /* Empty state */
        .empty-state {
            text-align: center;
            padding: 40px 20px;
            color: var(--text-muted);
        }

        .empty-state-icon {
            font-size: 48px;
            margin-bottom: 12px;
            opacity: 0.5;
        }

        /* Modal */
        .modal-overlay {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            bottom: 0;
            background: rgba(0,0,0,0.7);
            backdrop-filter: blur(8px);
            z-index: 1000;
            display: none;
            align-items: flex-end;
            justify-content: center;
            opacity: 0;
            transition: opacity 0.3s;
        }

        .modal-overlay.active {
            display: flex;
            opacity: 1;
        }

        .modal {
            background: var(--surface);
            width: 100%;
            max-width: 430px;
            border-radius: var(--radius) var(--radius) 0 0;
            padding: 24px 20px 32px;
            transform: translateY(100%);
            transition: transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
            max-height: 90vh;
            overflow-y: auto;
        }

        .modal-overlay.active .modal {
            transform: translateY(0);
        }

        .modal-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 24px;
        }

        .modal-title {
            font-size: 20px;
            font-weight: 700;
        }

        .modal-close {
            width: 36px;
            height: 36px;
            border-radius: 50%;
            border: none;
            background: var(--surface-light);
            color: var(--text);
            font-size: 20px;
            cursor: pointer;
        }

        /* Form */
        .form-group {
            margin-bottom: 20px;
        }

        .form-label {
            display: block;
            font-size: 13px;
            color: var(--text-secondary);
            margin-bottom: 8px;
            font-weight: 600;
        }

        .form-input, .form-select {
            width: 100%;
            padding: 14px 16px;
            border-radius: var(--radius-sm);
            border: 1px solid var(--border);
            background: var(--bg);
            color: var(--text);
            font-size: 16px;
            outline: none;
            transition: border-color 0.2s;
        }

        .form-input:focus, .form-select:focus {
            border-color: var(--primary);
        }

        .type-selector {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 10px;
            margin-bottom: 20px;
        }

        .type-option {
            padding: 14px;
            border-radius: var(--radius-sm);
            border: 2px solid var(--border);
            background: var(--bg);
            text-align: center;
            cursor: pointer;
            transition: all 0.2s;
            font-weight: 600;
        }

        .type-option.selected {
            border-color: var(--primary);
            background: rgba(0, 212, 170, 0.1);
            color: var(--primary);
        }

        .type-option.selected.expense-selected {
            border-color: var(--danger);
            background: rgba(255, 107, 107, 0.1);
            color: var(--danger);
        }

        .btn-primary {
            width: 100%;
            padding: 16px;
            border-radius: var(--radius-sm);
            border: none;
            background: var(--primary);
            color: var(--bg);
            font-size: 16px;
            font-weight: 700;
            cursor: pointer;
            transition: all 0.2s;
        }

        .btn-primary:active {
            transform: scale(0.98);
            background: var(--primary-dark);
        }

        /* Planning section */
        .planning-card {
            background: var(--surface);
            border-radius: var(--radius-sm);
            padding: 16px;
            border: 1px solid var(--border);
            margin-bottom: 12px;
        }

        .planning-header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 12px;
        }

        .planning-title {
            font-weight: 600;
            font-size: 15px;
        }

        .planning-amount {
            font-weight: 700;
            color: var(--primary);
        }

        .progress-bar {
            height: 6px;
            background: var(--surface-light);
            border-radius: 3px;
            overflow: hidden;
        }

        .progress-fill {
            height: 100%;
            background: var(--primary);
            border-radius: 3px;
            transition: width 0.5s ease;
        }

        .progress-fill.over {
            background: var(--danger);
        }

        .planning-meta {
            display: flex;
            justify-content: space-between;
            margin-top: 8px;
            font-size: 12px;
            color: var(--text-muted);
        }

        /* Real balance input */
        .real-balance-section {
            background: linear-gradient(135deg, var(--surface) 0%, var(--surface-light) 100%);
            border-radius: var(--radius-sm);
            padding: 20px;
            border: 1px solid var(--border);
            margin-bottom: 20px;
        }

        .real-balance-input {
            display: flex;
            gap: 10px;
            margin-top: 12px;
        }

        .real-balance-input input {
            flex: 1;
        }

        .real-balance-input button {
            padding: 14px 20px;
            border-radius: var(--radius-sm);
            border: none;
            background: var(--warning);
            color: var(--bg);
            font-weight: 700;
            cursor: pointer;
        }

        /* Chart */
        .chart-container {
            height: 200px;
            background: var(--surface);
            border-radius: var(--radius-sm);
            padding: 16px;
            border: 1px solid var(--border);
            margin-bottom: 20px;
            position: relative;
        }

        .chart-bars {
            display: flex;
            align-items: flex-end;
            justify-content: space-around;
            height: 140px;
            gap: 8px;
        }

        .chart-bar-wrapper {
            flex: 1;
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 6px;
        }

        .chart-bar {
            width: 100%;
            max-width: 40px;
            border-radius: 6px 6px 0 0;
            transition: height 0.5s ease;
            position: relative;
        }

        .chart-bar.income-bar {
            background: var(--primary);
        }

        .chart-bar.expense-bar {
            background: var(--danger);
        }

        .chart-label {
            font-size: 11px;
            color: var(--text-muted);
        }

        .chart-value {
            font-size: 10px;
            color: var(--text);
            font-weight: 600;
            margin-bottom: 4px;
        }

        /* Bottom nav */
        .bottom-nav {
            position: fixed;
            bottom: 0;
            left: 50%;
            transform: translateX(-50%);
            width: 100%;
            max-width: 430px;
            background: var(--surface);
            border-top: 1px solid var(--border);
            display: grid;
            grid-template-columns: 1fr 1fr 1fr 1fr;
            padding: 8px 0 24px;
            z-index: 100;
        }

        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 4px;
            padding: 8px;
            border: none;
            background: none;
            color: var(--text-muted);
            font-size: 11px;
            cursor: pointer;
            transition: color 0.2s;
        }

        .nav-item.active {
            color: var(--primary);
        }

        .nav-item svg {
            width: 24px;
            height: 24px;
        }

        /* Animations */
        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.7; }
        }

        .pulse {
            animation: pulse 2s infinite;
        }

        /* Scrollbar */
        ::-webkit-scrollbar {
            width: 4px;
        }

        ::-webkit-scrollbar-track {
            background: var(--bg);
        }

        ::-webkit-scrollbar-thumb {
            background: var(--surface-light);
            border-radius: 2px;
        }

        /* Hide sections */
        .section {
            display: none;
        }

        .section.active {
            display: block;
            animation: fadeIn 0.3s ease;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Swipe hint */
        .swipe-hint {
            text-align: center;
            font-size: 12px;
            color: var(--text-muted);
            padding: 8px;
            margin-bottom: 8px;
        }

        /* Category tags */
        .category-tags {
            display: flex;
            flex-wrap: wrap;
            gap: 8px;
            margin-top: 8px;
        }

        .category-tag {
            padding: 6px 12px;
            border-radius: 16px;
            background: var(--surface-light);
            border: 1px solid var(--border);
            font-size: 12px;
            cursor: pointer;
            transition: all 0.2s;
        }

        .category-tag.selected {
            background: var(--primary);
            color: var(--bg);
            border-color: var(--primary);
        }
    </style>
<base target="_blank">
</head>
<body>
    <div class="app-container">
        <!-- Header -->
        <div class="header">
            <div class="month-nav">
                <button class="month-btn" onclick="app.prevMonth()">&#8249;</button>
                <div class="month-title" id="monthTitle">Maio 2026</div>
                <button class="month-btn" onclick="app.nextMonth()">&#8250;</button>
            </div>
        </div>

        <!-- Cards -->
        <div class="cards-container">
            <div class="card">
                <div class="card-label">
                    <span>📥</span> Receitas
                </div>
                <div class="card-value positive" id="totalIncome">€ 0,00</div>
            </div>
            <div class="card">
                <div class="card-label">
                    <span>📤</span> Despesas
                </div>
                <div class="card-value negative" id="totalExpense">€ 0,00</div>
            </div>
            <div class="card">
                <div class="card-label">
                    <span>⚖️</span> Balanço
                </div>
                <div class="card-value" id="balance">€ 0,00</div>
                <div class="card-sub" id="balanceSub">Projetado</div>
            </div>
            <div class="card">
                <div class="card-label">
                    <span>🏦</span> Saldo Real
                </div>
                <div class="card-value warning" id="realBalance">€ 0,00</div>
                <div class="card-sub" id="realBalanceSub">-</div>
            </div>
            <div class="card full-width">
                <div class="card-label">
                    <span>📊</span> Comparação: Real vs Projetado
                </div>
                <div style="display: flex; justify-content: space-between; margin-bottom: 6px;">
                    <span style="font-size: 12px; color: var(--text-muted);">Projetado: <span id="compProjected">€ 0,00</span></span>
                    <span style="font-size: 12px; color: var(--warning);">Real: <span id="compReal">€ 0,00</span></span>
                </div>
                <div class="comparison-bar">
                    <div class="comparison-fill expected" id="compBarExpected"></div>
                    <div class="comparison-fill real" id="compBarReal"></div>
                </div>
                <div class="card-sub" id="compDiff" style="margin-top: 8px; text-align: center;">Diferença: € 0,00</div>
            </div>
        </div>

        <!-- Tabs -->
        <div class="tabs">
            <button class="tab active" onclick="app.setTab('transactions')">Transações</button>
            <button class="tab" onclick="app.setTab('planning')">Planejamento</button>
            <button class="tab" onclick="app.setTab('overview')">Visão Geral</button>
        </div>

        <!-- Content -->
        <div class="content">
            <!-- Transactions Section -->
            <div class="section active" id="section-transactions">
                <div class="real-balance-section">
                    <div class="card-label">💰 Saldo Real na Conta</div>
                    <div style="font-size: 13px; color: var(--text-secondary); margin-bottom: 8px;">
                        Digite seu saldo bancário real para comparar com o balanço projetado
                    </div>
                    <div class="real-balance-input">
                        <input type="number" class="form-input" id="realBalanceInput" placeholder="0,00" step="0.01">
                        <button onclick="app.saveRealBalance()">Atualizar</button>
                    </div>
                </div>

                <div class="section-title">
                    <span>Transações do Mês</span>
                    <button onclick="app.openModal()">+</button>
                </div>

                <div class="swipe-hint">← Deslize para excluir</div>

                <div class="transaction-list" id="transactionList">
                    <div class="empty-state">
                        <div class="empty-state-icon">📝</div>
                        <div>Nenhuma transação ainda</div>
                        <div style="font-size: 13px; margin-top: 4px;">Toque em + para adicionar</div>
                    </div>
                </div>
            </div>

            <!-- Planning Section -->
            <div class="section" id="section-planning">
                <div class="section-title">
                    <span>Orçamento do Mês</span>
                    <button onclick="app.openPlanningModal()">+</button>
                </div>
                <div id="planningList">
                    <div class="empty-state">
                        <div class="empty-state-icon">🎯</div>
                        <div>Sem metas de orçamento</div>
                        <div style="font-size: 13px; margin-top: 4px;">Defina limites por categoria</div>
                    </div>
                </div>
            </div>

            <!-- Overview Section -->
            <div class="section" id="section-overview">
                <div class="section-title">Últimos 6 Meses</div>
                <div class="chart-container">
                    <div class="chart-bars" id="chartBars"></div>
                </div>

                <div class="section-title" style="margin-top: 24px;">Resumo do Ano</div>
                <div class="cards-container" style="padding: 0;">
                    <div class="card">
                        <div class="card-label">Total Receitas</div>
                        <div class="card-value positive" id="yearIncome">€ 0,00</div>
                    </div>
                    <div class="card">
                        <div class="card-label">Total Despesas</div>
                        <div class="card-value negative" id="yearExpense">€ 0,00</div>
                    </div>
                    <div class="card full-width">
                        <div class="card-label">Balanço Anual</div>
                        <div class="card-value" id="yearBalance">€ 0,00</div>
                    </div>
                </div>
            </div>
        </div>

        <!-- Bottom Nav -->
        <div class="bottom-nav">
            <button class="nav-item active" onclick="app.setTab('transactions')">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <rect x="3" y="3" width="18" height="18" rx="2"/>
                    <line x1="3" y1="9" x2="21" y2="9"/>
                    <line x1="9" y1="21" x2="9" y2="9"/>
                </svg>
                <span>Início</span>
            </button>
            <button class="nav-item" onclick="app.setTab('planning')">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <circle cx="12" cy="12" r="10"/>
                    <path d="M12 6v6l4 2"/>
                </svg>
                <span>Metas</span>
            </button>
            <button class="nav-item" onclick="app.setTab('overview')">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M18 20V10M12 20V4M6 20v-6"/>
                </svg>
                <span>Gráficos</span>
            </button>
            <button class="nav-item" onclick="app.exportData()">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
                    <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4"/>
                    <polyline points="7 10 12 15 17 10"/>
                    <line x1="12" y1="15" x2="12" y2="3"/>
                </svg>
                <span>Backup</span>
            </button>
        </div>

        <!-- Transaction Modal -->
        <div class="modal-overlay" id="transactionModal">
            <div class="modal">
                <div class="modal-header">
                    <div class="modal-title">Nova Transação</div>
                    <button class="modal-close" onclick="app.closeModal()">&times;</button>
                </div>

                <div class="type-selector">
                    <div class="type-option selected" onclick="app.selectType('income')" id="typeIncome">
                        📥 Receita
                    </div>
                    <div class="type-option" onclick="app.selectType('expense')" id="typeExpense">
                        📤 Despesa
                    </div>
                </div>

                <div class="form-group">
                    <label class="form-label">Descrição</label>
                    <input type="text" class="form-input" id="transDesc" placeholder="Ex: Salário, Aluguel...">
                </div>

                <div class="form-group">
                    <label class="form-label">Valor (R$)</label>
                    <input type="number" class="form-input" id="transAmount" placeholder="0,00" step="0.01">
                </div>

                <div class="form-group">
                    <label class="form-label">Categoria</label>
                    <div class="category-tags" id="categoryTags">
                        <span class="category-tag selected" data-cat="salario">Salário</span>
                        <span class="category-tag" data-cat="freelance">Freelance</span>
                        <span class="category-tag" data-cat="investimentos">Investimentos</span>
                        <span class="category-tag" data-cat="outros">Outros</span>
                    </div>
                </div>

                <div class="form-group">
                    <label class="form-label">Data</label>
                    <input type="date" class="form-input" id="transDate">
                </div>

                <button class="btn-primary" onclick="app.saveTransaction()">Salvar Transação</button>
            </div>
        </div>

        <!-- Planning Modal -->
        <div class="modal-overlay" id="planningModal">
            <div class="modal">
                <div class="modal-header">
                    <div class="modal-title">Novo Orçamento</div>
                    <button class="modal-close" onclick="app.closePlanningModal()">&times;</button>
                </div>

                <div class="form-group">
                    <label class="form-label">Categoria</label>
                    <select class="form-select" id="planCategory">
                        <option value="alimentacao">Alimentação</option>
                        <option value="transporte">Transporte</option>
                        <option value="moradia">Moradia</option>
                        <option value="lazer">Lazer</option>
                        <option value="saude">Saúde</option>
                        <option value="educacao">Educação</option>
                        <option value="compras">Compras</option>
                        <option value="outros">Outros</option>
                    </select>
                </div>

                <div class="form-group">
                    <label class="form-label">Limite Mensal (R$)</label>
                    <input type="number" class="form-input" id="planAmount" placeholder="0,00" step="0.01">
                </div>

                <button class="btn-primary" onclick="app.savePlanning()">Salvar Orçamento</button>
            </div>
        </div>
    </div>

    <script>
        class FinanceApp {
            constructor() {
                this.currentDate = new Date();
                this.currentMonth = this.currentDate.getMonth();
                this.currentYear = this.currentDate.getFullYear();
                this.transactions = this.loadData('transactions') || {};
                this.plannings = this.loadData('plannings') || {};
                this.realBalances = this.loadData('realBalances') || {};
                this.currentTab = 'transactions';
                this.selectedType = 'income';
                this.selectedCategory = 'salario';
                this.touchStartX = 0;
                this.touchEndX = 0;

                this.init();
            }

            init() {
                this.updateMonthTitle();
                this.render();
                this.setupEventListeners();
                this.setupSwipe();

                // Set default date to today
                document.getElementById('transDate').valueAsDate = new Date();
            }

            loadData(key) {
                try {
                    return JSON.parse(localStorage.getItem('finances_' + key));
                } catch {
                    return null;
                }
            }

            saveData(key, data) {
                localStorage.setItem('finances_' + key, JSON.stringify(data));
            }

            getMonthKey() {
                return `${this.currentYear}-${String(this.currentMonth + 1).padStart(2, '0')}`;
            }

            getMonthTransactions() {
                return this.transactions[this.getMonthKey()] || [];
            }

            getMonthPlannings() {
                return this.plannings[this.getMonthKey()] || [];
            }

            prevMonth() {
                this.currentMonth--;
                if (this.currentMonth < 0) {
                    this.currentMonth = 11;
                    this.currentYear--;
                }
                this.updateMonthTitle();
                this.render();
            }

            nextMonth() {
                this.currentMonth++;
                if (this.currentMonth > 11) {
                    this.currentMonth = 0;
                    this.currentYear++;
                }
                this.updateMonthTitle();
                this.render();
            }

            updateMonthTitle() {
                const months = ['Janeiro', 'Fevereiro', 'Março', 'Abril', 'Maio', 'Junho',
                              'Julho', 'Agosto', 'Setembro', 'Outubro', 'Novembro', 'Dezembro'];
                document.getElementById('monthTitle').textContent = 
                    `${months[this.currentMonth]} ${this.currentYear}`;
            }

            setTab(tab) {
                this.currentTab = tab;

                // Update tabs
                document.querySelectorAll('.tab').forEach(t => t.classList.remove('active'));
                event.target.classList.add('active');

                // Update nav
                document.querySelectorAll('.nav-item').forEach(n => n.classList.remove('active'));
                const navIndex = {transactions: 0, planning: 1, overview: 2}[tab];
                if (navIndex !== undefined) {
                    document.querySelectorAll('.nav-item')[navIndex].classList.add('active');
                }

                // Update sections
                document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
                document.getElementById(`section-${tab}`).classList.add('active');

                if (tab === 'overview') {
                    this.renderChart();
                    this.renderYearSummary();
                }
            }

            formatMoney(value) {
                return '€ ' + Math.abs(value).toLocaleString('de-DE', {
                    minimumFractionDigits: 2,
                    maximumFractionDigits: 2
                });
            }

            render() {
                const transactions = this.getMonthTransactions();
                const plannings = this.getMonthPlannings();
                const realBalance = this.realBalances[this.getMonthKey()];

                // Calculate totals
                let income = 0, expense = 0;
                transactions.forEach(t => {
                    if (t.type === 'income') income += t.amount;
                    else expense += t.amount;
                });

                const balance = income - expense;

                // Update cards
                document.getElementById('totalIncome').textContent = this.formatMoney(income);
                document.getElementById('totalExpense').textContent = this.formatMoney(expense);

                const balanceEl = document.getElementById('balance');
                balanceEl.textContent = this.formatMoney(balance);
                balanceEl.className = 'card-value ' + (balance >= 0 ? 'positive' : 'negative');

                // Real balance
                const realBalanceEl = document.getElementById('realBalance');
                if (realBalance !== undefined) {
                    realBalanceEl.textContent = this.formatMoney(realBalance);
                    document.getElementById('realBalanceSub').textContent = 'Atualizado';

                    // Comparison
                    const diff = realBalance - balance;
                    const diffEl = document.getElementById('compDiff');
                    diffEl.textContent = `Diferença: ${diff >= 0 ? '+' : '-'}${this.formatMoney(diff)}`;
                    diffEl.style.color = diff >= 0 ? 'var(--primary)' : 'var(--danger)';

                    document.getElementById('compProjected').textContent = this.formatMoney(balance);
                    document.getElementById('compReal').textContent = this.formatMoney(realBalance);

                    // Bars
                    const max = Math.max(Math.abs(balance), Math.abs(realBalance));
                    const expectedPct = max > 0 ? (Math.abs(balance) / max) * 100 : 0;
                    const realPct = max > 0 ? (Math.abs(realBalance) / max) * 100 : 0;

                    document.getElementById('compBarExpected').style.width = expectedPct + '%';
                    document.getElementById('compBarReal').style.width = realPct + '%';
                } else {
                    realBalanceEl.textContent = '€ --';
                    document.getElementById('realBalanceSub').textContent = 'Não informado';
                    document.getElementById('compDiff').textContent = 'Diferença: € --';
                    document.getElementById('compBarExpected').style.width = '0%';
                    document.getElementById('compBarReal').style.width = '0%';
                }

                // Render transactions
                this.renderTransactions(transactions);

                // Render planning
                this.renderPlanning(plannings, transactions);
            }

            renderTransactions(transactions) {
                const list = document.getElementById('transactionList');

                if (transactions.length === 0) {
                    list.innerHTML = `
                        <div class="empty-state">
                            <div class="empty-state-icon">📝</div>
                            <div>Nenhuma transação ainda</div>
                            <div style="font-size: 13px; margin-top: 4px;">Toque em + para adicionar</div>
                        </div>
                    `;
                    return;
                }

                // Sort by date desc
                const sorted = [...transactions].sort((a, b) => new Date(b.date) - new Date(a.date));

                const icons = {
                    salario: '💰', freelance: '💻', investimentos: '📈', alimentacao: '🍽️',
                    transporte: '🚗', moradia: '🏠', lazer: '🎮', saude: '💊', educacao: '📚',
                    compras: '🛍️', outros: '📦'
                };

                list.innerHTML = sorted.map((t, index) => `
                    <div class="transaction-item" data-index="${index}" ontouchstart="app.handleTouchStart(event)" ontouchend="app.handleTouchEnd(event, ${index})">
                        <div class="transaction-icon ${t.type}">
                            ${icons[t.category] || '📦'}
                        </div>
                        <div class="transaction-info">
                            <div class="transaction-title">${t.description}</div>
                            <div class="transaction-date">${this.formatDate(t.date)} · ${this.getCategoryName(t.category)}</div>
                        </div>
                        <div class="transaction-amount ${t.type}">
                            ${t.type === 'income' ? '+' : '-'} ${this.formatMoney(t.amount)}
                        </div>
                        <button class="delete-btn" onclick="app.deleteTransaction(${index})">🗑️</button>
                    </div>
                `).join('');
            }

            renderPlanning(plannings, transactions) {
                const list = document.getElementById('planningList');

                if (plannings.length === 0) {
                    list.innerHTML = `
                        <div class="empty-state">
                            <div class="empty-state-icon">🎯</div>
                            <div>Sem metas de orçamento</div>
                            <div style="font-size: 13px; margin-top: 4px;">Defina limites por categoria</div>
                        </div>
                    `;
                    return;
                }

                // Calculate spent per category
                const spent = {};
                transactions.filter(t => t.type === 'expense').forEach(t => {
                    spent[t.category] = (spent[t.category] || 0) + t.amount;
                });

                list.innerHTML = plannings.map((p, index) => {
                    const actual = spent[p.category] || 0;
                    const pct = Math.min((actual / p.amount) * 100, 100);
                    const over = actual > p.amount;

                    return `
                        <div class="planning-card">
                            <div class="planning-header">
                                <div class="planning-title">${this.getCategoryName(p.category)}</div>
                                <div class="planning-amount">${this.formatMoney(actual)} / ${this.formatMoney(p.amount)}</div>
                            </div>
                            <div class="progress-bar">
                                <div class="progress-fill ${over ? 'over' : ''}" style="width: ${pct}%"></div>
                            </div>
                            <div class="planning-meta">
                                <span>${pct.toFixed(0)}% utilizado</span>
                                <span style="color: ${over ? 'var(--danger)' : 'var(--text-muted)'}">
                                    ${over ? '🔴 Ultrapassou' : '🟢 Dentro do limite'}
                                </span>
                            </div>
                            <button onclick="app.deletePlanning(${index})" style="margin-top: 10px; background: none; border: none; color: var(--danger); font-size: 12px; cursor: pointer; width: 100%; text-align: right;">
                                Excluir meta
                            </button>
                        </div>
                    `;
                }).join('');
            }

            renderChart() {
                const months = [];
                const incomeData = [];
                const expenseData = [];

                for (let i = 5; i >= 0; i--) {
                    const d = new Date(this.currentYear, this.currentMonth - i, 1);
                    const key = `${d.getFullYear()}-${String(d.getMonth() + 1).padStart(2, '0')}`;
                    const trans = this.transactions[key] || [];

                    let inc = 0, exp = 0;
                    trans.forEach(t => {
                        if (t.type === 'income') inc += t.amount;
                        else exp += t.amount;
                    });

                    months.push(d.toLocaleDateString('de-DE', {month: 'short'}));
                    incomeData.push(inc);
                    expenseData.push(exp);
                }

                const max = Math.max(...incomeData, ...expenseData, 1);

                const container = document.getElementById('chartBars');
                container.innerHTML = months.map((m, i) => {
                    const incH = (incomeData[i] / max) * 120;
                    const expH = (expenseData[i] / max) * 120;

                    return `
                        <div class="chart-bar-wrapper">
                            <div style="display: flex; gap: 4px; align-items: flex-end; height: 120px;">
                                <div class="chart-bar income-bar" style="height: ${incH}px;"></div>
                                <div class="chart-bar expense-bar" style="height: ${expH}px;"></div>
                            </div>
                            <div class="chart-label">${m}</div>
                        </div>
                    `;
                }).join('');
            }

            renderYearSummary() {
                let yearIncome = 0, yearExpense = 0;

                for (let m = 0; m < 12; m++) {
                    const key = `${this.currentYear}-${String(m + 1).padStart(2, '0')}`;
                    const trans = this.transactions[key] || [];
                    trans.forEach(t => {
                        if (t.type === 'income') yearIncome += t.amount;
                        else yearExpense += t.amount;
                    });
                }

                const balance = yearIncome - yearExpense;

                document.getElementById('yearIncome').textContent = this.formatMoney(yearIncome);
                document.getElementById('yearExpense').textContent = this.formatMoney(yearExpense);

                const balEl = document.getElementById('yearBalance');
                balEl.textContent = this.formatMoney(balance);
                balEl.className = 'card-value ' + (balance >= 0 ? 'positive' : 'negative');
            }

            getCategoryName(cat) {
                const names = {
                    salario: 'Salário', freelance: 'Freelance', investimentos: 'Investimentos',
                    alimentacao: 'Alimentação', transporte: 'Transporte', moradia: 'Moradia',
                    lazer: 'Lazer', saude: 'Saúde', educacao: 'Educação', compras: 'Compras',
                    outros: 'Outros'
                };
                return names[cat] || cat;
            }

            formatDate(dateStr) {
                const d = new Date(dateStr + 'T12:00:00');
                return d.toLocaleDateString('de-DE');
            }

            openModal() {
                document.getElementById('transactionModal').classList.add('active');
                document.getElementById('transDesc').focus();
            }

            closeModal() {
                document.getElementById('transactionModal').classList.remove('active');
                // Reset form
                document.getElementById('transDesc').value = '';
                document.getElementById('transAmount').value = '';
                this.selectType('income');
            }

            openPlanningModal() {
                document.getElementById('planningModal').classList.add('active');
            }

            closePlanningModal() {
                document.getElementById('planningModal').classList.remove('active');
                document.getElementById('planAmount').value = '';
            }

            selectType(type) {
                this.selectedType = type;
                document.getElementById('typeIncome').classList.toggle('selected', type === 'income');
                document.getElementById('typeExpense').classList.toggle('selected', type === 'expense');
                document.getElementById('typeExpense').classList.toggle('expense-selected', type === 'expense');

                // Update categories
                const incomeCats = ['salario', 'freelance', 'investimentos', 'outros'];
                const expenseCats = ['alimentacao', 'transporte', 'moradia', 'lazer', 'saude', 'educacao', 'compras', 'outros'];
                const cats = type === 'income' ? incomeCats : expenseCats;

                const container = document.getElementById('categoryTags');
                container.innerHTML = cats.map((cat, i) => 
                    `<span class="category-tag ${i === 0 ? 'selected' : ''}" data-cat="${cat}" onclick="app.selectCategory('${cat}')">${this.getCategoryName(cat)}</span>`
                ).join('');

                this.selectedCategory = cats[0];
            }

            selectCategory(cat) {
                this.selectedCategory = cat;
                document.querySelectorAll('.category-tag').forEach(t => {
                    t.classList.toggle('selected', t.dataset.cat === cat);
                });
            }

            saveTransaction() {
                const desc = document.getElementById('transDesc').value.trim();
                const amount = parseFloat(document.getElementById('transAmount').value);
                const date = document.getElementById('transDate').value;

                if (!desc || !amount || amount <= 0 || !date) {
                    alert('Preencha todos os campos corretamente');
                    return;
                }

                const key = this.getMonthKey();
                if (!this.transactions[key]) this.transactions[key] = [];

                this.transactions[key].push({
                    id: Date.now(),
                    description: desc,
                    amount: amount,
                    type: this.selectedType,
                    category: this.selectedCategory,
                    date: date
                });

                this.saveData('transactions', this.transactions);
                this.closeModal();
                this.render();
            }

            deleteTransaction(index) {
                const key = this.getMonthKey();
                const trans = this.getMonthTransactions();
                // Find actual index in unsorted array
                const sorted = [...trans].sort((a, b) => new Date(b.date) - new Date(a.date));
                const item = sorted[index];
                const actualIndex = this.transactions[key].findIndex(t => t.id === item.id);

                if (actualIndex > -1) {
                    this.transactions[key].splice(actualIndex, 1);
                    this.saveData('transactions', this.transactions);
                    this.render();
                }
            }

            savePlanning() {
                const category = document.getElementById('planCategory').value;
                const amount = parseFloat(document.getElementById('planAmount').value);

                if (!amount || amount <= 0) {
                    alert('Informe um valor válido');
                    return;
                }

                const key = this.getMonthKey();
                if (!this.plannings[key]) this.plannings[key] = [];

                // Remove existing for same category
                this.plannings[key] = this.plannings[key].filter(p => p.category !== category);

                this.plannings[key].push({
                    category: category,
                    amount: amount
                });

                this.saveData('plannings', this.plannings);
                this.closePlanningModal();
                this.render();
            }

            deletePlanning(index) {
                const key = this.getMonthKey();
                this.plannings[key].splice(index, 1);
                this.saveData('plannings', this.plannings);
                this.render();
            }

            saveRealBalance() {
                const value = parseFloat(document.getElementById('realBalanceInput').value);
                if (isNaN(value)) {
                    alert('Informe um valor válido');
                    return;
                }

                this.realBalances[this.getMonthKey()] = value;
                this.saveData('realBalances', this.realBalances);
                document.getElementById('realBalanceInput').value = '';
                this.render();
            }

            exportData() {
                const data = {
                    transactions: this.transactions,
                    plannings: this.plannings,
                    realBalances: this.realBalances,
                    exportDate: new Date().toISOString()
                };

                const blob = new Blob([JSON.stringify(data, null, 2)], {type: 'application/json'});
                const url = URL.createObjectURL(blob);
                const a = document.createElement('a');
                a.href = url;
                a.download = `financas_backup_${this.getMonthKey()}.json`;
                a.click();
                URL.revokeObjectURL(url);
            }

            setupEventListeners() {
                // Category tag clicks
                document.getElementById('categoryTags').addEventListener('click', (e) => {
                    if (e.target.classList.contains('category-tag')) {
                        this.selectCategory(e.target.dataset.cat);
                    }
                });

                // Close modal on overlay click
                document.getElementById('transactionModal').addEventListener('click', (e) => {
                    if (e.target === e.currentTarget) this.closeModal();
                });

                document.getElementById('planningModal').addEventListener('click', (e) => {
                    if (e.target === e.currentTarget) this.closePlanningModal();
                });
            }

            setupSwipe() {
                // Month navigation swipe
                const container = document.querySelector('.app-container');
                let startX = 0;

                container.addEventListener('touchstart', (e) => {
                    startX = e.touches[0].clientX;
                }, {passive: true});

                container.addEventListener('touchend', (e) => {
                    const endX = e.changedTouches[0].clientX;
                    const diff = startX - endX;

                    if (Math.abs(diff) > 80) {
                        if (diff > 0) this.nextMonth();
                        else this.prevMonth();
                    }
                }, {passive: true});
            }

            handleTouchStart(e) {
                this.touchStartX = e.touches[0].clientX;
            }

            handleTouchEnd(e, index) {
                this.touchEndX = e.changedTouches[0].clientX;
                const diff = this.touchStartX - this.touchEndX;

                if (Math.abs(diff) > 60) {
                    const item = e.currentTarget;
                    if (diff > 0) {
                        item.classList.add('swiped');
                        // Auto remove swipe after 3s
                        setTimeout(() => item.classList.remove('swiped'), 3000);
                    } else {
                        item.classList.remove('swiped');
                    }
                }
            }
        }

        // Initialize
        const app = new FinanceApp();
    </script>
</body>
</html>
