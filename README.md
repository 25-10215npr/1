<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8" />
  <title>모스부호 해독기</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #f4f4f4;
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
      color: #333;
    }
  </style>
</head>
<body>
  <h1>모스부호 해독기</h1>
  <p>점(.)과 선(-)을 입력하고, 단어는 /로 구분하세요.</p>

  <textarea id="morseInput" placeholder="예: .... . .-.. .-.. --- / .-- --- .-. .-.. -.."></textarea><br>
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
      const words = input.split(" / "); // 단어 구분
      const decoded = words.map(word => {
        return word.split(" ").map(code => morseCode[code] || "").join("");
      }).join(" ");
      document.getElementById("output").innerText = decoded || "해독할 내용이 없습니다.";
    }
  </script>
</body>
</html>
