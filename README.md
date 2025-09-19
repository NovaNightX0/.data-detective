<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <title>🔍 محقق البيانات</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Comic+Neue:wght@700&display=swap');

    body {
      font-family: 'Comic Neue', cursive;
      text-align: center;
      margin-top: 50px;
      direction: rtl;
      background: linear-gradient(120deg, #f6d365, #fda085);
      color: #333;
      overflow-x: hidden;
    }
    h1 {
      color: #fff;
      text-shadow: 3px 3px 8px #ff69b4;
      font-size: 3em;
    }
    #question, #data {
      background-color: #fff;
      display: inline-block;
      padding: 15px 20px;
      border-radius: 20px;
      box-shadow: 3px 3px 15px rgba(0,0,0,0.3);
      margin: 10px 0;
      font-size: 1.3em;
    }
    input {
      padding: 12px;
      font-size: 16px;
      border-radius: 15px;
      border: 2px solid #ff69b4;
      width: 220px;
      text-align: center;
    }
    button {
      margin: 10px;
      padding: 12px 25px;
      font-size: 16px;
      border: none;
      border-radius: 15px;
      cursor: pointer;
      transition: all 0.2s;
      box-shadow: 2px 2px 10px rgba(0,0,0,0.2);
    }
    button:hover {
      transform: scale(1.1);
    }
    #submitBtn { background-color: #ff69b4; color: #fff; }
    #nextBtn { background-color: #1e90ff; color: #fff; }
    #result {
      font-size: 1.6em;
      margin: 15px 0;
      font-weight: bold;
    }
    #score {
      font-weight: bold;
      font-size: 1.4em;
      color: #fff;
      text-shadow: 1px 1px 3px #ff69b4;
    }
    #credits {
      margin-top: 30px;
      font-size: 1.1em;
      color: #fff;
      text-shadow: 1px 1px 3px #ff69b4;
    }

    /* Cute floating stars */
    .star {
      position: absolute;
      width: 10px;
      height: 10px;
      background: yellow;
      border-radius: 50%;
      animation: float 5s infinite linear;
      opacity: 0.7;
    }
    @keyframes float {
      0% { transform: translateY(0px) rotate(0deg); }
      50% { transform: translateY(-150px) rotate(180deg); }
      100% { transform: translateY(0px) rotate(360deg); }
    }
  </style>
</head>
<body>
  <h1>🔍 محقق البيانات</h1>
  <p id="question">اضغط على "السؤال التالي" للبدء!</p>
  <p id="data"></p>
  <input type="text" id="answer" placeholder="اكتب إجابتك هنا">
  <br>
  <button id="submitBtn" onclick="checkAnswer()">تأكيد ✅</button>
  <button id="nextBtn" onclick="nextQuestion()">السؤال التالي ➡️</button>
  <p id="result"></p>
  <p>النقاط: <span id="score">0</span> 🌟</p>
  <p id="credits">Made by Maysoon and Tasbeeh 💖</p>

  <script>
    let score = 0;
    let current;

    const datasets = [
      { type: "sum", data: [25, 10, 15], question: "ما مجموع مبيعات المنتج A؟" },
      { type: "average", data: [80, 90, 70], question: "ما متوسط درجات الطالب X؟" },
      { type: "max", data: [20, 45, 30], question: "ما أكبر عدد زوار في يوم واحد؟" },
      { type: "min", data: [50, 40, 60], question: "ما أقل درجة في مادة الرياضيات؟" },
      { type: "sum", data: [5, 15, 20], question: "كم مجموع الأصوات في الاستطلاع؟" },
      { type: "average", data: [10, 20, 30, 40], question: "ما المتوسط البسيط للأرقام التالية؟" }
    ];

    function nextQuestion() {
      document.getElementById("result").innerText = "";
      document.getElementById("answer").value = "";
      current = datasets[Math.floor(Math.random() * datasets.length)];
      document.getElementById("question").innerText = current.question;
      document.getElementById("data").innerText = "البيانات: " + current.data.join(", ");
    }

    function checkAnswer() {
      let correct;
      if (current.type === "sum") correct = current.data.reduce((a,b)=>a+b,0);
      if (current.type === "average") correct = Math.floor(current.data.reduce((a,b)=>a+b,0)/current.data.length);
      if (current.type === "max") correct = Math.max(...current.data);
      if (current.type === "min") correct = Math.min(...current.data);

      let user = document.getElementById("answer").value.trim();
      const resultEl = document.getElementById("result");
      if (user == correct) {
        resultEl.innerText = "✅ صحيح!";
        resultEl.style.color = "#28a745";
        score++;
        addStar();
      } else {
        resultEl.innerText = "❌ خطأ! الإجابة الصحيحة هي " + correct;
        resultEl.style.color = "#dc3545";
      }
      document.getElementById("score").innerText = score + " 🌟";
    }

    // Cute floating stars
    function addStar() {
      const star = document.createElement('div');
      star.className = 'star';
      star.style.left = Math.random() * window.innerWidth + 'px';
      star.style.background = `hsl(${Math.random()*360}, 100%, 70%)`;
      document.body.appendChild(star);
      setTimeout(() => star.remove(), 5000);
    }
  </script>
</body>
</html>
