<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8">
  <title>🔍 محقق البيانات</title>
  <style>
    body {
      font-family: 'Comic Sans MS', cursive, sans-serif;
      text-align: center;
      margin-top: 50px;
      direction: rtl;
      background: linear-gradient(120deg, #f6d365, #fda085);
      color: #333;
    }
    h1 {
      color: #fff;
      text-shadow: 2px 2px 5px #ff69b4;
      font-size: 3em;
    }
    #question, #data {
      background-color: #fff;
      display: inline-block;
      padding: 15px 20px;
      border-radius: 15px;
      box-shadow: 2px 2px 10px rgba(0,0,0,0.2);
      margin: 10px 0;
      font-size: 1.2em;
    }
    input {
      padding: 10px;
      font-size: 16px;
      border-radius: 10px;
      border: 2px solid #ff69b4;
      width: 200px;
      text-align: center;
    }
    button {
      margin: 10px;
      padding: 10px 20px;
      font-size: 16px;
      border: none;
      border-radius: 12px;
      cursor: pointer;
      transition: all 0.2s;
    }
    button:hover {
      transform: scale(1.1);
    }
    #submitBtn { background-color: #ff69b4; color: #fff; }
    #nextBtn { background-color: #1e90ff; color: #fff; }
    #result {
      font-size: 1.5em;
      margin: 15px 0;
    }
    #score {
      font-weight: bold;
      font-size: 1.3em;
    }
  </style>
</head>
<body>
  <h1>🔍 محقق البيانات</h1>
  <p id="question">اضغط على "السؤال التالي" للبدء!</p>
  <p id="data"></p>
  <input type="text" id="answer" placeholder="اكتب إجابتك هنا">
  <br>
  <button id="submitBtn" onclick="checkAnswer()">تأكيد</button>
  <button id="nextBtn" onclick="nextQuestion()">السؤال التالي</button>
  <p id="result"></p>
  <p>النقاط: <span id="score">0</span></p>

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
      if (user == correct) {
        document.getElementById("result").innerText = "✅ صحيح!";
        document.getElementById("result").style.color = "#28a745";
        score++;
      } else {
        document.getElementById("result").innerText = "❌ خطأ! الإجابة الصحيحة هي " + correct;
        document.getElementById("result").style.color = "#dc3545";
      }
      document.getElementById("score").innerText = score;
    }
  </script>
</body>
</html>
