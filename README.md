# -<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <title>Калькулятор стройматериалов</title>
  <style>
    body { font-family: Arial; background: #f0f0f0; padding: 20px; text-align: center; }
    h1 { color: #00796b; }
    input, button {
      padding: 10px;
      margin: 5px;
      font-size: 16px;
    }
    .section {
      background: #fff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 0 10px #ccc;
      margin-top: 20px;
      display: none;
    }
    #result1, #result2, #result3, #result4 {
      font-size: 20px;
      color: #2e7d32;
      margin-top: 10px;
    }
    .btn-select {
      margin: 5px;
      padding: 10px 20px;
      font-size: 18px;
      background-color: #26a69a;
      color: white;
      border: none;
      border-radius: 8px;
      cursor: pointer;
    }
  </style>
</head>
<body>

  <h1>Калькулятор стройматериалов</h1>
  <p>Выберите нужный калькулятор:</p>

  <button class="btn-select" onclick="showCalc('wood')">📏 Доски</button>
  <button class="btn-select" onclick="showCalc('concrete')">🧱 Бетон</button>
  <button class="btn-select" onclick="showCalc('brick')">🧱 Кирпич</button>
  <button class="btn-select" onclick="showCalc('block')">🧊 Блоки</button>

  <!-- Калькулятор древесины -->
  <div id="wood" class="section">
    <h2>Калькулятор досок</h2>
    <label>Ширина доски (см):</label><br>
    <input type="number" id="width"><br>

    <label>Толщина доски (см):</label><br>
    <input type="number" id="thickness"><br>

    <label>Длина доски (м):</label><br>
    <input type="number" id="length"><br>

    <button onclick="calcWood()">Рассчитать</button>
    <div id="result1"></div>
  </div>

  <!-- Калькулятор бетона -->
  <div id="concrete" class="section">
    <h2>Калькулятор бетона</h2>
    <label>Длина (м):</label><br>
    <input type="number" id="len_conc"><br>

    <label>Ширина (м):</label><br>
    <input type="number" id="wid_conc"><br>

    <label>Высота (м):</label><br>
    <input type="number" id="hei_conc"><br>

    <button onclick="calcConcrete()">Рассчитать</button>
    <div id="result2"></div>
  </div>

  <!-- Калькулятор кирпича -->
  <div id="brick" class="section">
    <h2>Калькулятор кирпича</h2>
    <label>Площадь стены (м²):</label><br>
    <input type="number" id="wall_area"><br>

    <label>На 1 м² кладки нужно ≈ 50 кирпичей</label><br>
    <button onclick="calcBrick()">Рассчитать</button>
    <div id="result3"></div>
  </div>

  <!-- Калькулятор блоков -->
  <div id="block" class="section">
    <h2>Калькулятор блоков</h2>
    <label>Длина блока (см):</label><br>
    <input type="number" id="block_len"><br>

    <label>Высота блока (см):</label><br>
    <input type="number" id="block_hei"><br>

    <label>Толщина блока (см):</label><br>
    <input type="number" id="block_wid"><br>

    <label>Объём стены (м³):</label><br>
    <input type="number" id="wall_vol"><br>

    <button onclick="calcBlocks()">Рассчитать</button>
    <div id="result4"></div>
  </div>

  <script>
    function showCalc(type) {
      ['wood', 'concrete', 'brick', 'block'].forEach(id => {
        document.getElementById(id).style.display = 'none';
      });
      document.getElementById(type).style.display = 'block';
    }

    function calcWood() {
      const w = parseFloat(document.getElementById("width").value) / 100;
      const t = parseFloat(document.getElementById("thickness").value) / 100;
      const l = parseFloat(document.getElementById("length").value);
      const one = w * t * l;
      const count = 1 / one;
      document.getElementById("result1").innerText =
        "Примерно " + Math.floor(count) + " досок в 1 м³.";
    }

    function calcConcrete() {
      const l = parseFloat(document.getElementById("len_conc").value);
      const w = parseFloat(document.getElementById("wid_conc").value);
      const h = parseFloat(document.getElementById("hei_conc").value);
      const volume = l * w * h;
      document.getElementById("result2").innerText =
        "Объём бетона: " + volume.toFixed(2) + " м³";
    }

    function calcBrick() {
      const area = parseFloat(document.getElementById("wall_area").value);
      const bricks = area * 50; // 50 кирпичей на 1 м²
      document.getElementById("result3").innerText =
        "Примерно " + Math.ceil(bricks) + " кирпичей потребуется.";
    }

    function calcBlocks() {
      const len = parseFloat(document.getElementById("block_len").value) / 100;
      const hei = parseFloat(document.getElementById("block_hei").value) / 100;
      const wid = parseFloat(document.getElementById("block_wid").value) / 100;
      const wallVol = parseFloat(document.getElementById("wall_vol").value);
      const blockVol = len * hei * wid;
      const blocks = wallVol / blockVol;
      document.getElementById("result4").innerText =
        "Потребуется примерно " + Math.ceil(blocks) + " блоков.";
    }
  </script>

</body>
</html>
