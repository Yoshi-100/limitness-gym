<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>リミットネス Gym</title>
  <style>
    /* 基本リセット */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    body {
      font-family: Arial, sans-serif;
      line-height: 1.6;
      background: #f4f4f4;
      color: #333;
    }
    /* ヘッダー */
    header {
      background: #333;
      color: #fff;
      padding: 20px;
      text-align: center;
    }
    header h1 {
      margin-bottom: 5px;
    }
    /* タブ用のナビゲーション */
    nav {
      background: #555;
      overflow: hidden;
    }
    nav .tab {
      float: left;
      display: block;
      color: #fff;
      text-align: center;
      padding: 14px 20px;
      text-decoration: none;
      cursor: pointer;
    }
    nav .tab:hover {
      background: #444;
    }
    nav .active {
      background: #222;
    }
    /* コンテナ */
    .container {
      padding: 20px;
    }
    .tab-content {
      display: none;
      background: #fff;
      padding: 20px;
      margin-top: 10px;
      border-radius: 4px;
      box-shadow: 0 0 5px rgba(0,0,0,0.1);
    }
    /* 予約フォーム等のスタイル */
    form input, form select, form button {
      display: block;
      width: 100%;
      padding: 8px;
      margin: 10px 0;
    }
    form label {
      margin-top: 10px;
      display: block;
    }
    .status-message {
      margin-top: 10px;
      padding: 10px;
      border-radius: 4px;
      display: none;
    }
    .status-success {
      background: #e0ffe0;
      color: #006600;
    }
    .status-error {
      background: #ffe0e0;
      color: #990000;
    }
    /* テーブル（予約状況表示用）のスタイル */
    table {
      width: 100%;
      border-collapse: collapse;
      margin-top: 10px;
    }
    table, th, td {
      border: 1px solid #ccc;
    }
    th, td {
      padding: 10px;
      text-align: center;
    }
  </style>
