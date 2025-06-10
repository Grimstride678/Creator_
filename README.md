<html lang="ka">
<head>
  <meta charset="UTF-8" />
  <title>დათარსულები</title>
  <style>
    body {
      font-family: sans-serif;
      background-color: #f1e211;
      color: white;
      margin: 0;
      padding: 20px;
    }
    h1 {
      text-align: center;
      color: #000000;
    }
    p {
      text-align: left;
      color: #000000;
    }
    input[type="text"] {
      width: 100%;
      padding: 10px;
      margin-bottom: 20px;
      font-size: 16px;
    }
    .season {
      margin-bottom: 30px;
    }
    .season h2 {
      color: #000000;
    }
    .episode-list {
      display: flex;
      flex-wrap: wrap;
      gap: 10px;
    }
    .episode {
      width: 150px;
      background-color: #f87205;
      border-radius: 8px;
      overflow: hidden;
      cursor: pointer;
      transition: 0.3s;
    }
    .episode:hover {
      background-color: #ff9100;
    }
    .episode img {
      width: 100%;
      height: 90px;
      object-fit: cover;
    }
    .episode p {
      margin: 0;
      padding: 5px;
      text-align: center;
    }
    .video-player {
      position: fixed;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: rgba(0, 0, 0, 0.9);
      display: none;
      justify-content: center;
      align-items: center;
      z-index: 999;
    }
    .video-player iframe {
      width: 80%;
      height: 80%;
    }
    .video-player span {
      position: absolute;
      top: 20px; right: 30px;
      font-size: 30px;
      cursor: pointer;
      color: white;
    }
    .question {
      margin-bottom: 30px;
    }
    .btn {
      padding: 10px 20px;
      margin: 5px;
      border: none;
      border-radius: 8px;
      background-color: #333;
      color: white;
      cursor: pointer;
      transition: 0.3s;
    }
    .btn:hover {
      background-color: #555;
    }
    .correct {
      background-color: #28a745 !important;
    }
    .wrong {
      background-color: #dc3545 !important;
    }
  </style>
