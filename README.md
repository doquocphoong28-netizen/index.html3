<!DOCTYPE html>
<html lang="vi">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <link
      href="https://fonts.googleapis.com/css2?family=Nunito:wght@300;600;800&family=Dancing+Script:wght@500;700&display=swap"
      rel="stylesheet"
    />

    <style>
      body {
        margin: 0;
        background: linear-gradient(#fff7fe, #f9fffb);
        font-family: "Nunito", sans-serif;
        text-align: center;
        overflow-x: hidden;
      }
      h2 {
        font-family: "Dancing Script";
        font-size: 42px;
        color: #ff4b8d;
      }

      /* NAME BOX */
      #nameBox {
        position: fixed;
        inset: 0;
        background: white;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        z-index: 999;
      }
      #txtName {
        width: 80%;
        height: 50px;
        font-size: 22px;
        border-radius: 12px;
        border: 2px solid #ffa1cf;
        padding-left: 12px;
      }
      button {
        background: #ffe3f4;
        border: none;
        padding: 12px 25px;
        font-size: 22px;
        border-radius: 14px;
        color: #ff4b8d;
        font-family: "Dancing Script";
        cursor: pointer;
        box-shadow: 0 4px 12px rgba(255, 120, 170, 0.3);
      }

      /* AVATAR */
      .avatar {
        width: 170px;
        height: 170px;
        border-radius: 50%;
        border: 4px solid #ffb6d9;
        object-fit: cover;
        margin-top: 30px;
        box-shadow: 0 0 20px rgba(255, 100, 160, 0.4);
      }

      /* INVITE */
      .invite-box {
        font-size: 26px;
        width: 90%;
        margin: 20px auto;
        padding: 25px;
        background: #fff2fa;
        border-radius: 18px;
        box-shadow: 0 4px 20px rgba(255, 100, 160, 0.25);
        white-space: pre-line;
        line-height: 1.5;
      }
      .typing {
        border-right: 3px solid #ff74aa;
        animation: caret 0.6s infinite;
      }
      @keyframes caret {
        50% {
          border-color: transparent;
        }
      }

      /* GAME */
      .game-box {
        width: 90%;
        margin: 40px auto;
        padding: 30px;
        background: #fff6fb;
        border-radius: 20px;
        box-shadow: 0 10px 30px rgba(255, 120, 170, 0.3);
        display: none;
      }
      .game-title {
        font-family: "Dancing Script";
        font-size: 36px;
        color: #ff4b8d;
      }
      .stars {
        display: flex;
        justify-content: center;
        gap: 20px;
        margin: 25px 0;
        flex-wrap: wrap;
      }
      .star {
        font-size: 42px;
        cursor: pointer;
        animation: pulse 1.5s infinite;
      }
      @keyframes pulse {
        0% {
          transform: scale(1);
        }
        50% {
          transform: scale(1.2);
        }
        100% {
          transform: scale(1);
        }
      }
      .star.collected {
        opacity: 0;
        transform: translateY(-80px);
        transition: 0.6s;
      }
      .game-msg {
        font-family: "Dancing Script";
        font-size: 26px;
        color: #ff4b8d;
        min-height: 50px;
      }

      /* FINAL OVERLAY */
      .overlay {
        position: fixed;
        inset: 0;
        background: rgba(0, 0, 0, 0.55);
        display: none;
        justify-content: center;
        align-items: center;
        z-index: 998;
      }
      .final-box {
        background: white;
        padding: 35px 30px;
        border-radius: 22px;
        box-shadow: 0 20px 40px rgba(255, 100, 160, 0.4);
        animation: zoom 0.8s ease;
        max-width: 90%;
      }
      @keyframes zoom {
        from {
          transform: scale(0.5);
          opacity: 0;
        }
        to {
          transform: scale(1);
          opacity: 1;
        }
      }
      .final-text {
        font-family: "Dancing Script";
        font-size: 30px;
        color: #ff4b8d;
        line-height: 1.4;
      }
      .tap-close {
        margin-top: 18px;
        font-size: 14px;
        color: #999;
        font-style: italic;
      }

      /* ADDRESS */
      .info-box {
        width: 90%;
        margin: 30px auto;
        padding: 28px;
        background: linear-gradient(135deg, #fff0f8, #f9fffb);
        border-radius: 22px;
        box-shadow: 0 8px 25px rgba(255, 140, 190, 0.3);
        font-size: 24px;
      }
      .info-row {
        margin: 12px 0;
      }
      .info-icon {
        font-size: 26px;
        margin-right: 8px;
      }
      .map-btn {
        display: inline-block;
        margin-top: 18px;
        background: #ff4b8d;
        color: white;
        padding: 12px 28px;
        border-radius: 30px;
        font-size: 22px;
        box-shadow: 0 6px 18px rgba(255, 100, 160, 0.4);
      }
    </style>
  </head>

  <body>
    <div id="nameBox">
      <h2>Cho Quốc Phong biết tên của bạn</h2>
      <input id="txtName" placeholder="Ví dụ: Đỗ Quốc Phong" />
      <button onclick="start()">Xác nhận</button>
    </div>

    <img
      src="img/z7317242070756_6ee59e5429d012f3dd053c8af7d958af.jpg"
      class="avatar"
    />

    <button onclick="showInvite()">✨ Mở Lời Mời ✨</button>

    <div id="invite" class="invite-box"></div>

    <div class="game-box" id="game">
      <div class="game-title">✨ Thu Thập Ký Ức ✨</div>
      <div class="stars" id="stars"></div>
      <div class="game-msg" id="gameMsg"></div>
    </div>

    <!-- FINAL MESSAGE -->
    <div class="overlay" id="overlay" onclick="closeOverlay()">
      <div class="final-box" onclick="event.stopPropagation()">
        <div class="final-text" id="finalText"></div>
        <div class="tap-close">(Chạm ra ngoài để đóng)</div>
      </div>
    </div>

    <!-- ADDRESS -->
    <div class="info-box">
      <div class="info-row">
        <span class="info-icon">🏫</span>
        <b>Địa điểm:</b> Sân Trường THPT Lý Nhân Tông
      </div>
      <div class="info-row">
        <span class="info-icon">⏰</span>
        <b>Thời gian:</b> 10:30 AM – Chủ Nhật, 18/01/2026
      </div>
      <a
        class="map-btn"
        href="https://maps.app.goo.gl/mBgtegybbqVoiKH5A"
        target="_blank"
      >
        📍 Mở Google Maps
      </a>
    </div>

    <script>
      let userName = "",
        textIndex = 0,
        fullText = "";
      function start() {
        userName = txtName.value.trim();
        if (!userName) return alert("Nhập tên trước nha 😭");
        nameBox.style.display = "none";
      }

      function showInvite() {
        fullText = `✨ ${userName} thân mến ✨

Nhân gian vạn kiếp như hư ảnh,
Thanh xuân một đoạn hóa tiên duyên.
Ngày sau ngoảnh lại mỉm cười khẽ,
Hóa ra năm ấy… đã có nhau..`;
        invite.innerHTML = '<div class="typing" id="typingBox"></div>';
        typeEffect();
      }

      function typeEffect() {
        const box = document.getElementById("typingBox");
        if (textIndex < fullText.length) {
          box.textContent += fullText.charAt(textIndex++);
          setTimeout(typeEffect, 55);
        } else {
          game.style.display = "block";
          createStars();
        }
      }

      /* GAME */
      const messages = [
        "Một ngày nắng đẹp 🌸",
        "Một tiếng cười vô tư ✨",
        "Một người từng rất thân 💕",
        "Một đoạn ký ức không quên 🌈",
        "Thanh xuân đã thật trọn vẹn 🎓",
      ];
      let collected = 0;
      function createStars() {
        for (let i = 0; i < 5; i++) {
          const s = document.createElement("div");
          s.className = "star";
          s.textContent = "⭐";
          s.onclick = () => {
            s.classList.add("collected");
            gameMsg.textContent = messages[collected];
            collected++;
            if (collected === 5) setTimeout(showFinal, 700);
          };
          stars.appendChild(s);
        }
      }

      function showFinal() {
        overlay.style.display = "flex";
        finalText.innerHTML = `💖 ${userName} 💖<br><br>
  Cảm ơn vì đã là một phần<br>
  của thanh xuân này.`;
      }
      function closeOverlay() {
        overlay.style.display = "none";
      }
    </script>

    <audio id="bgm" loop>
      <source src="img/hoàn chỉnh.mp4" type="audio/mpeg" />
    </audio>
    <script>
      window.addEventListener(
        "click",
        () => {
          bgm.volume = 0.5;
          bgm.play();
        },
        { once: true }
      );
    </script>
  </body>
</html>