</head>
<body>
  <header>
    <h1>リミットネス Gym</h1>
    <p>～あなたの限界を超える場所～</p>
  </header>

  <nav>
    <div class="tab active" data-target="home">ホーム</div>
    <div class="tab" data-target="overview">ジム概要</div>
    <div class="tab" data-target="reservation">予約</div>
  </nav>

  <div class="container">
    <!-- ホームタブ -->
    <div id="home" class="tab-content" style="display: block;">
      <h2>Welcome to リミットネス Gym</h2>
      <p>リミットネスは、あなたの限界を挑戦するための最高の場所です。トレーニング設備は最新で、充実したサポート体制を整えています。ぜひ一度ご来館ください。</p>
      <img src="image.jpg" alt="ジムのイメージ" style="max-width:100%; height:auto;">
    </div>

    <!-- ジム概要タブ -->
    <div id="overview" class="tab-content">
      <h2>ジム概要</h2>
      <p>リミットネス Gym は、最新設備と経験豊富なトレーナーにより、あなたのフィットネスライフを全力でサポートします。広いトレーニングエリア、専用器具、ヨガ・ピラティス用スタジオなど、充実した施設を完備しています。</p>
      <h3>施設の特徴</h3>
      <ul>
        <li>最新マシン導入</li>
        <li>パーソナルトレーニングプログラム</li>
        <li>充実した会員専用ダッシュボード（今後の機能拡張予定）</li>
      </ul>
      <img src="image.jpg" alt="その他施設イメージ" style="max-width:100%; height:auto;">
    </div>

    <!-- 予約タブ -->
    <div id="reservation" class="tab-content">
      <h2>予約管理</h2>
      
      <!-- 予約状況確認 -->
      <section id="reservation-status">
        <h3>現在の予約状況</h3>
        <button id="checkReservationBtn">予約状況を確認する</button>
        <div id="reservationResults"></div>
      </section>
      
      <hr>

      <!-- 新規予約フォーム -->
      <section id="newReservation">
        <h3>新規予約</h3>
        <p>※ ご予約は、まず空いている日付と時間を選び、名字（苗字）を入力してください。初回ご利用の方は、氏名、性別、メール（任意）の入力も必要となります。</p>
        <form id="reservationForm">
          <label for="date">日付を選択</label>
          <input type="date" id="date" name="date" required>
          
          <label for="time">時間を選択</label>
          <select id="time" name="time" required>
            <option value="">-- 時間を選択 --</option>
            <option value="06:00">06:00</option>
            <option value="07:00">07:00</option>
            <option value="08:00">08:00</option>
            <option value="09:00">09:00</option>
            <option value="10:00">10:00</option>
            <!-- 必要に応じてオプション追加 -->
          </select>
          
          <label for="surname">名字（苗字）</label>
          <input type="text" id="surname" name="surname" placeholder="例：山田" required>
          
          <p>初回ご利用の方はこちらをご記入ください（既にご利用済みの方は不要です）</p>
          <label for="fullname">氏名</label>
          <input type="text" id="fullname" name="fullname" placeholder="例：山田 太郎">
          
          <label>性別</label>
          <select id="gender" name="gender">
            <option value="">-- 選択してください --</option>
            <option value="male">男性</option>
            <option value="female">女性</option>
          </select>
          
          <label for="email">メール（任意）</label>
          <input type="email" id="email" name="email" placeholder="例：example@example.com">
          
          <button type="submit">予約を送信</button>
        </form>
        <div id="formStatus" class="status-message"></div>
      </section>
    </div>
  </div>

  <script>
    // タブの切り替え機能
    document.querySelectorAll('nav .tab').forEach(function(tab) {
      tab.addEventListener('click', function() {
        // 全てのタブからactiveクラスを削除
        document.querySelectorAll('nav .tab').forEach(function(t) {
          t.classList.remove('active');
        });
        // 全てのタブコンテンツを非表示
        document.querySelectorAll('.tab-content').forEach(function(content) {
          content.style.display = 'none';
        });
        // クリックしたタブにactiveクラスを付与し、対応するコンテンツを表示
        tab.classList.add('active');
        var target = tab.getAttribute('data-target');
        document.getElementById(target).style.display = 'block';
      });
    });

    // 予約状況確認ボタンの処理
    document.getElementById('checkReservationBtn').addEventListener('click', function() {
      // 仮のAPIエンドポイントへGETリクエスト
      fetch('https://example.com/api/getReservationStatus')
        .then(function(response) {
          return response.json();
        })
        .then(function(data) {
          // 例：dataは以下と仮定
          // { reservations: [ {date:"2023-10-15", time:"08:00", surname:"山田"}, ... ] }
          var html = '<table><thead><tr><th>日付</th><th>時間</th><th>名字</th></tr></thead><tbody>';
          if(data.reservations && data.reservations.length > 0) {
            data.reservations.forEach(function(item) {
              html += '<tr><td>' + item.date + '</td><td>' + item.time + '</td><td>' + item.surname + '</td></tr>';
            });
          } else {
            html += '<tr><td colspan="3">予約はありません</td></tr>';
          }
          html += '</tbody></table>';
          document.getElementById('reservationResults').innerHTML = html;
        })
        .catch(function(error) {
          document.getElementById('reservationResults').innerHTML = 'エラーが発生しました。';
          console.error('Error:', error);
        });
    });

    // 予約フォーム送信の処理
    document.getElementById('reservationForm').addEventListener('submit', function(e) {
      e.preventDefault();

      var formData = {
        date: document.getElementById('date').value,
        time: document.getElementById('time').value,
        surname: document.getElementById('surname').value,
        fullname: document.getElementById('fullname').value,
        gender: document.getElementById('gender').value,
        email: document.getElementById('email').value
      };
      
      // 入力チェック（例：初回の場合、fullnameとgenderが未入力の場合は警告）
      if(formData.fullname === '' || formData.gender === '') {
        // 初回予約のときの入力を要求（※ここをユーザーの状況に合わせて調整します）
        if(!confirm("初回ご利用の場合、氏名と性別の入力が必要です。本当に続行しますか？")) {
          return;
        }
      }
      
      // 仮のAPIエンドポイントへPOSTリクエスト
      fetch('https://example.com/api/createReservation', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify(formData)
      })
      .then(function(response) {
        return response.json();
      })
      .then(function(result) {
        var statusDiv = document.getElementById('formStatus');
        // 仮想のレスポンス例: { success: true, message: "予約が完了しました" }
        if(result.success) {
          statusDiv.textContent = result.message || "予約が完了しました。確認メールを送信しました。";
          statusDiv.className = 'status-message status-success';
          statusDiv.style.display = 'block';
          // 必要ならフォームのリセットなど
          document.getElementById('reservationForm').reset();
        } else {
          statusDiv.textContent = result.message || "予約に失敗しました。";
          statusDiv.className = 'status-message status-error';
          statusDiv.style.display = 'block';
        }
      })
      .catch(function(error) {
        var statusDiv = document.getElementById('formStatus');
        statusDiv.textContent = "エラーが発生しました。";
        statusDiv.className = 'status-message status-error';
        statusDiv.style.display = 'block';
        console.error('Error:', error);
      });
    });
  </script>
</body>
</html>
