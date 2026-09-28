[神経衰弱中１社会index.html](https://github.com/user-attachments/files/32749211/index.html)
<!DOCTYPE html>
<html lang="ja">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>中1社会 ペアマッチ！神経衰弱</title>
    <!-- Tailwind CSS -->
    <script src="https://cdn.tailwindcss.com"></script>
    <!-- Font Awesome Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <!-- Canvas Confetti -->
    <script src="https://cdn.jsdelivr.net/npm/canvas-confetti@1.6.0/dist/confetti.browser.min.js"></script>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=M+PLUS+Rounded+1c:wght@400;600;800;900&display=swap');

        body {
            font-family: 'M PLUS Rounded 1c', sans-serif;
            background: linear-gradient(135deg, #f0fdf4 0%, #e0f2fe 50%, #fef3c7 100%);
            user-select: none;
            -webkit-user-select: none;
            touch-action: manipulation;
        }

        .card-perspective {
            perspective: 1000px;
        }

        .card-inner {
            position: relative;
            width: 100%;
            height: 100%;
            transition: transform 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            transform-style: preserve-3d;
        }

        .card-inner.is-flipped {
            transform: rotateY(180deg);
        }

        .card-face {
            position: absolute;
            width: 100%;
            height: 100%;
            backface-visibility: hidden;
            -webkit-backface-visibility: hidden;
            border-radius: 0.85rem;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            box-shadow: 0 4px 12px rgba(0, 0, 0, 0.08);
            padding: 0.25rem;
        }

        /* Card Front (Pattern side) */
        .card-front {
            background: linear-gradient(135deg, #3b82f6 0%, #2563eb 100%);
            border: 3px solid #93c5fd;
            color: white;
        }

        /* Card Back (Content side) */
        .card-back {
            background: #ffffff;
            border: 3px solid #cbd5e1;
            transform: rotateY(180deg);
            color: #1e293b;
        }

        /* Matched State */
        .matched .card-back {
            border-color: #10b981;
            background-color: #ecfdf5;
            animation: matchPulse 0.4s ease-out;
        }

        @keyframes matchPulse {
            0% { transform: rotateY(180deg) scale(1); }
            50% { transform: rotateY(180deg) scale(1.08); }
            100% { transform: rotateY(180deg) scale(1); }
        }

        ::-webkit-scrollbar {
            width: 6px;
        }
        ::-webkit-scrollbar-thumb {
            background: #cbd5e1;
            border-radius: 9999px;
        }
    </style>
</head>
<body class="min-h-screen flex flex-col justify-between overflow-x-hidden text-slate-800">

    <header class="w-full bg-white/90 backdrop-blur-md border-b border-slate-200/80 sticky top-0 z-30 shadow-sm px-4 py-3">
        <div class="max-w-md mx-auto flex justify-between items-center">
            <div class="flex items-center space-x-2">
                <span class="text-2xl animate-bounce">🧩</span>
                <h1 class="text-lg sm:text-xl font-extrabold bg-gradient-to-r from-blue-600 via-indigo-600 to-purple-600 bg-clip-text text-transparent">
                    中1社会 ペアマッチ！
                </h1>
            </div>
            <button id="soundToggleBtn" class="w-10 h-10 rounded-full bg-slate-100 active:scale-95 text-slate-600 flex items-center justify-center transition shadow-inner">
                <i id="soundIcon" class="fas fa-volume-up text-lg text-indigo-600"></i>
            </button>
        </div>
    </header>

    <main class="w-full max-w-md mx-auto px-4 py-4 flex-1 flex flex-col justify-center items-center">

        <!-- Mode Selection Screen -->
        <div id="selectionScreen" class="w-full bg-white/95 rounded-3xl shadow-xl p-6 border border-slate-100 text-center space-y-5 my-auto">
            <div class="space-y-1">
                <h2 class="text-2xl font-black text-slate-800">ジャンルを選ぼう！</h2>
                <p class="text-slate-500 text-xs sm:text-sm font-semibold">全48テーマからランダム出題！</p>
            </div>

            <div class="grid grid-cols-1 gap-3.5 pt-2">
                <!-- 地理 Mode Button -->
                <button onclick="startGame('geography')" class="group relative overflow-hidden p-4 rounded-2xl border-2 border-emerald-300 bg-gradient-to-r from-emerald-50 to-teal-50 active:scale-98 transition-all flex items-center space-x-4 shadow-md text-left">
                    <div class="w-12 h-12 rounded-xl bg-emerald-500 text-white flex items-center justify-center text-2xl shadow-lg shrink-0 group-hover:scale-110 transition-transform">
                        🌍
                    </div>
                    <div>
                        <div class="font-extrabold text-base text-emerald-900 flex items-center space-x-1">
                            <span>地理モード</span>
                            <span class="bg-emerald-200 text-emerald-800 text-[10px] px-2 py-0.5 rounded-full font-bold">全24テーマ</span>
                        </div>
                        <div class="text-xs text-emerald-700 font-medium mt-0.5">世界の気候・工業地帯・地形・農業の特徴など</div>
                    </div>
                </button>

                <!-- 歴史 Mode Button -->
                <button onclick="startGame('history')" class="group relative overflow-hidden p-4 rounded-2xl border-2 border-amber-300 bg-gradient-to-r from-amber-50 to-orange-50 active:scale-98 transition-all flex items-center space-x-4 shadow-md text-left">
                    <div class="w-12 h-12 rounded-xl bg-amber-500 text-white flex items-center justify-center text-2xl shadow-lg shrink-0 group-hover:scale-110 transition-transform">
                        📜
                    </div>
                    <div>
                        <div class="font-extrabold text-base text-amber-900 flex items-center space-x-1">
                            <span>歴史モード</span>
                            <span class="bg-amber-200 text-amber-800 text-[10px] px-2 py-0.5 rounded-full font-bold">全24テーマ</span>
                        </div>
                        <div class="text-xs text-amber-700 font-medium mt-0.5">旧石器時代から安土桃山・江戸幕府開設まで</div>
                    </div>
                </button>

                <!-- ミックス Mode Button -->
                <button onclick="startGame('mix')" class="group relative overflow-hidden p-4 rounded-2xl border-2 border-indigo-300 bg-gradient-to-r from-indigo-50 to-purple-50 active:scale-98 transition-all flex items-center space-x-4 shadow-md text-left">
                    <div class="w-12 h-12 rounded-xl bg-indigo-500 text-white flex items-center justify-center text-2xl shadow-lg shrink-0 group-hover:scale-110 transition-transform">
                        ⭐
                    </div>
                    <div>
                        <div class="font-extrabold text-base text-indigo-900 flex items-center space-x-1">
                            <span>ミックスモード</span>
                            <span class="bg-indigo-200 text-indigo-800 text-[10px] px-2 py-0.5 rounded-full font-bold">全48テーマ</span>
                        </div>
                        <div class="text-xs text-indigo-700 font-medium mt-0.5">地理と歴史の全問題からランダムで挑戦！</div>
                    </div>
                </button>
            </div>

            <div class="bg-slate-50 p-3 rounded-xl border border-slate-200/80 text-xs text-slate-500 font-semibold flex items-center justify-center space-x-2">
                <i class="fas fa-lightbulb text-amber-500"></i>
                <span>揃えると詳しい豆知識ポップアップが出るよ！</span>
            </div>
        </div>

        <!-- Gameplay Screen -->
        <div id="gameScreen" class="w-full hidden flex flex-col items-center">
            
            <!-- Dashboard Info -->
            <div class="w-full bg-white rounded-2xl shadow-md p-3.5 mb-3 flex justify-between items-center border border-slate-100">
                <button onclick="showModeSelection()" class="text-xs bg-slate-100 hover:bg-slate-200 text-slate-600 font-bold px-3 py-2 rounded-xl transition flex items-center space-x-1">
                    <i class="fas fa-arrow-left"></i>
                    <span>戻る</span>
                </button>

                <div class="flex space-x-4">
                    <div class="text-center">
                        <span class="text-[10px] text-slate-400 font-bold block uppercase tracking-wider">タイム</span>
                        <div id="timer" class="font-black text-lg text-slate-700 font-mono">00:00</div>
                    </div>
                    <div class="text-center">
                        <span class="text-[10px] text-slate-400 font-bold block uppercase tracking-wider">めくった回数</span>
                        <div id="moveCount" class="font-black text-lg text-indigo-600">0</div>
                    </div>
                    <div class="text-center">
                        <span class="text-[10px] text-slate-400 font-bold block uppercase tracking-wider">ペア</span>
                        <div id="matchCount" class="font-black text-lg text-emerald-600">0 / 6</div>
                    </div>
                </div>
            </div>

            <!-- Memory Card Grid -->
            <div id="cardGrid" class="w-full grid grid-cols-3 gap-2.5 sm:gap-3 mb-2">
                <!-- Cards injected via JavaScript -->
            </div>
        </div>

    </main>

    <!-- Educational Explanation Modal -->
    <div id="explanationModal" class="fixed inset-0 bg-slate-900/60 backdrop-blur-sm z-50 flex items-center justify-center p-4 hidden opacity-0 transition-opacity duration-300">
        <div id="modalCard" class="bg-white rounded-3xl max-w-xs w-full p-5 shadow-2xl border border-slate-100 text-center transform scale-95 transition-transform duration-300 space-y-3">
            <div class="flex justify-between items-center">
                <span class="px-2.5 py-0.5 bg-emerald-100 text-emerald-800 text-[11px] font-extrabold rounded-full flex items-center space-x-1">
                    <i class="fas fa-check-circle text-emerald-600"></i>
                    <span>正解ペア！</span>
                </span>
                <span id="modalCategory" class="text-xs text-slate-400 font-bold">地理</span>
            </div>
            
            <div class="text-3xl" id="modalEmoji">💡</div>
            
            <h3 id="modalPairTitle" class="text-lg font-black text-slate-800">
                ペアのタイトル
            </h3>
            
            <div class="bg-slate-50 p-3.5 rounded-2xl border border-slate-200 text-left">
                <p id="modalExplanation" class="text-xs text-slate-600 font-medium leading-relaxed">
                    解説テキスト
                </p>
            </div>

            <button onclick="closeExplanationModal()" class="w-full py-3 bg-gradient-to-r from-emerald-500 to-teal-500 hover:from-emerald-600 hover:to-teal-600 active:scale-98 text-white font-extrabold rounded-xl shadow-lg shadow-emerald-500/25 transition">
                つぎへ進む
            </button>
        </div>
    </div>

    <!-- Final Game Over Modal -->
    <div id="resultModal" class="fixed inset-0 bg-slate-900/70 backdrop-blur-md z-50 flex items-center justify-center p-4 hidden">
        <div class="bg-white rounded-3xl max-w-xs w-full p-6 text-center shadow-2xl border border-slate-100 space-y-4">
            <div class="text-5xl animate-bounce">🏆</div>
            <div>
                <h2 class="text-2xl font-black text-slate-800">ステージクリア！</h2>
                <p class="text-slate-500 text-xs font-semibold">社会の重要用語をマスターしたよ！</p>
            </div>

            <!-- Star Rating -->
            <div id="starRating" class="text-3xl text-amber-400 flex justify-center space-x-2">
                <i class="fas fa-star"></i>
                <i class="fas fa-star"></i>
                <i class="fas fa-star"></i>
            </div>

            <div class="bg-slate-50 rounded-2xl p-3.5 border border-slate-200 text-xs grid grid-cols-2 gap-2 text-slate-600 font-bold">
                <div class="bg-white p-2 rounded-xl shadow-sm">クリア時間<br><span id="finalTime" class="text-slate-800 text-sm font-black">--:--</span></div>
                <div class="bg-white p-2 rounded-xl shadow-sm">めくった回数<br><span id="finalMoves" class="text-slate-800 text-sm font-black">0</span>回</div>
            </div>

            <div class="flex space-x-2 pt-1">
                <button onclick="restartGame()" class="flex-1 py-3 bg-slate-100 hover:bg-slate-200 active:scale-98 text-slate-700 font-extrabold rounded-xl transition">
                    もう一度
                </button>
                <button onclick="showModeSelection()" class="flex-1 py-3 bg-gradient-to-r from-indigo-600 to-purple-600 hover:from-indigo-700 hover:to-purple-700 active:scale-98 text-white font-extrabold rounded-xl shadow-lg shadow-indigo-600/30 transition">
                    ジャンル選択
                </button>
            </div>
        </div>
    </div>

    <script>
        const gameData = {
            geography: [
                {
                    id: 'g1',
                    itemA: { icon: '🇮🇹', title: 'イタリア', detail: '地中海性気候' },
                    itemB: { icon: '🍕', title: 'オリーブ・ブドウ', detail: '夏に乾燥する気候' },
                    category: '地理',
                    title: 'イタリア ↔ 特徴・作物',
                    explanation: 'イタリアは「地中海性気候」に属し、夏は雨が少なく乾燥します。オリーブやブドウの栽培（地中海式農業）や観光業が非常に有名です。'
                },
                {
                    id: 'g2',
                    itemA: { icon: '🌲', title: '冷帯（亜寒帯）', detail: '短い夏と厳しい冬' },
                    itemB: { icon: '❄️', title: 'タイガ（針葉樹林）', detail: 'シベリアなどに分布' },
                    category: '地理',
                    title: '冷帯 ↔ タイガ（針葉樹林）',
                    explanation: '冬の寒さが厳しい「冷帯」地域には、「タイガ」と呼ばれる広大な針葉樹林帯（松やスギの仲間）が広がっています。'
                },
                {
                    id: 'g3',
                    itemA: { icon: '🌾', title: '北海道', detail: '日本の北端' },
                    itemB: { icon: '🥛', title: '稲作・酪農', detail: '大規模な農業' },
                    category: '地理',
                    title: '北海道 ↔ 稲作・酪農',
                    explanation: '北海道では石狩平野での稲作（米作り）や、根釧台地での広大な土地を生かした「酪農（乳牛の飼育）」が非常に盛んです。'
                },
                {
                    id: 'g4',
                    itemA: { icon: '🇪🇬', title: 'エジプト', detail: 'アフリカ大陸' },
                    itemB: { icon: '🏺', title: 'ピラミッド・ナイル川', detail: '古代文明の地' },
                    category: '地理',
                    title: 'エジプト ↔ ピラミッド・ナイル川',
                    explanation: '「ナイル川の恵み」によって発展したエジプト。巨大なピラミッドやスフィンクスなどの世界遺産で有名です。'
                },
                {
                    id: 'g5',
                    itemA: { icon: '🇧🇷', title: 'ブラジル', detail: '南アメリカ大陸' },
                    itemB: { icon: '🌳', title: 'アマゾン川・セルバ', detail: '熱帯雨林' },
                    category: '地理',
                    title: 'ブラジル ↔ アマゾン川・熱帯雨林',
                    explanation: 'ブラジルには流域面積世界一の「アマゾン川」が流れ、「セルバ」と呼ばれる巨大な熱帯雨林が広がっています。'
                },
                {
                    id: 'g6',
                    itemA: { icon: '🌧️', title: '熱帯雨林気候', detail: '赤道付近' },
                    itemB: { icon: '⚡', title: 'スコール', detail: '午後の激しい雨' },
                    category: '地理',
                    title: '熱帯 ↔ スコール',
                    explanation: '一年中気温が高い熱帯地域では、ほぼ毎日午後になると「スコール」と呼ばれる強い雷雨が降ります。'
                },
                {
                    id: 'g7',
                    itemA: { icon: '🇺🇸', title: 'アメリカ合衆国', detail: '北アメリカ' },
                    itemB: { icon: '🚜', title: '適地適作・大平原', detail: '大規模商業農業' },
                    category: '地理',
                    title: 'アメリカ ↔ 適地適作',
                    explanation: 'アメリカでは、地域の気候や土壌に最も適した作物を大規模に栽培する「適地適作」が行われています。'
                },
                {
                    id: 'g8',
                    itemA: { icon: '🕋', title: 'イスラム教', detail: '三大宗教' },
                    itemB: { icon: '📖', title: 'コーラン・モスク', detail: '断食（ラマダン）' },
                    category: '地理',
                    title: 'イスラム教 ↔ コーラン・モスク',
                    explanation: '西アジアを中心に信仰されるイスラム教。聖典は『コーラン』で、礼拝を行う施設を「モスク」と呼びます。'
                },
                {
                    id: 'g9',
                    itemA: { icon: '🇪🇺', title: 'EU（欧州連合）', detail: 'ヨーロッパの統合' },
                    itemB: { icon: '💶', title: 'ユーロ（共通通貨）', detail: '国境移動の自由' },
                    category: '地理',
                    title: 'EU ↔ ユーロ',
                    explanation: 'ヨーロッパ諸国が経済や政治で協力するために結成したEU。加盟国間では共通通貨「ユーロ」が使われています。'
                },
                {
                    id: 'g10',
                    itemA: { icon: '🍅', title: '高知県・宮崎県', detail: '太平洋側の暖かい気候' },
                    itemB: { icon: '☀️', title: '促成栽培', detail: 'ビニールハウスで早出荷' },
                    category: '地理',
                    title: '高知・宮崎 ↔ 促成栽培',
                    explanation: '温暖な気候を生かし、野菜（ピーマンやナスなど）を普通より早い時期に出荷する「促成栽培」が行われています。'
                },
                {
                    id: 'g11',
                    itemA: { icon: '🌋', title: '九州南部（鹿児島など）', detail: '火山の噴火物' },
                    itemB: { icon: '🍠', title: 'シラス台地', detail: 'サツマイモ・畜産' },
                    category: '地理',
                    title: '九州南部 ↔ シラス台地',
                    explanation: '火山灰などが積み重なってできた「シラス台地」は水もちが悪いため、稲作ではなくサツマイモ栽培や畜産（豚・肉牛）が盛んです。'
                },
                {
                    id: 'g12',
                    itemA: { icon: '❄️', title: '日本海側の気候', detail: '冬の季節風' },
                    itemB: { icon: '☃️', title: '冬に大雪が降る', detail: '北西の季節風' },
                    category: '地理',
                    title: '日本海側の気候 ↔ 冬の大雪',
                    explanation: '冬になると、ユーラシア大陸から湿った北西の季節風が日本海を渡って吹きつけるため、山沿いを中心に世界有数の大雪が降ります。'
                },
                {
                    id: 'g13',
                    itemA: { icon: '🇨🇳', title: '中国', detail: 'アジアの大国' },
                    itemB: { icon: '🏭', title: '世界の工場・世界一の人口', detail: '経済成長が著しい' },
                    category: '地理',
                    title: '中国 ↔ 世界の工場',
                    explanation: '豊富な労働力と広大な土地を生かし、世界中の工業製品を生産しているため「世界の工場」と呼ばれています。'
                },
                {
                    id: 'g14',
                    itemA: { icon: '🇦🇺', title: 'オーストラリア', detail: 'オセアニア' },
                    itemB: { icon: '🪨', title: '石炭・鉄鉱石の輸出', detail: '豊かな鉱産資源' },
                    category: '地理',
                    title: 'オーストラリア ↔ 鉱産資源',
                    explanation: '東部で「石炭」、北西部で「鉄鉱石」などの鉱産資源が豊富に採掘され、日本へも多く輸出されています。'
                },
                {
                    id: 'g15',
                    itemA: { icon: '🌍', title: 'モノカルチャー経済', detail: '発展途上国' },
                    itemB: { icon: '🍫', title: '特定の産品に依存', detail: 'カカオや銅など' },
                    category: '地理',
                    title: 'モノカルチャー経済 ↔ 特定作物への依存',
                    explanation: 'アフリカなどの発展途上国で、特定の農産物や鉱産資源（カカオ、銅など）の輸出に頼り切っている経済構造のことです。'
                },
                {
                    id: 'g16',
                    itemA: { icon: '⛰️', title: 'アルプス・ヒマラヤ山脈', detail: '高く険しい山脈' },
                    itemB: { icon: '🌋', title: '新期造山帯', detail: '地震や火山活動が多い' },
                    category: '地理',
                    title: 'アルプス・ヒマラヤ ↔ 新期造山帯',
                    explanation: '比較的新しく形成された「新期造山帯」は高く険しい山脈が多く、地震や火山活動が活発です。'
                },
                {
                    id: 'g17',
                    itemA: { icon: '🚗', title: '中京工業地帯', detail: '愛知・三重・岐阜' },
                    itemB: { icon: '🏆', title: '自動車工業・出荷額日本一', detail: '豊田市など' },
                    category: '地理',
                    title: '中京工業地帯 ↔ 自動車工業',
                    explanation: '豊田市を中心とした自動車工業が非常に盛んで、日本の工業地帯の中で製造品出荷額が第1位です。'
                },
                {
                    id: 'g18',
                    itemA: { icon: '🏢', title: '阪神工業地帯', detail: '大阪・兵庫' },
                    itemB: { icon: '🔧', title: '中小企業の高い技術', detail: '金属・機械工業' },
                    category: '地理',
                    title: '阪神工業地帯 ↔ 中小企業',
                    explanation: '東大阪市などに代表されるように、高い技術力を持った中小企業の割合が高いことが特徴です。'
                },
                {
                    id: 'g19',
                    itemA: { icon: '🥬', title: '茨城県・千葉県', detail: '首都圏に近い' },
                    itemB: { icon: '🚚', title: '近郊農業', detail: '大都市向け野菜栽培' },
                    category: '地理',
                    title: '茨城・千葉 ↔ 近郊農業',
                    explanation: '大都市の近くで新鮮な野菜（キャベツやハクサイなど）を栽培し、すぐに出荷する「近郊農業」が盛んです。'
                },
                {
                    id: 'g20',
                    itemA: { icon: '🍇', title: '扇状地（せんじょうち）', detail: '川が山から平野へ出る場所' },
                    itemB: { icon: '🍑', title: '水はけが良く果樹園に利用', detail: 'ブドウやモモの栽培' },
                    category: '地理',
                    title: '扇状地 ↔ 果樹園',
                    explanation: '砂利が多く水はけが良いため、お米作りよりもブドウやモモなどの果樹園として利用されます（山梨県の甲府盆地など）。'
                },
                {
                    id: 'g21',
                    itemA: { icon: '🌾', title: '三角州（さんかくす）', detail: '川の河口付近' },
                    itemB: { icon: '🍚', title: '水が得やすく水田に利用', detail: '低く平らな土地' },
                    category: '地理',
                    title: '三角州 ↔ 水田利用',
                    explanation: '川が海や湖に流れ込む河口付近にできる平らな土地で、水が得やすいため主に「水田（米作り）」に利用されます。'
                },
                {
                    id: 'g22',
                    itemA: { icon: '☀️', title: 'サンベルト', detail: 'アメリカ合衆国' },
                    itemB: { icon: '💻', title: '北緯37度以南・先端技術産業', detail: 'シリコンバレーなど' },
                    category: '地理',
                    title: 'サンベルト ↔ 先端技術産業',
                    explanation: 'アメリカの北緯37度より南の地域。温暖な気候を生かし、電子機器や宇宙産業などのハイテク産業（先端技術産業）が発展しました。'
                },
                {
                    id: 'g23',
                    itemA: { icon: '🏜️', title: 'サウジアラビア', detail: '西アジア' },
                    itemB: { icon: '🛢️', title: '乾燥帯（砂漠）と石油産出', detail: 'ペルシャ湾沿岸' },
                    category: '地理',
                    title: 'サウジアラビア ↔ 砂漠気候・石油',
                    explanation: '国土の大部分が砂漠（乾燥帯）ですが、ペルシャ湾沿岸を中心に世界有数の石油（原油）を産出しています。'
                },
                {
                    id: 'g24',
                    itemA: { icon: '🏙️', title: '過密と過疎', detail: '日本の人口問題' },
                    itemB: { icon: '🏚️', title: '都市への集中と地方の減少', detail: '限界集落・交通難' },
                    category: '地理',
                    title: '過密と過疎 ↔ 人口移動',
                    explanation: '東京などの大都市に人口が集中して問題となる「過密」と、地方で人口が減り生活維持が難しくなる「過疎」が社会問題となっています。'
                }
            ],
            history: [
                {
                    id: 'h1',
                    itemA: { icon: '👑', title: '聖徳太子', detail: '推古天皇の摂政' },
                    itemB: { icon: '📜', title: '十七条の憲法・冠位十二階', detail: '天皇中心の国づくり' },
                    category: '歴史',
                    title: '聖徳太子 ↔ 憲法・冠位十二階',
                    explanation: '聖徳太子（厩戸王）は、家柄にとらわれず才能ある人を登用する「冠位十二階」や、役人の心得を定めた「十七条の憲法」を制定しました。'
                },
                {
                    id: 'h2',
                    itemA: { icon: '🪨', title: '縄文時代', detail: '約1万数千年前〜' },
                    itemB: { icon: '🏺', title: '縄文土器・竪穴住居', detail: '貝塚・狩り採集' },
                    category: '歴史',
                    title: '縄文時代 ↔ 縄文土器・竪穴住居',
                    explanation: '表面に縄目の模様がある縄文土器を使い、狩りや採集をして「竪穴住居」に住みました。ゴミ捨て場である「貝塚」も有名です。'
                },
                {
                    id: 'h3',
                    itemA: { icon: '👸', title: '卑弥呼', detail: '3世紀・邪馬台国' },
                    itemB: { icon: '💎', title: '親魏倭王・金印', detail: '魏（中国）への使者' },
                    category: '歴史',
                    title: '卑弥呼 ↔ 邪馬台国・親魏倭王',
                    explanation: '邪馬台国の女王「卑弥呼」は中国の魏に使者を送り、「親魏倭王」の称号や金印・銅鏡を授かったと『魏志倭人伝』に書かれています。'
                },
                {
                    id: 'h4',
                    itemA: { icon: '⚔️', title: '坂上田村麻呂', detail: '平安時代初期' },
                    itemB: { icon: '🐎', title: '征夷大将軍', detail: '蝦夷（東北）の平定' },
                    category: '歴史',
                    title: '坂上田村麻呂 ↔ 征夷大将軍',
                    explanation: '桓武天皇によって初代「征夷大将軍」に任命された坂上田村麻呂は、東北地方（蝦夷）へ向かい平定しました。'
                },
                {
                    id: 'h5',
                    itemA: { icon: '🏯', title: '中大兄皇子・中臣鎌足', detail: '645年' },
                    itemB: { icon: '🔥', title: '大化の改新', detail: '公地公民・蘇我氏を倒す' },
                    category: '歴史',
                    title: '中大兄皇子たち ↔ 大化の改新',
                    explanation: '645年、蘇我氏を倒して始まった政治改革。土地や人民を国のものとする「公地公民」を定め、天皇中心の政治を目指しました。'
                },
                {
                    id: 'h6',
                    itemA: { icon: '🌾', title: '弥生時代', detail: '紀元前10世紀頃〜' },
                    itemB: { icon: '🏠', title: '稲作・高床倉庫', detail: '金属器（青銅器・鉄器）' },
                    category: '歴史',
                    title: '弥生時代 ↔ 稲作・高床倉庫',
                    explanation: '大陸から米作り（稲作）と金属器が伝わりました。収穫したお米は、湿気やねずみを防ぐ「高床倉庫」に蓄えられました。'
                },
                {
                    id: 'h7',
                    itemA: { icon: '⛩️', title: '平清盛', detail: '武士初の太政大臣' },
                    itemB: { icon: '🚢', title: '日宋貿易・厳島神社', detail: '大輪田泊の修築' },
                    category: '歴史',
                    title: '平清盛 ↔ 日宋貿易',
                    explanation: '武士として初めて太政大臣となった平清盛。兵庫の港（大輪田泊）を整備して、中国（宋）との「日宋貿易」を進めました。'
                },
                {
                    id: 'h8',
                    itemA: { icon: '⚔️', title: '源頼朝', detail: '鎌倉幕府を開く' },
                    itemB: { icon: '📜', title: '御恩と奉公・守護地頭', detail: '武家政権の始まり' },
                    category: '歴史',
                    title: '源頼朝 ↔ 鎌倉幕府',
                    explanation: '源頼朝は全国に「守護」と「地頭」を配置し、将軍と御家人が「御恩と奉公」で結ばれる鎌倉幕府を開きました。'
                },
                {
                    id: 'h9',
                    itemA: { icon: '🌸', title: '紫式部・清少納言', detail: '平安時代の女性文学' },
                    itemB: { icon: '✍️', title: '『源氏物語』『枕草子』', detail: 'かな文字と国風文化' },
                    category: '歴史',
                    title: '平安時代の文化 ↔ かな文字文学',
                    explanation: '唐風の文化から日本の風土に合った「国風文化」へ発展。かな文字が使われ、紫式部が『源氏物語』、清少納言が『枕草子』を書きました。'
                },
                {
                    id: 'h10',
                    itemA: { icon: '🏯', title: '足利義満', detail: '室町幕府3代将軍' },
                    itemB: { icon: '✨', title: '金閣・勘合貿易（日明貿易）', detail: '北山文化' },
                    category: '歴史',
                    title: '足利義満 ↔ 金閣・勘合貿易',
                    explanation: '南北朝の統一を果たした足利義満。京都に「金閣」を建て、明（中国）と「勘合」という割り符を使った日明貿易を行いました。'
                },
                {
                    id: 'h11',
                    itemA: { icon: '🏯', title: '織田信長', detail: '安土桃山時代' },
                    itemB: { icon: '🔫', title: '長篠の戦い・楽市楽座', detail: '安土城・天下布武' },
                    category: '歴史',
                    title: '織田信長 ↔ 長篠の戦い・楽市楽座',
                    explanation: '鉄砲を大量に使って武田軍を破った「長篠の戦い」や、関所を廃止して商売を自由にした「楽市楽座」で全国統一を進めました。'
                },
                {
                    id: 'h12',
                    itemA: { icon: '🌾', title: '豊臣秀吉', detail: '全国統一の達成' },
                    itemB: { icon: '🗡️', title: '太閤検地・刀狩', detail: '兵農分離' },
                    category: '歴史',
                    title: '豊臣秀吉 ↔ 太閤検地・刀狩',
                    explanation: '全国の土地の大きさと収穫量を調べた「太閤検地」や、農民から武器を取り上げた「刀狩」により、武士と農民を区別する「兵農分離」を進めました。'
                },
                {
                    id: 'h13',
                    itemA: { icon: '🪨', title: '旧石器時代', detail: '日本列島の始まり' },
                    itemB: { icon: '🦴', title: '打製石器・マンモス', detail: '土器はまだない' },
                    category: '歴史',
                    title: '旧石器時代 ↔ 打製石器',
                    explanation: 'ナウマンゾウやマンモスを追いかけて移動生活を送りました。石を打ち砕いて作られた「打製石器」が使われました。'
                },
                {
                    id: 'h14',
                    itemA: { icon: '🌏', title: '渡来人（とらいじん）', detail: '朝鮮半島・中国から' },
                    itemB: { icon: '📜', title: '漢字・仏教・須恵器', detail: '高度な文化を伝える' },
                    category: '歴史',
                    title: '渡来人 ↔ 漢字・仏教・須恵器',
                    explanation: '5〜6世紀頃に大陸から日本へ移り住んだ渡来人は、漢字や儒教・仏教の教え、固い土器（須恵器）などの製法を伝えました。'
                },
                {
                    id: 'h15',
                    itemA: { icon: '☸️', title: '聖武天皇', detail: '奈良時代（天平文化）' },
                    itemB: { icon: '⛩️', title: '東大寺の大仏・国分寺', detail: '仏教で国を治める' },
                    category: '歴史',
                    title: '聖武天皇 ↔ 東大寺の大仏',
                    explanation: '疫病や社会の不安を仏教の力で静めようと考え、全国に国分寺を建て、都には「東大寺の大仏」を造らせました。'
                },
                {
                    id: 'h16',
                    itemA: { icon: '⛵', title: '鑑真（がんじん）', detail: '唐（中国）の高僧' },
                    itemB: { icon: '🏛️', title: '唐招提寺を開く', detail: '幾度の失明を乗り越え来日' },
                    category: '歴史',
                    title: '鑑真 ↔ 唐招提寺',
                    explanation: '正しい仏教の戒律を伝えるため、5回の渡航失敗で失明しながらも来日。奈良に「唐招提寺」を建てました。'
                },
                {
                    id: 'h17',
                    itemA: { icon: '📜', title: '菅原道真', detail: '平安時代（894年）' },
                    itemB: { icon: '🚫', title: '遣唐使の停止', detail: '唐の衰退と渡航危険' },
                    category: '歴史',
                    title: '菅原道真 ↔ 遣唐使の停止',
                    explanation: '唐の政治の乱れと渡航の危険性を理由に、894年に遣唐使の停止を提案。これが日本独自の「国風文化」の発展につながりました。'
                },
                {
                    id: 'h18',
                    itemA: { icon: '🌕', title: '藤原道長', detail: '平安時代（11世紀）' },
                    itemB: { icon: '👑', title: '摂関政治（この世をば...）', detail: '娘を天皇のきさきにする' },
                    category: '歴史',
                    title: '藤原道長 ↔ 摂関政治',
                    explanation: '娘を天皇の妃にすることで摂政・関白の職に就き、政治の実権を握りました。「この世をば...」の歌で全盛期を詠みました。'
                },
                {
                    id: 'h19',
                    itemA: { icon: '🛡️', title: '北条時宗', detail: '鎌倉幕府8代執権' },
                    itemB: { icon: '⚔️', title: '元寇（文永の役・弘安の役）', detail: 'モンゴル帝国の襲来' },
                    category: '歴史',
                    title: '北条時宗 ↔ 元寇',
                    explanation: 'ユーラシア大陸を支配した「元（モンゴル帝国）」が2度にわたって九州に襲来した際、御家人を率いてこれを退けました。'
                },
                {
                    id: 'h20',
                    itemA: { icon: '👸', title: '北条政子', detail: '源頼朝の妻（尼将軍）' },
                    itemB: { icon: '📜', title: '承久の乱で御家人を演説', detail: '朝廷（後鳥羽上皇）に対抗' },
                    category: '歴史',
                    title: '北条政子 ↔ 承久の乱での演説',
                    explanation: '頼朝の死後「承久の乱」が起きた際、御家人たちに頼朝の恩義を訴え結束させ、朝廷側の軍を破りました。'
                },
                {
                    id: 'h21',
                    itemA: { icon: '🎭', title: '観阿弥・世阿弥', detail: '室町時代' },
                    itemB: { icon: '🌸', title: '能（のう）を大成', detail: '足利義満の保護' },
                    category: '歴史',
                    title: '観阿弥・世阿弥 ↔ 能の大成',
                    explanation: '将軍・足利義満の保護を受け、伝統芸能である「能（能楽）」を芸術として完成させました。'
                },
                {
                    id: 'h22',
                    itemA: { icon: '🍵', title: '足利義政', detail: '室町幕府8代将軍' },
                    itemB: { icon: '🎨', title: '銀閣・東山文化（書院造）', detail: 'わび・さびの文化' },
                    category: '歴史',
                    title: '足利義政 ↔ 銀閣・東山文化',
                    explanation: '京都の東山に「銀閣」を建て、畳や床の間がある「書院造」や水墨画など、質素で深い味わい（わび・さび）の東山文化を生み出しました。'
                },
                {
                    id: 'h23',
                    itemA: { icon: '✝️', title: 'フランシスコ・ザビエル', detail: 'イエズス会宣教師（1549年）' },
                    itemB: { icon: '🔔', title: 'キリスト教の伝来', detail: '鹿児島に漂着' },
                    category: '歴史',
                    title: 'ザビエル ↔ キリスト教の伝来',
                    explanation: '1549年、鹿児島に到着して日本に初めて「キリスト教」を伝えました。信者は「キリシタン」と呼ばれ広まりました。'
                },
                {
                    id: 'h24',
                    itemA: { icon: '🏯', title: '徳川家康', detail: '1603年' },
                    itemB: { icon: '⚔️', title: '関ヶ原の戦い・江戸幕府', detail: '260年の泰平の世' },
                    category: '歴史',
                    title: '徳川家康 ↔ 江戸幕府の開設',
                    explanation: '1600年の「関ヶ原の戦い」で勝利し、1603年に征夷大将軍となって江戸幕府を開き、長きにわたる平和な時代を作りました。'
                }
            ]
        };

        class SoundEngine {
            constructor() {
                this.ctx = null;
                this.enabled = true;
            }

            init() {
                if (!this.ctx) {
                    this.ctx = new (window.AudioContext || window.webkitAudioContext)();
                }
            }

            playFlip() {
                if (!this.enabled) return;
                this.init();
                const osc = this.ctx.createOscillator();
                const gain = this.ctx.createGain();
                osc.type = 'sine';
                osc.frequency.setValueAtTime(350, this.ctx.currentTime);
                osc.frequency.exponentialRampToValueAtTime(700, this.ctx.currentTime + 0.08);
                gain.gain.setValueAtTime(0.12, this.ctx.currentTime);
                gain.gain.linearRampToValueAtTime(0.01, this.ctx.currentTime + 0.08);
                osc.connect(gain);
                gain.connect(this.ctx.destination);
                osc.start();
                osc.stop(this.ctx.currentTime + 0.08);
            }

            playMatch() {
                if (!this.enabled) return;
                this.init();
                const now = this.ctx.currentTime;
                const notes = [523.25, 659.25, 783.99, 1046.50];
                notes.forEach((freq, idx) => {
                    const osc = this.ctx.createOscillator();
                    const gain = this.ctx.createGain();
                    osc.type = 'triangle';
                    osc.frequency.setValueAtTime(freq, now + idx * 0.07);
                    gain.gain.setValueAtTime(0.18, now + idx * 0.07);
                    gain.gain.linearRampToValueAtTime(0.01, now + idx * 0.07 + 0.2);
                    osc.connect(gain);
                    gain.connect(this.ctx.destination);
                    osc.start(now + idx * 0.07);
                    osc.stop(now + idx * 0.07 + 0.2);
                });
            }

            playMismatch() {
                if (!this.enabled) return;
                this.init();
                const now = this.ctx.currentTime;
                const osc = this.ctx.createOscillator();
                const gain = this.ctx.createGain();
                osc.type = 'sawtooth';
                osc.frequency.setValueAtTime(240, now);
                osc.frequency.setValueAtTime(190, now + 0.1);
                gain.gain.setValueAtTime(0.12, now);
                gain.gain.linearRampToValueAtTime(0.01, now + 0.25);
                osc.connect(gain);
                gain.connect(this.ctx.destination);
                osc.start(now);
                osc.stop(now + 0.25);
            }

            playWin() {
                if (!this.enabled) return;
                this.init();
                const now = this.ctx.currentTime;
                const melody = [523.25, 659.25, 783.99, 880.00, 1046.50];
                melody.forEach((freq, idx) => {
                    const osc = this.ctx.createOscillator();
                    const gain = this.ctx.createGain();
                    osc.type = 'sine';
                    osc.frequency.setValueAtTime(freq, now + idx * 0.1);
                    gain.gain.setValueAtTime(0.2, now + idx * 0.1);
                    gain.gain.linearRampToValueAtTime(0.01, now + idx * 0.1 + 0.35);
                    osc.connect(gain);
                    gain.connect(this.ctx.destination);
                    osc.start(now + idx * 0.1);
                    osc.stop(now + idx * 0.1 + 0.35);
                });
            }
        }

        const sound = new SoundEngine();

        document.getElementById('soundToggleBtn').addEventListener('click', () => {
            sound.enabled = !sound.enabled;
            const icon = document.getElementById('soundIcon');
            if (sound.enabled) {
                icon.className = 'fas fa-volume-up text-lg text-indigo-600';
            } else {
                icon.className = 'fas fa-volume-mute text-lg text-slate-400';
            }
        });

        let currentMode = 'geography';
        let cards = [];
        let flippedCards = [];
        let matchedPairs = 0;
        let totalPairs = 6;
        let moves = 0;
        let timerInterval = null;
        let secondsElapsed = 0;
        let isProcessing = false;

        function showModeSelection() {
            clearInterval(timerInterval);
            document.getElementById('gameScreen').classList.add('hidden');
            document.getElementById('selectionScreen').classList.remove('hidden');
            document.getElementById('resultModal').classList.add('hidden');
            document.getElementById('explanationModal').classList.add('hidden');
        }

        function startGame(mode) {
            currentMode = mode;
            document.getElementById('selectionScreen').classList.add('hidden');
            document.getElementById('gameScreen').classList.remove('hidden');
            
            resetGameState();
            buildDeck();
            renderCards();
            startTimer();
        }

        function resetGameState() {
            cards = [];
            flippedCards = [];
            matchedPairs = 0;
            moves = 0;
            secondsElapsed = 0;
            isProcessing = false;
            
            document.getElementById('moveCount').textContent = '0';
            document.getElementById('matchCount').textContent = `0 / ${totalPairs}`;
            document.getElementById('timer').textContent = '00:00';
            clearInterval(timerInterval);
        }

        function buildDeck() {
            let pool = [];
            
            if (currentMode === 'geography') {
                pool = [...gameData.geography];
            } else if (currentMode === 'history') {
                pool = [...gameData.history];
            } else {
                pool = [...gameData.geography, ...gameData.history];
            }

            // Randomly select 6 pairs from the expanded question pool
            const selectedDataset = [...pool].sort(() => 0.5 - Math.random()).slice(0, 6);

            totalPairs = selectedDataset.length;
            document.getElementById('matchCount').textContent = `0 / ${totalPairs}`;

            let cardPool = [];
            selectedDataset.forEach(pair => {
                cardPool.push({
                    pairId: pair.id,
                    content: pair.itemA,
                    data: pair
                });
                cardPool.push({
                    pairId: pair.id,
                    content: pair.itemB,
                    data: pair
                });
            });

            // Fisher-Yates Shuffle
            for (let i = cardPool.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [cardPool[i], cardPool[j]] = [cardPool[j], cardPool[i]];
            }

            cards = cardPool;
        }

        function renderCards() {
            const grid = document.getElementById('cardGrid');
            grid.innerHTML = '';

            cards.forEach((card, index) => {
                const cardElement = document.createElement('div');
                cardElement.className = 'card-perspective aspect-[3/4] w-full cursor-pointer';
                cardElement.dataset.index = index;
                
                cardElement.innerHTML = `
                    <div class="card-inner h-full w-full" id="card-inner-${index}">
                        <div class="card-face card-front active:scale-95 transition-transform">
                            <span class="text-2xl sm:text-3xl mb-0.5 opacity-90">📘</span>
                            <span class="text-[10px] font-extrabold tracking-wider opacity-70">社会</span>
                        </div>
                        <div class="card-face card-back leading-tight">
                            <span class="text-[18px] sm:text-[22px] mb-1">${card.content.icon}</span>
                            <span class="font-black text-xs sm:text-sm text-slate-800 text-center px-1">${card.content.title}</span>
                            <span class="text-[9px] sm:text-[10px] font-bold text-slate-400 mt-1 text-center px-1">${card.content.detail}</span>
                        </div>
                    </div>
                `;

                cardElement.addEventListener('click', () => handleCardClick(index));
                grid.appendChild(cardElement);
            });
        }

        function handleCardClick(index) {
            if (isProcessing) return;
            const innerElement = document.getElementById(`card-inner-${index}`);
            
            if (innerElement.classList.contains('is-flipped') || innerElement.parentElement.classList.contains('matched')) {
                return;
            }

            sound.playFlip();
            innerElement.classList.add('is-flipped');
            flippedCards.push({ index, card: cards[index] });

            if (flippedCards.length === 2) {
                moves++;
                document.getElementById('moveCount').textContent = moves;
                checkMatch();
            }
        }

        function checkMatch() {
            isProcessing = true;
            const [first, second] = flippedCards;

            if (first.card.pairId === second.card.pairId) {
                setTimeout(() => {
                    sound.playMatch();
                    
                    const card1 = document.getElementById(`card-inner-${first.index}`).parentElement;
                    const card2 = document.getElementById(`card-inner-${second.index}`).parentElement;
                    
                    card1.classList.add('matched');
                    card2.classList.add('matched');

                    matchedPairs++;
                    document.getElementById('matchCount').textContent = `${matchedPairs} / ${totalPairs}`;

                    // Display educational explanation modal
                    openExplanationModal(first.card.data);

                    flippedCards = [];
                    isProcessing = false;
                }, 350);
            } else {
                setTimeout(() => {
                    sound.playMismatch();
                    document.getElementById(`card-inner-${first.index}`).classList.remove('is-flipped');
                    document.getElementById(`card-inner-${second.index}`).classList.remove('is-flipped');
                    flippedCards = [];
                    isProcessing = false;
                }, 900);
            }
        }

        function openExplanationModal(pairData) {
            document.getElementById('modalCategory').textContent = pairData.category;
            document.getElementById('modalEmoji').textContent = pairData.itemA.icon || '💡';
            document.getElementById('modalPairTitle').textContent = pairData.title;
            document.getElementById('modalExplanation').textContent = pairData.explanation;

            const modal = document.getElementById('explanationModal');
            const card = document.getElementById('modalCard');
            
            modal.classList.remove('hidden');
            setTimeout(() => {
                modal.classList.remove('opacity-0');
                card.classList.remove('scale-95');
                card.classList.add('scale-100');
            }, 10);
        }

        // Modified: Check if all pairs are completed AFTER closing the modal so the last explanation stays readable!
        function closeExplanationModal() {
            const modal = document.getElementById('explanationModal');
            const card = document.getElementById('modalCard');
            
            modal.classList.add('opacity-0');
            card.classList.remove('scale-100');
            card.classList.add('scale-95');
            
            setTimeout(() => {
                modal.classList.add('hidden');
                
                // Only trigger stage complete after player reads and closes the modal
                if (matchedPairs === totalPairs) {
                    completeGame();
                }
            }, 250);
        }

        function startTimer() {
            timerInterval = setInterval(() => {
                secondsElapsed++;
                const mins = String(Math.floor(secondsElapsed / 60)).padStart(2, '0');
                const secs = String(secondsElapsed % 60).padStart(2, '0');
                document.getElementById('timer').textContent = `${mins}:${secs}`;
            }, 1000);
        }

        function completeGame() {
            clearInterval(timerInterval);
            sound.playWin();

            confetti({
                particleCount: 100,
                spread: 70,
                origin: { y: 0.6 }
            });

            const starContainer = document.getElementById('starRating');
            let stars = 3;
            if (moves > totalPairs * 2.2) stars = 2;
            if (moves > totalPairs * 3.2) stars = 1;

            starContainer.innerHTML = '';
            for (let i = 0; i < 3; i++) {
                if (i < stars) {
                    starContainer.innerHTML += '<i class="fas fa-star text-amber-400"></i>';
                } else {
                    starContainer.innerHTML += '<i class="far fa-star text-slate-300"></i>';
                }
            }

            const mins = String(Math.floor(secondsElapsed / 60)).padStart(2, '0');
            const secs = String(secondsElapsed % 60).padStart(2, '0');
            document.getElementById('finalTime').textContent = `${mins}:${secs}`;
            document.getElementById('finalMoves').textContent = moves;

            document.getElementById('resultModal').classList.remove('hidden');
        }

        function restartGame() {
            document.getElementById('resultModal').classList.add('hidden');
            startGame(currentMode);
        }
    </script>
</body>
</html>