</head>
<body>
  <h1>დათარსულები</h1>
  <input type="text" id="search" placeholder="ძებნა...">

  <div id="container"></div>

  <div class="video-player" id="player">
    <span onclick="closePlayer()">✖</span>
    <iframe id="videoFrame" src="" frameborder="0" allowfullscreen></iframe>
  </div>

  <script>
    const data = {
      "სეზონი 1": [
        { title: "სოფლის კვერცხების ბიზნესი", youtubeId: "5BVyinRRqPg" },
        { title: "საერთო მტერი", youtubeId: "OlCaeeCsv-s" },
        { title: "მელოტი კაცების გაქირავება vs სველი წიგნები", youtubeId: "wyzcnJdXljo" },
        { title: "სულები", youtubeId: "ptUt74tYLbM" },
        ],
      "სეზონი 2": [
      { title: " კლასის არჩევნები", youtubeId: "XM7ls6YySh8" },
        { title: "განდრონის მოსვლა", youtubeId: "eKLtAuUZvpI" },
        { title: "განდრონის მოქმედება", youtubeId: "KlmvQB6yjjE" },
        { title: "განდრონი vs ყურსასხლეტი", youtubeId: "cdSoBn6Kv80" },
        { title: "ჩუმბაჩამბა", youtubeId: "_U7LXCCSbqU" },
        { title: "კუბასთან შეწინააღმდეგება", youtubeId: "HvDiCl014Vs" },
        { title: "საუკეთესო მომენტები სეზონი 1-2", youtubeId: "txWqx_vnnN0" },
      ],
      "სეზონი 3": [
      { title: "მშჩო", youtubeId: "AaMgE_lPFgI" },
        { title: "სტალინის მუზეუმის გადაწვა", youtubeId: "GnI34yZ2RTM" },
        { title: "სიზმრებთან ფრთხილად", youtubeId: "-k_6JThHYJo" },
        { title: "ჯადოქრების სკოლა", youtubeId: "E9gtOh7SUDY" },
        { title: "სიზმრების 2 თამაში", youtubeId: "UMGcKHiohkQ" },
        { title: "სიზმრებში შესასვლელი პორტალი", youtubeId: "oJyFsG7SUPM" },
        { title: "ხვრინტატორთან შეწინააღმდეგება ნაწილი:1", youtubeId: "pleHq321Trk" },
        { title: "ხვრინტატორთან შეწინააღმდეგება ნაწილი:2", youtubeId: "a_5qMHK8uPc" },
        { title: "სამოთხე x ჯოჯოხეთი", youtubeId: "mlHjUsyVyFw" },
        { title: "3 სეზონის საუკეთესო მომენტები", youtubeId: "-ZUxfoJxgcA" },
      ],
      "სეზონი 4": [
      { title: "დებატები", youtubeId: "PV92m26oR-I" },
        { title: "ნახმარი ტელეფონი", youtubeId: "3VSqaASiW3c" },
        { title: "მოჩვენება თარსულაში", youtubeId: "JRZv6W6M7ys" },
        { title: "ქვაბული", youtubeId: "fQb5rgzSyH0" },
        { title: "სიმართლის ზარი", youtubeId: "nw6YYGU3TB0" },
        { title: "ციხის მარგალიტები", youtubeId: "3Hx76CRxlLM" },
        { title: "ზვიგენის ხორხი", youtubeId: "t74LyMxaVcw" },
        { title: "განდრონი vs მურშაქი", youtubeId: "FSloWn9qn4E" },
        { title: "პოლიკას ახალი ბიზნესი", youtubeId: "DbP0d_EY9MU" },
        { title: "ტურამ,ტურამ, ყველა მოვკვდებით!", youtubeId: "UaJwy8cFgbY" },
        { title: "ჩამომსხენით", youtubeId: "0xURKw7bN0w" },
        { title: "4 სეზონის საუკეთესო მომენტები", youtubeId: "HhU0ezhIG6k" },
      ],
      "სეზონი 5": [
      { title: "დრაკონის წვა", youtubeId: "vKLqV6Lda4I" },
        { title: "შპს ბოდიში", youtubeId: "CwPhXJTjQH4" },
        { title: "chatლახი", youtubeId: "viDWnRE7oBo" },
        { title: "წლის შეწერვა", youtubeId: "3hqJWeK53lM" },
      ]
    };

    const container = document.getElementById("container");

    function render(searchedText = "") {
      container.innerHTML = "";
      for (const season in data) {
        const filteredEpisodes = data[season].filter(ep =>
          ep.title.toLowerCase().includes(searchedText.toLowerCase())
        );
        if (filteredEpisodes.length === 0) continue;

        const seasonDiv = document.createElement("div");
        seasonDiv.className = "season";
        seasonDiv.innerHTML = `<h2>${season}</h2>`;
        const list = document.createElement("div");
        list.className = "episode-list";

        filteredEpisodes.forEach(ep => {
          const episodeDiv = document.createElement("div");
          episodeDiv.className = "episode";
          episodeDiv.innerHTML = `
            <img src="https://img.youtube.com/vi/${ep.youtubeId}/0.jpg" alt="${ep.title}">
            <p>${ep.title}</p>
          `;
          episodeDiv.onclick = () => openPlayer(ep.youtubeId);
          list.appendChild(episodeDiv);
        });

        seasonDiv.appendChild(list);
        container.appendChild(seasonDiv);
      }
    }

    function openPlayer(id) {
      const player = document.getElementById("player");
      const frame = document.getElementById("videoFrame");
      frame.src = `https://www.youtube.com/embed/${id}?autoplay=1`;
      player.style.display = "flex";
    }

    function closePlayer() {
      const player = document.getElementById("player");
      const frame = document.getElementById("videoFrame");
      frame.src = "";
      player.style.display = "none";
    }

    document.getElementById("search").addEventListener("input", (e) => {
      render(e.target.value);
    });

    render();
  </script>
  <hr>

  <div class="quiz-container">
    <h1>ქვიზები</h1>

    <div class="question" id="q1">
      <p>1. დოჟრაჟის გამოყენებით რომელი შელოცვა უნდა გამოიყენო იმისთვის რომ ელვა წარმოქმნა?</p>
      <button class="btn" onclick="checkAnswer(this, 'q1', false)">გორდუს</button>
      <button class="btn" onclick="checkAnswer(this, 'q1', true)">ვოლტუს</button>
      <button class="btn" onclick="checkAnswer(this, 'q1', false)">ბარიერა</button>
    </div>

    <div class="question" id="q2">
      <p>2. რატომ მოკლა გაიოზმა ჩუმბაჩამბა?</p>
      <button class="btn" onclick="checkAnswer(this, 'q2', true)">შემთხვევით</button>
      <button class="btn" onclick="checkAnswer(this, 'q2', false)">პოლიკამ დააძალა</button>
      <button class="btn" onclick="checkAnswer(this, 'q2', false)">გაიოზს ეშინოდა რომ არ დასჯილიყო</button>
    </div>

    <div class="question" id="q3">
      <p>3. ბიჭებმა რატომ მოიპარეს სიმართლის ზარი?</p>
      <button class="btn" onclick="checkAnswer(this, 'q3', true)">კატა კლიზმამ დაავალა</button>
      <button class="btn" onclick="checkAnswer(this, 'q3', false)">მათ სიმართლის გაგება უნდოდათ</button>
      <button class="btn" onclick="checkAnswer(this, 'q3', false)">განადგურება უნდოდთ</button>
    </div>
  </div>

  <script>
    function checkAnswer(btn, questionId, isCorrect) {
      const questionDiv = document.getElementById(questionId);
      const buttons = questionDiv.querySelectorAll('button');

      buttons.forEach(button => {
        button.disabled = true;
        if (button === btn) {
          if (isCorrect) {
            button.classList.add('correct');
          } else {
            button.classList.add('wrong');
          }
        }
      });
    }
  </script>
</body>
</html>
