<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>LINE受付管理ボット インタラクティブドキュメント</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Chosen Palette: Warm Neutral & Deep Teal -->
    <!-- Application Structure Plan: 左側にナビゲーションを持つシングルページ構成。セクションは「概要」「システム構成」「インタラクティブフロー」「運用・保守」に分割。中心機能である「インタラクティブフロー」では、ユーザーがシナリオを選択し、クリック操作でボットのロジックをステップ・バイ・ステップで追体験できるシミュレーターを配置。この対話的な構造は、静的なフローチャートを読むよりも深く、かつ直感的な理解を促進するために選択されました。 -->
    <!-- Visualization & Content Choices: 
        - 概要: Goal:Inform -> Method:アイコン付きカード -> Interaction:None -> Justification:主要機能を視覚的に分かりやすく提示。
        - システム構成: Goal:Organize -> Method:HTML/CSSによる図解とテーブル -> Interaction:None -> Justification:外部ライブラリを使わず、システムの全体像とデータ構造を明確化。
        - インタラクティブフロー: Goal:Interact/Simulate -> Method:JSによる対話型シミュレーション -> Interaction:ユーザーがボタンをクリックしてシナリオを進行 -> Justification:複雑な条件分岐と状態変化をユーザー自身が体験することで、抽象的なロジックを具体的に理解できる。本アプリケーションの核。
        - 運用・保守: Goal:Organize -> Method:アコーディオンUI -> Interaction:クリックで開閉 -> Justification:詳細情報をデフォルトで隠し、必要な情報に素早くアクセス可能にすることで、可読性を向上。
    -->
    <!-- CONFIRMATION: NO SVG graphics used. NO Mermaid JS used. -->
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@400;500;700&display=swap');
        body {
            font-family: 'Noto Sans JP', sans-serif;
            background-color: #f8f7f4;
            color: #333;
        }
        .content-section {
            display: none;
        }
        .content-section.active {
            display: block;
        }
        .nav-link {
            transition: all 0.3s;
        }
        .nav-link.active {
            background-color: #008080;
            color: white;
            transform: translateX(4px);
        }
        .accordion-content {
            max-height: 0;
            overflow: hidden;
            transition: max-height 0.3s ease-in-out;
        }
        .accordion-title.open + .accordion-content {
            max-height: 1000px;
        }
        .sim-button {
            transition: all 0.2s;
        }
        .sim-button:hover {
            transform: translateY(-2px);
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        }
        .chat-bubble {
            animation: fadeIn 0.5s ease-in-out;
        }
        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(10px); }
            to { opacity: 1; transform: translateY(0); }
        }
        .table-cell-highlight {
            background-color: #fefcbf;
            transition: background-color 0.5s;
        }
    </style>
