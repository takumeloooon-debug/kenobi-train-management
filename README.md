# kenobi-train-management
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>ダンス練習日記</title>

  <style>
    body {
      font-family: sans-serif;
      max-width: 600px;
      margin: 40px auto;
      padding: 0 20px;
    }

    textarea {
      width: 100%;
      height: 150px;
      margin-top: 10px;
    }

    button {
      margin-top: 10px;
      padding: 10px 20px;
    }

    .diary {
      border-top: 1px solid #ccc;
      padding: 20px 0;
    }
  </style>
</head>

<body>

  <h1>ダンス練習日記</h1>

  <input type="date" id="date">

  <textarea
    id="diaryText"
    placeholder="今日の練習について書く"
  ></textarea>

  <button onclick="saveDiary()">保存</button>

  <h2>過去の日記</h2>

  <div id="diaryList"></div>


  <script>
    let diaries =
      JSON.parse(localStorage.getItem("diaries")) || [];

    function saveDiary() {
      const date = document.getElementById("date").value;
      const text = document.getElementById("diaryText").value;

      if (!date || !text) {
        alert("日付と日記を入力してください");
        return;
      }

      diaries.unshift({
        date: date,
        text: text
      });

      localStorage.setItem(
        "diaries",
        JSON.stringify(diaries)
      );

      document.getElementById("diaryText").value = "";

      showDiaries();
    }

    function showDiaries() {
      const diaryList =
        document.getElementById("diaryList");

      diaryList.innerHTML = "";

      diaries.forEach(diary => {
        diaryList.innerHTML += `
          <div class="diary">
            <strong>${diary.date}</strong>
            <p>${diary.text}</p>
          </div>
        `;
      });
    }

    showDiaries();
