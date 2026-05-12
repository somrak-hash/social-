<html lang="th">
<head>
  <meta charset="UTF-8">
  <title>Geo-Location Guessing Game</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body { font-family: 'Kanit', sans-serif; background: #f0f0f8; margin:0; padding:0; }
    .container {
      width: 95%; max-width: 400px; margin: 60px auto; padding: 28px;
      background: #fff; border-radius: 16px; box-shadow: 0 5px 24px #a3b3ff30;
      text-align: center;
    }
    h1 { color: #4b61d1; margin-bottom: 22px;}
    .clue-img {
      width: 100%; border-radius: 11px; margin-bottom: 16px; box-shadow: 0 2px 8px #4441;
    }
    .input-group { margin:16px 0;}
    input[type="text"] {
      padding: 9px; width: 70%; border-radius: 6px;
      border: 1px solid #bcc; font-size: 1.05em;
    }
    button {
      background: #5b63e7; color: #fff; border: none; border-radius: 6px;
      padding: 9px 20px; font-size: 1.07em; cursor: pointer;
      margin-left:8px;
    }
    .result { margin: 16px 0; font-size: 1.13em; min-height: 30px; }
    .score { margin-bottom: 9px; color: #099d7a;}
    .next-btn { background:#a3b3ff; color:#223; margin-top:10px;}
  </style>
</head>
<body>
  <div class="container">
    <h1>เกมทายตำแหน่งภูมิศาสตร์</h1>
    <div class="score">คะแนน: <span id="score">0</span></div>
    <img id="clueImg" class="clue-img" src="" alt="รูปสถานที่" style="display:none;">
    <div id="hint" class="hint">กำลังโหลดคำใบ้…</div>
    <div class="input-group">
      <input type="text" id="guessInput" placeholder="กรอกชื่อเมืองหรือประเทศ">
      <button onclick="submitGuess()">ส่งคำตอบ</button>
    </div>
    <div class="result" id="result"></div>
    <button class="next-btn" onclick="nextQuestion()">ถัดไป</button>
  </div>
  <script>
    // ตัวอย่างข้อมูลโจทย์
    const data = [
      {
        image: "https://upload.wikimedia.org/wikipedia/commons/9/9e/Tokyo_Shibuya_Scramble_Crossing_2018-10-09.jpg",
        answer: "โตเกียว",
        hint: "เมืองหลวงของญี่ปุ่น มีแยกไฟแดงที่คนข้ามเยอะที่สุดในโลก"
      },
      {
        image: "https://upload.wikimedia.org/wikipedia/commons/a/a1/Eiffel_Tower_at_Sunset_%28Paris%29.jpg",
        answer: "ปารีส",
        hint: "หอไอเฟลตั้งอยู่ที่นี่ เมืองหลวงของฝรั่งเศส"
      },
      {
        image: "https://upload.wikimedia.org/wikipedia/commons/e/e1/Grand_Palace_Bangkok_Thailand.jpg",
        answer: "กรุงเทพ",
        hint: "พระบรมมหาราชวังตั้งอยู่ที่เมืองหลวงของประเทศไทย"
      },
      {
        image: "https://upload.wikimedia.org/wikipedia/commons/d/d4/Statue_of_Liberty%2C_NY.jpg",
        answer: "นิวยอร์ก",
        hint: "เทพีเสรีภาพเป็นสัญลักษณ์สำคัญของเมืองนี้"
      }
      // เพิ่มอีกได้ตามต้องการ
    ];

    let current = 0, score = 0;

    function showQuestion() {
      document.getElementById('result').textContent = "";
      document.getElementById('guessInput').value = "";
      const q = data[current];
      if(q.image) {
        document.getElementById('clueImg').src = q.image;
        document.getElementById('clueImg').style.display = "";
      } else {
        document.getElementById('clueImg').style.display = "none";
      }
      document.getElementById('hint').textContent = (q.hint || "");
    }

    function submitGuess() {
      const ans = data[current].answer.trim().toLowerCase();
      const guess = document.getElementById('guessInput').value.trim().toLowerCase();
      if (!guess) return;
      if (guess === ans) {
        document.getElementById('result').textContent = "✅ ถูกต้อง!";
        score++;
        document.getElementById('score').textContent = score;
      } else {
        document.getElementById('result').textContent = "❌ ไม่ถูกต้อง คำตอบคือ: " + data[current].answer;
      }
    }

    function nextQuestion() {
      current++;
      if (current >= data.length) {
        document.getElementById('hint').textContent = "";
        document.getElementById('clueImg').style.display = "none";
        document.getElementById('result').textContent = "เกมจบแล้ว! คะแนนรวม: " + score + "/" + data.length;
        document.querySelector('.next-btn').disabled = true;
        document.querySelector('.input-group').style.display = "none";
        return;
      }
      showQuestion();
    }

    // เริ่มเกม
    showQuestion();
  </script>
</body>
</html>