</head>
<body class="antialiased">

    <div class="flex flex-col md:flex-row min-h-screen">
        <!-- Sidebar Navigation -->
        <aside class="w-full md:w-64 bg-gray-100 p-4 md:p-6 sticky top-0 h-screen shadow-lg">
            <h1 class="text-xl font-bold text-teal-800 mb-6">運用ドキュメント</h1>
            <nav id="nav-menu">
                <a href="#overview" class="nav-link block p-3 rounded-lg mb-2 font-medium text-gray-700 hover:bg-teal-100">概要</a>
                <a href="#architecture" class="nav-link block p-3 rounded-lg mb-2 font-medium text-gray-700 hover:bg-teal-100">システム構成</a>
                <a href="#interactive-flow" class="nav-link block p-3 rounded-lg mb-2 font-medium text-gray-700 hover:bg-teal-100">インタラクティブフロー</a>
                <a href="#maintenance" class="nav-link block p-3 rounded-lg mb-2 font-medium text-gray-700 hover:bg-teal-100">運用とメンテナンス</a>
                <a href="#ideas" class="nav-link block p-3 rounded-lg mb-2 font-medium text-gray-700 hover:bg-teal-100">今後の拡張アイデア</a>
            </nav>
        </aside>

        <!-- Main Content -->
        <main class="flex-1 p-4 md:p-10">
            <!-- Overview Section -->
            <section id="overview" class="content-section">
                <h2 class="text-3xl font-bold mb-6 text-teal-900 border-b-4 border-teal-300 pb-2">1. 概要</h2>
                <p class="mb-8 text-lg text-gray-700">このドキュメントは、LINEとGoogleスプレッドシートを連携させた受付管理ボットの機能、動作フロー、および運用に必要な技術的詳細を後任者向けにまとめたものです。この対話的なWebページを通じて、ボットの複雑なロジックを直感的に理解することができます。</p>
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
                    <div class="bg-white p-6 rounded-xl shadow-md border-l-4 border-teal-500">
                        <h3 class="text-xl font-semibold mb-2 text-teal-800">参加登録とポイント付与</h3>
                        <p class="text-gray-600">ユーザーはLINEから「参加」と入力するだけで、セミナーへの参加登録とポイント獲得が可能です。</p>
                    </div>
                    <div class="bg-white p-6 rounded-xl shadow-md border-l-4 border-teal-500">
                        <h3 class="text-xl font-semibold mb-2 text-teal-800">条件分岐ロジック</h3>
                        <p class="text-gray-600">「所属」が「静岡市」のユーザーには追加の質問を行い、回答に応じて異なる処理を実行します。</p>
                    </div>
                    <div class="bg-white p-6 rounded-xl shadow-md border-l-4 border-teal-500">
                        <h3 class="text-xl font-semibold mb-2 text-teal-800">データ連携</h3>
                        <p class="text-gray-600">全ての登録情報やポイントは、リアルタイムでGoogleスプレッドシートに記録・管理されます。</p>
                    </div>
                     <div class="bg-white p-6 rounded-xl shadow-md border-l-4 border-teal-500">
                        <h3 class="text-xl font-semibold mb-2 text-teal-800">ポイント制限とリセット</h3>
                        <p class="text-gray-600">1日のポイント獲得数には上限があり、目標達成後には自動でリセットされるゲーミフィケーション要素を備えています。</p>
                    </div>
                </div>
            </section>

            <!-- Architecture Section -->
            <section id="architecture" class="content-section">
                <h2 class="text-3xl font-bold mb-6 text-teal-900 border-b-4 border-teal-300 pb-2">2. システム構成</h2>
                <p class="mb-8 text-lg text-gray-700">このボットは、LINE Messaging API、Google Apps Script、Googleスプレッドシートの3つの主要コンポーネントで構成されています。それぞれの役割とデータの流れを以下に示します。</p>
                
                <div class="bg-white p-8 rounded-xl shadow-lg mb-12">
                    <h3 class="text-2xl font-semibold mb-6 text-center text-teal-800">システム連携図</h3>
                    <div class="flex flex-col md:flex-row items-center justify-center space-y-4 md:space-y-0 md:space-x-8">
                        <div class="text-center">
                            <div class="p-4 bg-green-500 text-white rounded-lg shadow-md">LINEユーザー</div>
                        </div>
                        <div class="font-bold text-2xl text-teal-500 transform rotate-90 md:rotate-0">&rarr;</div>
                        <div class="text-center">
                            <div class="p-4 bg-gray-700 text-white rounded-lg shadow-md">LINE Platform</div>
                            <p class="text-xs mt-1 text-gray-500">(Webhook)</p>
                        </div>
                        <div class="font-bold text-2xl text-teal-500 transform rotate-90 md:rotate-0">&rarr;</div>
                        <div class="text-center">
                            <div class="p-4 bg-yellow-500 text-gray-800 rounded-lg shadow-md">Google Apps Script</div>
                            <p class="text-xs mt-1 text-gray-500">(ロジック処理)</p>
                        </div>
                        <div class="font-bold text-2xl text-teal-500 transform rotate-90 md:rotate-0">&harr;</div>
                        <div class="text-center">
                             <div class="p-4 bg-blue-500 text-white rounded-lg shadow-md">Google Sheets</div>
                             <p class="text-xs mt-1 text-gray-500">(データベース)</p>
                        </div>
                    </div>
                </div>

                <h3 class="text-2xl font-semibold mb-4 text-teal-800">Googleスプレッドシートの構造</h3>
                <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                    <div class="bg-white p-6 rounded-xl shadow-lg">
                        <h4 class="text-xl font-bold mb-3 text-gray-800">① `会員情報` シート</h4>
                        <p class="text-sm text-gray-600 mb-4">ユーザーの基本情報と現在のポイントを管理します。</p>
                        <div class="overflow-x-auto">
                            <table class="min-w-full bg-white border">
                                <thead class="bg-teal-50">
                                    <tr>
                                        <th class="py-2 px-4 border">列名</th>
                                        <th class="py-2 px-4 border">説明</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr><td class="border px-4 py-2 font-semibold">LINE ID</td><td class="border px-4 py-2">ユーザーを一意に識別するID。</td></tr>
                                    <tr><td class="border px-4 py-2 font-semibold">名前</td><td class="border px-4 py-2">ユーザーの氏名。</td></tr>
                                    <tr><td class="border px-4 py-2 font-semibold">所属</td><td class="border px-4 py-2">「静岡市」の場合に分岐ロジックが発動。</td></tr>
                                    <tr><td class="border px-4 py-2 font-semibold">ポイント</td><td class="border px-4 py-2">現在の累計ポイント。</td></tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                    <div class="bg-white p-6 rounded-xl shadow-lg">
                        <h4 class="text-xl font-bold mb-3 text-gray-800">② `受付履歴` シート</h4>
                        <p class="text-sm text-gray-600 mb-4">各ユーザーのセミナー参加履歴を記録します。</p>
                         <div class="overflow-x-auto">
                            <table class="min-w-full bg-white border">
                                <thead class="bg-teal-50">
                                    <tr>
                                        <th class="py-2 px-4 border">列名</th>
                                        <th class="py-2 px-4 border">説明</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr><td class="border px-4 py-2 font-semibold">タイムスタンプ</td><td class="border px-4 py-2">参加登録が行われた日時。</td></tr>
                                    <tr><td class="border px-4 py-2 font-semibold">LINE ID</td><td class="border px-4 py-2">参加したユーザーのID。</td></tr>
                                    <tr><td class="border px-4 py-2 font-semibold">名前</td><td class="border px-4 py-2">参加したユーザーの名前。</td></tr>
                                    <tr><td class="border px-4 py-2 font-semibold">参加行事</td><td class="border px-4 py-2">参加した行事名。</td></tr>
                                    <tr><td class="border px-4 py-2 font-semibold">今回ポイント</td><td class="border px-4 py-2">その時点での累計ポイント。</td></tr>
                                </tbody>
                            </table>
                        </div>
                    </div>
                </div>
            </section>
            
            <!-- Interactive Flow Section -->
            <section id="interactive-flow" class="content-section">
                <h2 class="text-3xl font-bold mb-6 text-teal-900 border-b-4 border-teal-300 pb-2">3. インタラクティブフロー</h2>
                <p class="mb-4 text-lg text-gray-700">ボットの動作を実際に体験してみましょう。下のシナリオを選択し、「シミュレーション開始」ボタンを押して、ユーザーとしてボットと対話を進めてください。右側には、操作に応じて更新されるスプレッドシートの状態が表示されます。</p>
                
                <div class="bg-white p-6 rounded-xl shadow-lg mb-6">
                    <div class="flex flex-col sm:flex-row items-center gap-4">
                         <div class="flex-1">
                            <label for="scenario-select" class="block text-sm font-medium text-gray-700 mb-1">シナリオ選択</label>
                            <select id="scenario-select" class="w-full p-2 border border-gray-300 rounded-md shadow-sm focus:ring-teal-500 focus:border-teal-500">
                                <option value="newUser">1. 新規ユーザーの登録</option>
                                <option value="existingUserOther">2. 既存ユーザーの登録 (所属: 静岡市以外)</option>
                                <option value="existingUserShizuoka">3. 既存ユーザーの登録 (所属: 静岡市)</option>
                                <option value="limitCheck">4. 1日のポイント付与制限チェック (2回登録済み)</option>
                                <option value="goalCheck">5. ポイント目標達成 (19ポイントから開始)</option>
                            </select>
                        </div>
                        <button id="start-sim-btn" class="w-full sm:w-auto bg-teal-600 text-white font-bold py-2 px-6 rounded-lg hover:bg-teal-700 sim-button mt-4 sm:mt-0 self-end">シミュレーション開始</button>
                    </div>
                </div>

                <div class="grid grid-cols-1 lg:grid-cols-2 gap-8">
                    <!-- Simulation Chat UI -->
                    <div class="bg-gray-50 p-6 rounded-xl shadow-inner min-h-[400px]">
                         <h3 class="text-xl font-semibold mb-4 text-gray-800">ボットとの対話</h3>
                         <div id="chat-log" class="space-y-4 h-[400px] overflow-y-auto pr-2">
                            <!-- Chat messages will be appended here -->
                         </div>
                         <div id="user-actions" class="mt-4 pt-4 border-t">
                            <!-- User action buttons will be appended here -->
                         </div>
                    </div>

                    <!-- Mock Spreadsheet UI -->
                    <div>
                         <div class="bg-gray-50 p-6 rounded-xl shadow-inner mb-6">
                            <h3 class="text-xl font-semibold mb-4 text-gray-800">会員情報シート</h3>
                            <div class="overflow-x-auto">
                                <table class="min-w-full text-sm">
                                    <thead class="bg-gray-200">
                                        <tr>
                                            <th class="p-2 border">LINE ID</th>
                                            <th class="p-2 border">名前</th>
                                            <th class="p-2 border">所属</th>
                                            <th class="p-2 border">ポイント</th>
                                        </tr>
                                    </thead>
                                    <tbody id="member-sheet-body">
                                        <!-- Member data rows will be appended here -->
                                    </tbody>
                                </table>
                            </div>
                         </div>
                         <div class="bg-gray-50 p-6 rounded-xl shadow-inner">
                            <h3 class="text-xl font-semibold mb-4 text-gray-800">受付履歴シート</h3>
                             <div class="overflow-x-auto">
                                <table class="min-w-full text-sm">
                                    <thead class="bg-gray-200">
                                        <tr>
                                            <th class="p-2 border">タイムスタンプ</th>
                                            <th class="p-2 border">LINE ID</th>
                                            <th class="p-2 border">名前</th>
                                            <th class="p-2 border">参加行事</th>
                                            <th class="p-2 border">今回ポイント</th>
                                        </tr>
                                    </thead>
                                    <tbody id="history-sheet-body">
                                        <!-- History data rows will be appended here -->
                                    </tbody>
                                </table>
                             </div>
                         </div>
                    </div>
                </div>
            </section>

            <!-- Maintenance Section -->
            <section id="maintenance" class="content-section">
                <h2 class="text-3xl font-bold mb-6 text-teal-900 border-b-4 border-teal-300 pb-2">4. 運用とメンテナンス</h2>
                <p class="mb-8 text-lg text-gray-700">ボットの安定した運用と将来の改修のために、以下のポイントを理解しておくことが重要です。</p>
                <div class="space-y-4">
                    <div class="bg-white rounded-lg shadow-md">
                        <h3 class="accordion-title p-5 w-full text-left font-semibold text-lg text-teal-800 flex justify-between items-center cursor-pointer">
                            <span>GASプロジェクトの管理</span>
                            <span class="text-teal-500 text-2xl transform transition-transform duration-300">&#x25BC;</span>
                        </h3>
                        <div class="accordion-content px-5 pb-5 text-gray-600">
                            <ul class="list-disc list-inside space-y-2">
                                <li><strong>デプロイ:</strong> コードを修正した際は、必ず**新しいバージョンとして再デプロイ**してください。これにより変更がWebアプリに反映されます。</li>
                                <li><strong>認証情報:</strong> `LINE_CHANNEL_ACCESS_TOKEN` と `SPREADSHEET_ID` は機密情報です。外部に漏洩しないよう厳重に管理し、必要に応じて更新してください。</li>
                                <li><strong>実行ログ:</strong> 動作に問題がある場合は、GASエディタの「実行」メニューからログを確認してください。`Logger.log` で出力されたメッセージが問題解決の鍵となります。</li>
                            </ul>
                        </div>
                    </div>
                    <div class="bg-white rounded-lg shadow-md">
                        <h3 class="accordion-title p-5 w-full text-left font-semibold text-lg text-teal-800 flex justify-between items-center cursor-pointer">
                            <span>Googleスプレッドシートの管理</span>
                             <span class="text-teal-500 text-2xl transform transition-transform duration-300">&#x25BC;</span>
                        </h3>
                        <div class="accordion-content px-5 pb-5 text-gray-600">
                            <ul class="list-disc list-inside space-y-2">
                                <li><strong>シート名と列順:</strong> シート名 (`会員情報`, `受付履歴`) と各シートの列の順番は、GASのコードと一致している必要があります。変更する場合は、GASコードの修正も必要です。</li>
                                <li><strong>データ形式:</strong> 「所属」は文字列、「ポイント」は数値で入力してください。特に手動で編集する際はデータ形式を間違えないよう注意が必要です。</li>
                            </ul>
                        </div>
                    </div>
                    <div class="bg-white rounded-lg shadow-md">
                        <h3 class="accordion-title p-5 w-full text-left font-semibold text-lg text-teal-800 flex justify-between items-center cursor-pointer">
                            <span>LINE Developersコンソール</span>
                             <span class="text-teal-500 text-2xl transform transition-transform duration-300">&#x25BC;</span>
                        </h3>
                        <div class="accordion-content px-5 pb-5 text-gray-600">
                            <ul class="list-disc list-inside space-y-2">
                                <li><strong>Webhook URL:</strong> GASをデプロイした際に発行されるURLが正しく設定されているか、「検証」ボタンで確認してください。</li>
                                <li><strong>応答メッセージ設定:</strong> LINE Developersの「応答メッセージ」は**OFF**に設定してください。ONになっていると、ボットのカスタム応答が機能しなくなります。</li>
                            </ul>
                        </div>
                    </div>
                </div>
            </section>
            
             <!-- Ideas Section -->
            <section id="ideas" class="content-section">
                <h2 class="text-3xl font-bold mb-6 text-teal-900 border-b-4 border-teal-300 pb-2">5. 今後の拡張アイデア</h2>
                <p class="mb-8 text-lg text-gray-700">このボットはさらに進化させるポテンシャルを秘めています。将来的な機能拡張のアイデアを以下に示します。</p>
                <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                    <div class="bg-white p-6 rounded-xl shadow-md border-t-4 border-teal-400">
                        <h3 class="text-xl font-semibold mb-2 text-teal-800">管理者向けコマンド</h3>
                        <p class="text-gray-600">特定の管理者のみが「ポイント確認」「ユーザー検索」などのコマンドを実行できる機能。</p>
                    </div>
                    <div class="bg-white p-6 rounded-xl shadow-md border-t-4 border-teal-400">
                        <h3 class="text-xl font-semibold mb-2 text-teal-800">リッチメニューの活用</h3>
                        <p class="text-gray-600">「参加」ボタンをリッチメニューとして常時表示し、ユーザーの操作性を向上させる。</p>
                    </div>
                    <div class="bg-white p-6 rounded-xl shadow-md border-t-4 border-teal-400">
                        <h3 class="text-xl font-semibold mb-2 text-teal-800">ポイント交換機能</h3>
                        <p class="text-gray-600">貯まったポイントを景品や特典と交換できる仕組みを導入する。</p>
                    </div>
                    <div class="bg-white p-6 rounded-xl shadow-md border-t-4 border-teal-400">
                        <h3 class="text-xl font-semibold mb-2 text-teal-800">エラー通知機能</h3>
                        <p class="text-gray-600">GASでエラーが発生した場合、管理者に自動で通知する仕組みを構築する。</p>
                    </div>
                </div>
            </section>
        </main>
    </div>

