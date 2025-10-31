<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <title>모스부호 해독기</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f0f0f0;
      text-align: center;
      padding: 40px;
    }
    textarea {
      width: 80%;
      height: 100px;
      font-size: 18px;
      margin-bottom: 20px;
    }
    button {
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
    }
    #output {
      margin-top: 20px;
      font-size: 24px;
      font-weight: bold;
      color: #222;
    }
  </style>
</head>
<body>
  <h1>모스부호 해독기</h1>
  <p>점(.)과 선(-)을 사용하고, 글자 구분은 <b>/</b>, 단어 구분은 <b>공백</b>으로 입력하세요.</p>

  <textarea id="morseInput" placeholder="예: .....././.-../.-../--- .--/---/.-./.-../-../"></textarea><br>
  <button onclick="decodeMorse()">해독하기</button>

  <div id="output"></div>

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

    function decodeMorse() {
      const input = document.getElementById("morseInput").value.trim();

      // 단어별 분리 (공백 기준)
      const words = input.split(" ");
      const decodedWords = words.map(word => {
        // 각 글자별 분리 (/ 기준)
        const letters = word.split("/");
        return letters.map(code => morseCode[code] || "").join("");
      });

      const result = decodedWords.join(" ");
      document.getElementById("output").innerText = result || "해독할 내용이 없습니다.";
    }
  </script>
</body>
</html>

