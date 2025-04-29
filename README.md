<!DOCTYPE html>
<html lang="zh-Hant">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>康愛無憂—高風險族群理賠潛力分析</title>
  <script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
  <style>
    body {
      margin: 0;
      font-family: "Microsoft JhengHei", sans-serif;
      background: linear-gradient(135deg, #FFEFD5, #FFF0F5);
      color: #333;
    }
    .container {
      max-width: 1000px;
      margin: 30px auto;
      padding: 20px;
      background: #fff;
      border-radius: 16px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    }
    h2 {
      text-align: center;
      color: #6A5ACD;
      margin-bottom: 10px;
    }
    p.notice {
      font-size: 0.9rem;
      color: #888;
      text-align: center;
      margin-bottom: 30px;
    }
    canvas {
      display: block;
      margin: 20px auto;
      max-width: 100%;
    }
    .caption {
      font-size: 0.8rem;
      color: #666;
      text-align: right;
      margin-top: -15px;
    }
    .conclusion {
      background: #F0F8FF;
      padding: 20px;
      border-radius: 12px;
      margin-top: 40px;
    }
    .conclusion h3 {
      color: #DC143C;
    }
  </style>
</head>
<body>
  <div class="container">
    <h2>高風險族群未來理賠潛力量化分析</h2>
    <p class="notice">
      ※ 本內容僅做健康險產品介紹與醫療數據說明，非投保建議，詳細內容請以保單條款為準。
    </p>

    <!-- 1. 折線圖：平均住院日數 -->
    <h2>平均住院日數比較</h2>
    <canvas id="lineChart"></canvas>
    <p class="caption">
      資料來源：2021年全民健康保險醫療費用前二十大疾病平均住院日數 :contentReference[oaicite:0]{index=0}、2022年國人每住院者平均住院日數前二十大疾病 :contentReference[oaicite:1]{index=1}
    </p>

    <!-- 2. 圓餅圖：重大傷病醫療費用占比 -->
    <h2>重大傷病住院醫療費用占比（110年）</h2>
    <canvas id="pieChart"></canvas>
    <p class="caption">
      資料來源：110年住院重大傷病醫療費用分項 :contentReference[oaicite:2]{index=2}
    </p>

    <!-- 3. 柱狀圖：平均理賠金額預估（單次事件） -->
    <h2>單次事件平均理賠金額預估</h2>
    <canvas id="barChart"></canvas>
    <p class="caption">
      計算依據：住院日額1,000元×平均住院天數＋手術給付3,000元；商品特色 :contentReference[oaicite:3]{index=3}、投保範例 :contentReference[oaicite:4]{index=4}
    </p>

    <!-- 4. 其他圖表（雷達圖）：平均住院天數 vs 單次理賠金額 -->
    <h2>醫療事件—住院日數 vs 理賠金額雷達圖</h2>
    <canvas id="radarChart"></canvas>
    <p class="caption">
      資料來源同上
    </p>

    <div class="conclusion">
      <h3>結論與建議</h3>
      <ul>
        <li>高風險族群常見的肺炎（67.8 天）、中風（22 天）、癌症（16.5 天）住院平均天數最長，對應理賠金額可達70,770 元、24,990 元、19,460 元。</li>
        <li>重大傷病住院總費用中，癌症占將近五成，肺衰竭及長期呼吸器占比逾一成，顯示高齡三高、癌症病史者潛在住院次數與天數皆高。</li>
        <li>「康愛無憂」提供不限次數的住院日額及手術給付，加上加護病房、燒燙傷病房等多項保障，重複給付效益顯著。</li>
        <li>建議示警客戶：因後續多次住院或手術的累積理賠潛力遠超過繳費總額 300,000 元，購買本商品可有效緩解高額自費與家人照護壓力。</li>
      </ul>
    </div>
  </div>

  <script>
    // 折線圖資料
    const lineCtx = document.getElementById('lineChart').getContext('2d');
    new Chart(lineCtx, {
      type: 'line',
      data: {
        labels: ['呼吸系統疾病','腦血管疾病','腸胃道惡性腫瘤','其他心臟疾病','急性腎衰竭/慢性腎病'],
        datasets: [{
          label: '平均住院日數 (天)',
          data: [67.77, 21.99, 16.46, 9.71, 7.40],
          borderWidth: 2,
          fill: false,
          tension: 0.3
        }]
      },
      options: {
        responsive: true,
        scales: {
          y: { beginAtZero: true }
        }
      }
    });

    // 圓餅圖資料
    const pieCtx = document.getElementById('pieChart').getContext('2d');
    new Chart(pieCtx, {
      type: 'pie',
      data: {
        labels: ['癌症','呼吸衰竭長期使用呼吸器','慢性腎衰竭需透析','慢性精神病','急性腦血管疾病','其他'],
        datasets: [{
          data: [49.3,13.6,10.0,9.1,7.9,10.1],
          borderWidth: 1
        }]
      },
      options: { responsive: true }
    });

    // 柱狀圖資料
    const barCtx = document.getElementById('barChart').getContext('2d');
    new Chart(barCtx, {
      type: 'bar',
      data: {
        labels: ['呼吸系統疾病','腦血管疾病','腸胃道惡性腫瘤','其他心臟疾病','急性腎衰竭/慢性腎病'],
        datasets: [{
          label: '單次平均理賠金額 (元)',
          data: [70770,24990,19460,12710,10400],
          borderWidth: 1
        }]
      },
      options: {
        responsive: true,
        scales: {
          y: { beginAtZero: true }
        }
      }
    });

    // 雷達圖資料
    const radarCtx = document.getElementById('radarChart').getContext('2d');
    new Chart(radarCtx, {
      type: 'radar',
      data: {
        labels: ['呼吸系統疾病','腦血管疾病','腸胃道惡性腫瘤','其他心臟疾病','急性腎衰竭/慢性腎病'],
        datasets: [
          {
            label: '平均住院日數 (天)',
            data: [67.77,21.99,16.46,9.71,7.40],
            borderWidth: 2,
            fill: true,
            pointStyle: 'circle'
          },
          {
            label: '單次理賠金額 (萬)',
            data: [7.077,2.499,1.946,1.271,1.040],
            borderWidth: 2,
            fill: true,
            pointStyle: 'rect'
          }
        ]
      },
      options: { responsive: true }
    });
  </script>
</body>
</html>