<script>
document.addEventListener('DOMContentLoaded', () => {
    // Navigation Logic
    const navLinks = document.querySelectorAll('.nav-link');
    const sections = document.querySelectorAll('.content-section');

    function updateActiveNav(hash) {
        navLinks.forEach(link => {
            link.classList.toggle('active', link.getAttribute('href') === hash);
        });
        sections.forEach(section => {
            section.classList.toggle('active', `#${section.id}` === hash);
        });
    }

    navLinks.forEach(link => {
        link.addEventListener('click', e => {
            e.preventDefault();
            const targetHash = link.getAttribute('href');
            history.pushState(null, null, targetHash);
            updateActiveNav(targetHash);
        });
    });

    window.addEventListener('popstate', () => {
        updateActiveNav(window.location.hash || '#overview');
    });

    // Initial load
    updateActiveNav(window.location.hash || '#overview');

    // Accordion Logic
    document.querySelectorAll('.accordion-title').forEach(title => {
        title.addEventListener('click', () => {
            title.classList.toggle('open');
            const arrow = title.querySelector('span:last-child');
            if(arrow) {
                arrow.style.transform = title.classList.contains('open') ? 'rotate(180deg)' : 'rotate(0deg)';
            }
        });
    });

    // --- Simulation Logic ---
    const scenarioSelect = document.getElementById('scenario-select');
    const startSimBtn = document.getElementById('start-sim-btn');
    const chatLog = document.getElementById('chat-log');
    const userActions = document.getElementById('user-actions');
    const memberSheetBody = document.getElementById('member-sheet-body');
    const historySheetBody = document.getElementById('history-sheet-body');

    let simState = {};
    let mockMemberSheet = [];
    let mockHistorySheet = [];

    const scenarios = {
        newUser: {
            description: "新規ユーザーの登録",
            initialMemberSheet: [],
            initialHistorySheet: [],
            userId: 'U_newUser_12345',
            userName: '新しいユーザー'
        },
        existingUserOther: {
            description: "既存ユーザー (所属: 静岡市以外)",
            initialMemberSheet: [
                { id: 'U_existing_67890', name: '既存 太郎', affiliation: '東京都', points: 5 }
            ],
            initialHistorySheet: [],
            userId: 'U_existing_67890',
            userName: '既存 太郎'
        },
        existingUserShizuoka: {
            description: "既存ユーザー (所属: 静岡市)",
            initialMemberSheet: [
                 { id: 'U_shizuoka_54321', name: '静岡 花子', affiliation: '静岡市', points: 10 }
            ],
            initialHistorySheet: [],
            userId: 'U_shizuoka_54321',
            userName: '静岡 花子'
        },
        limitCheck: {
            description: "ポイント付与制限チェック",
            initialMemberSheet: [
                { id: 'U_limit_11223', name: '制限 チェック', affiliation: '神奈川県', points: 12 }
            ],
            initialHistorySheet: [
                { timestamp: new Date(), id: 'U_limit_11223', name: '制限 チェック', event: 'モーニングセミナー', points: 11},
                { timestamp: new Date(), id: 'U_limit_11223', name: '制限 チェック', event: 'モーニングセミナー', points: 12},
            ],
            userId: 'U_limit_11223',
            userName: '制限 チェック'
        },
        goalCheck: {
            description: "ポイント目標達成",
            initialMemberSheet: [
                { id: 'U_goal_99887', name: '目標 達成', affiliation: '静岡市', points: 19 }
            ],
            initialHistorySheet: [],
            userId: 'U_goal_99887',
            userName: '目標 達成'
        }
    };

    function renderMemberSheet() {
        memberSheetBody.innerHTML = '';
        mockMemberSheet.forEach(row => {
            const tr = document.createElement('tr');
            tr.id = `member-${row.id}`;
            tr.innerHTML = `<td class="border p-2">${row.id}</td><td class="border p-2">${row.name}</td><td class="border p-2">${row.affiliation}</td><td class="border p-2">${row.points}</td>`;
            memberSheetBody.appendChild(tr);
        });
    }
    
    function renderHistorySheet() {
        historySheetBody.innerHTML = '';
        mockHistorySheet.forEach(row => {
            const tr = document.createElement('tr');
            tr.innerHTML = `<td class="border p-2">${row.timestamp.toLocaleTimeString('ja-JP')}</td><td class="border p-2">${row.id}</td><td class="border p-2">${row.name}</td><td class="border p-2">${row.event}</td><td class="border p-2">${row.points}</td>`;
            historySheetBody.appendChild(tr);
        });
    }

    function addChatMessage(sender, text, options = []) {
        const bubble = document.createElement('div');
        if (sender === 'user') {
            bubble.className = 'chat-bubble flex justify-end';
            bubble.innerHTML = `<div class="bg-teal-500 text-white p-3 rounded-lg max-w-xs">${text}</div>`;
        } else { // bot
            bubble.className = 'chat-bubble flex justify-start';
            bubble.innerHTML = `<div class="bg-gray-200 text-gray-800 p-3 rounded-lg max-w-xs">${text}</div>`;
        }
        chatLog.appendChild(bubble);
        chatLog.scrollTop = chatLog.scrollHeight;
        
        userActions.innerHTML = '';
        if (options.length > 0) {
            setTimeout(() => {
                options.forEach(opt => {
                    const button = document.createElement('button');
                    button.textContent = opt.label;
                    button.className = 'sim-button bg-white text-teal-600 font-semibold py-2 px-4 border border-teal-500 rounded-lg shadow mr-2';
                    button.onclick = opt.action;
                    userActions.appendChild(button);
                });
            }, 500);
        }
    }
    
    function highlightCell(sheet, rowId, colIndex) {
        let row;
        if (sheet === 'member') {
            row = document.getElementById(`member-${rowId}`);
        }
        if (row) {
            const cell = row.cells[colIndex];
            if (cell) {
                cell.classList.add('table-cell-highlight');
                setTimeout(() => cell.classList.remove('table-cell-highlight'), 1500);
            }
        }
    }

    function resetSimulation() {
        const selectedScenario = scenarios[scenarioSelect.value];
        simState = { ...selectedScenario, step: 'start' };
        mockMemberSheet = JSON.parse(JSON.stringify(selectedScenario.initialMemberSheet));
        mockHistorySheet = JSON.parse(JSON.stringify(selectedScenario.initialHistorySheet));
        chatLog.innerHTML = '';
        userActions.innerHTML = '';
        renderMemberSheet();
        renderHistorySheet();
    }

    startSimBtn.addEventListener('click', () => {
        resetSimulation();
        addChatMessage('bot', `シナリオ「${simState.description}」を開始します。「参加」ボタンを押してください。`);
        addChatMessage(null, null, [{ label: '参加', action: step1_sendSanka }]);
    });
    
    function step1_sendSanka() {
        addChatMessage('user', '参加');
        simState.step = 'waiting_for_confirmation';
        setTimeout(() => {
            addChatMessage('bot', '参加登録をしますか？', [
                { label: 'はい', action: step2_sendYes },
                { label: 'いいえ', action: step_cancel }
            ]);
        }, 800);
    }
    
    function step_cancel() {
        addChatMessage('user', 'いいえ');
         setTimeout(() => {
            addChatMessage('bot', '参加登録をキャンセルしました。');
            addChatMessage(null, null, [{ label: 'シミュレーションをリセット', action: resetSimulation }]);
        }, 800);
    }
    
    function step2_sendYes() {
        addChatMessage('user', 'はい');
        
        setTimeout(() => {
            let user = mockMemberSheet.find(u => u.id === simState.userId);
            
            if (user && user.affiliation === '静岡市') {
                simState.step = 'waiting_for_seminar_type';
                addChatMessage('bot', '本日、参加するセミナーは何ですか？', [
                    { label: 'モーニングセミナー', action: () => processShizuokaUser('モーニングセミナー') },
                    { label: 'それ以外', action: step3_askCustomEvent }
                ]);
            } else {
                // Not shizuoka or new user
                processParticipation('モーニングセミナー');
            }
        }, 1000);
    }

    function step3_askCustomEvent() {
        addChatMessage('user', 'それ以外');
        simState.step = 'waiting_for_custom_event';
         setTimeout(() => {
            addChatMessage('bot', '参加する行事を入力してください (例: 特別勉強会)');
             // This is simplified, we'll just provide a button for the example
            addChatMessage(null, null, [{ label: '特別勉強会', action: () => processShizuokaUser('特別勉強会') }]);
        }, 800);
    }

    function processShizuokaUser(eventName) {
         addChatMessage('user', eventName);
         processParticipation(eventName);
    }

    function processParticipation(eventName) {
        const dailyCount = mockHistorySheet.filter(r => r.id === simState.userId).length;
        if (dailyCount >= 2) {
             setTimeout(() => {
                addChatMessage('bot', 'ポイントは1日に最大2ポイントまでしか付与できません');
                addChatMessage(null, null, [{ label: 'シミュレーションをリセット', action: resetSimulation }]);
            }, 800);
            return;
        }

        let user = mockMemberSheet.find(u => u.id === simState.userId);
        if (!user) { // New user
            user = { id: simState.userId, name: simState.userName, affiliation: '', points: 0 };
            mockMemberSheet.push(user);
            renderMemberSheet();
            highlightCell('member', user.id, 0);
        }

        user.points += 1;
        mockHistorySheet.push({
            timestamp: new Date(),
            id: user.id,
            name: user.name,
            event: eventName,
            points: user.points
        });
        
        renderMemberSheet();
        highlightCell('member', user.id, 3);
        renderHistorySheet();
        
        setTimeout(() => {
            let message = `${user.name}さん、${eventName}の参加を登録しました。ポイントが${user.points}ポイント貯まりました！`;
            addChatMessage('bot', message);
            
            if (user.points >= 20) {
                 setTimeout(() => {
                     addChatMessage('bot', `🎉✨ おめでとうございます！20ポイント達成です！ ✨🎉\n\nこの達成を記念して、スクリーンショットを撮ってタイムラインに投稿してください！`);
                     user.points = 0;
                     renderMemberSheet();
                     highlightCell('member', user.id, 3);
                 }, 1000);
            }
            
            addChatMessage(null, null, [{ label: 'シミュレーションをリセット', action: resetSimulation }]);
        }, 1200);
    }

    // Initialize first view
    resetSimulation();
    document.getElementById('start-sim-btn').click();


});
</script>

</body>
</html>
