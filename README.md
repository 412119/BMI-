<!DOCTYPE html>
<html lang="zh-TW">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>現代 BMI計算機</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        body {
            background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
            min-height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            font-family: 'PingFang TC', 'Microsoft JhengHei', sans-serif;
        }
        .glass-card {
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 2rem;
            box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
        }
        input[type="range"] {
            accent-color: #4f46e5;
        }
    </style>
</head>
<body class="p-4">

    <div class="glass-card w-full max-w-md p-8">
        <h1 class="text-3xl font-bold text-center text-gray-800 mb-8">BMI 計算機</h1>
        
        <!-- 身高輸入 -->
        <div class="mb-8">
            <div class="flex justify-between items-center mb-2">
                <label class="text-gray-600 font-medium">身高 (cm)</label>
                <span id="heightDisplay" class="text-2xl font-bold text-indigo-600">170</span>
            </div>
            <input type="range" id="heightInput" min="100" max="220" value="170" 
                class="w-full h-2 bg-gray-200 rounded-lg appearance-none cursor-pointer">
        </div>

        <!-- 體重輸入 -->
        <div class="mb-8">
            <div class="flex justify-between items-center mb-2">
                <label class="text-gray-600 font-medium">體重 (kg)</label>
                <span id="weightDisplay" class="text-2xl font-bold text-indigo-600">65</span>
            </div>
            <input type="range" id="weightInput" min="30" max="150" value="65" 
                class="w-full h-2 bg-gray-200 rounded-lg appearance-none cursor-pointer">
        </div>

        <!-- 結果顯示區 -->
        <div id="resultCard" class="bg-indigo-50 rounded-2xl p-6 text-center transition-all duration-300">
            <p class="text-sm text-gray-500 uppercase tracking-wider mb-1">您的 BMI 指數</p>
            <h2 id="bmiValue" class="text-5xl font-black text-indigo-700 mb-2">22.5</h2>
            <div id="bmiStatus" class="inline-block px-4 py-1 rounded-full text-sm font-bold bg-green-100 text-green-700 mb-4">
                正常體重
            </div>
            <p id="bmiAdvice" class="text-gray-600 text-sm leading-relaxed">
                您的體重處於健康範圍，請繼續保持均衡飲食與規律運動！
            </p>
        </div>

        <div class="mt-8 grid grid-cols-4 gap-1 text-[10px] text-center text-gray-400">
            <div>< 18.5<br>過輕</div>
            <div>18.5 - 24<br>正常</div>
            <div>24 - 27<br>過重</div>
            <div>> 27<br>肥胖</div>
        </div>
    </div>

    <script>
        const heightInput = document.getElementById('heightInput');
        const weightInput = document.getElementById('weightInput');
        const heightDisplay = document.getElementById('heightDisplay');
        const weightDisplay = document.getElementById('weightDisplay');
        const bmiValue = document.getElementById('bmiValue');
        const bmiStatus = document.getElementById('bmiStatus');
        const bmiAdvice = document.getElementById('bmiAdvice');
        const resultCard = document.getElementById('resultCard');

        function updateBMI() {
            const h = parseFloat(heightInput.value);
            const w = parseFloat(weightInput.value);
            heightDisplay.innerText = h;
            weightDisplay.innerText = w;

            const bmi = (w / ((h / 100) ** 2)).toFixed(1);
            bmiValue.innerText = bmi;

            let status = "";
            let advice = "";
            let colorClass = "";
            let bgClass = "";

            if (bmi < 18.5) {
                status = "體重過輕";
                advice = "需要增加營養攝取，並進行適度的重量訓練來增加肌肉量。";
                colorClass = "text-blue-700";
                bgClass = "bg-blue-100";
                resultCard.className = "bg-blue-50 rounded-2xl p-6 text-center transition-all";
            } else if (bmi < 24) {
                status = "正常體重";
                advice = "您的體重處於健康範圍，請繼續保持均衡飲食與規律運動！";
                colorClass = "text-green-700";
                bgClass = "bg-green-100";
                resultCard.className = "bg-green-50 rounded-2xl p-6 text-center transition-all";
            } else if (bmi < 27) {
                status = "體重過重";
                advice = "建議微調飲食結構，減少高糖高油食物，增加日常活動量。";
                colorClass = "text-yellow-700";
                bgClass = "bg-yellow-100";
                resultCard.className = "bg-yellow-50 rounded-2xl p-6 text-center transition-all";
            } else {
                status = "肥胖";
                advice = "建議諮詢營養師或醫師，制定減重計畫以降低慢性疾病風險。";
                colorClass = "text-red-700";
                bgClass = "bg-red-100";
                resultCard.className = "bg-red-50 rounded-2xl p-6 text-center transition-all";
            }

            bmiStatus.innerText = status;
            bmiStatus.className = `inline-block px-4 py-1 rounded-full text-sm font-bold ${bgClass} ${colorClass} mb-4`;
        }

        heightInput.addEventListener('input', updateBMI);
        weightInput.addEventListener('input', updateBMI);

        // 初始化
        window.onload = updateBMI;
    </script>
</body>
</html>
