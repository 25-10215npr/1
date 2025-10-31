<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <title>모스부호 해독기</title>
  <style>
    body {
      font-family: "Segoe UI", Arial, sans-serif;
      background-color: #f5f6fa;
      text-align: center;
      padding: 40px;
      color: #333;
    }
    h1 {
      color: #2c3e50;
      margin-bottom: 10px;
    }
    p {
      font-size: 16px;
      color: #555;
    }
    textarea {
      width: 80%;
      height: 100px;
      font-size: 18px;
      margin: 20px 0;
      border-radius: 8px;
      border: 1px solid #ccc;
      padding: 10px;
      resize: none;
      outline: none;
    }
    textarea:focus {
      border-color: #3498db;
      box-shadow: 0 0 5px #3498db55;
    }
    button {
      padding: 10px 25px;
      font-size: 16px;
      cursor: pointer;
      border: none;
      border-radius: 6px;
      background-color: #3498db;
      color: white;
      transition: background-color 0.2s;
    }
    button:hover {
      background-color: #2980b9;
    }
    #output {
      margin-top: 20px;
      font-size: 26px;
      font-weight: bold;
      color: #2c3e50;
    }
    hr {
      margin: 40px 0 20px;
      border: none;
      border-top: 2px solid #ccc;
      width: 80%;
    }
    table {
      margin: 0 auto;
      border-collapse: collapse;
      width: 80%;
      background-color: white;
      border-radius: 8px;
      overflow: hidden;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    }
    th {
      background-color: #3498db;
      color: white;
      padding: 10px;
      font-size: 18px;
    }
    td {
      padding: 8px;
      border-bottom: 1px solid #eee;
      font-size: 18px;
    }
    tr:nth-child(even) {
      background-color: #f9f9f9;
    }
  </style>
</head>
<body>
  <h1>모스부호 해독기</h1>
  <p>점(<b>.</b>)과 선(<b>-</b>)을 사용하고, 글자 구분은 <b>/</b>, 단어 구분은 <b>공백</b>으로 입력하세요.</p>

  <textarea id="morseInput" placeholder="예: .....././.-../.-../--- .--/---/.-./.-../-../"></textarea><br>
  <button onclick="decodeMorse()">해독하기</button>

  <div id="output"></div>

  <hr>

  <h2> 모스부호 표</h2>

  <table>
    <thead>
      <tr><th>알파벳</th><th>모스부호</th><th>알파벳</th><th>모스부호</th></tr>
    </thead>
    <tbody id="morseTable"></tbody>
  </table>

  <script>
    const morseCode = {
      ".-": "A", "-...": "B", "-.-.": "C", "-..": "D", ".": "E",
      "..-.": "F", "--.": "G", "....": "H", "..": "I", ".---": "J",
      "-.-": "K", ".-..": "L", "--": "M", "-.": "N", "---": "O",
      ".--.": "P", "--.-": "Q", ".-.": "R", "...": "S", "-": "T",
      "..-": "U", "...-": "V", ".--": "W", "-..-": "X", "-.--": "Y", "--..": "Z",
      "-----": "0", ".----": "1", "..---": "2", "...--": "3", "....-": "4",
      ".....": "5", "-....": "6", "--...": "7", "---..": "8", "----.": "9"
    };

    // 역변환용 (표 생성용)
    const reverseMorse = Object.entries(morseCode)
      .map(([code, letter]) => ({ letter, code }))
      .sort((a, b) => a.letter.localeCompare(b.letter));

    function decodeMorse() {
      const input = document.getElementById("morseInput").value.trim();
      const words = input.split(" ");
      const decodedWords = words.map(word => {
        const letters = word.split("/");
        return letters.map(code => morseCode[code] || "").join("");
      });
      const result = decodedWords.join(" ");
      document.getElementById("output").innerText = result || "해독할 내용이 없습니다.";
    }

    // 표 자동 생성
    const tableBody = document.getElementById("morseTable");
    for (let i = 0; i < reverseMorse.length; i += 2) {
      const a = reverseMorse[i];
      const b = reverseMorse[i + 1];
      const row = document.createElement("tr");
      row.innerHTML = `
        <td>${a.letter}</td><td>${a.code}</td>
        <td>${b ? b.letter : ""}</td><td>${b ? b.code : ""}</td>
      `;
      tableBody.appendChild(row);
    }
  </script>
</body>
</html>
