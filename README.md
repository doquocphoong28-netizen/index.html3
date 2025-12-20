<html lang="vi">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />

    <!-- Font dễ thương, hỗ trợ tiếng Việt -->
    <link
      href="https://fonts.googleapis.com/css2?family=Nunito:wght@300;600;800&family=Dancing+Script:wght@500;700&display=swap"
      rel="stylesheet"
    />

    <style>
      body {
        margin: 0;
        padding: 0;
        background: linear-gradient(#fff7fe, #f9fffb);
        text-align: center;
        font-family: "Nunito", sans-serif;
      }

      h2 {
        font-family: "Dancing Script", cursive;
        font-size: 42px;
        color: #ff4b8d;
      }

      /* FADE TOÀN TRANG */
      .fade {
        animation: fadeUp 1s ease forwards;
      }

      @keyframes fadeUp {
        from {
          opacity: 0;
          transform: translateY(20px);
        }
        to {
          opacity: 1;
          transform: translateY(0);
        }
      }

      /* KHUNG NHẬP TÊN */
      #nameBox {
        position: fixed;
        inset: 0;
        background: white;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        gap: 15px;
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
        font-family: "Dancing Script", cursive;
        cursor: pointer;
        box-shadow: 0 4px 12px rgba(255, 120, 170, 0.3);
        transition: 0.3s ease;
      }

      button:active {
        transform: scale(0.95);
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
        animation: fadeIn 1.2s ease;
        transition: 0.4s ease;
      }

      .avatar:hover {
        transform: scale(1.05);
      }

      @keyframes fadeIn {
        from {
          opacity: 0;
          transform: scale(0.9);
        }
        to {
          opacity: 1;
          transform: scale(1);
        }
      }

      /* LỜI MỜI */
      .invite-box {
        font-size: 26px;
        margin: 20px auto;
        width: 90%;
        padding: 25px;
        background: #fff2fa;
        border-radius: 18px;
        box-shadow: 0 4px 20px rgba(255, 100, 160, 0.25);
        min-height: 160px;
        white-space: pre-line;
        line-height: 1.5;
        word-break: break-word;
      }

      .typing {
        border-right: 3px solid #ff74aa;
        white-space: pre-line;
        overflow: hidden;
        animation: caret 0.6s infinite;
      }

      @keyframes caret {
        50% {
          border-color: transparent;
        }
      }

      /* KHỐI ĐỊA CHỈ */
      .info-box {
        background: #fff4fb;
        padding: 25px;
        width: 90%;
        margin: 20px auto;
        border-radius: 16px;
        font-size: 25px;
        box-shadow: 0 6px 18px rgba(255, 140, 190, 0.25);
      }

      /* LIÊN HỆ */
      .contact-box {
        background: #fff4fb;
        padding: 25px;
        width: 90%;
        margin: 20px auto 40px;
        border-radius: 16px;
        font-size: 25px;
        box-shadow: 0 6px 18px rgba(255, 193, 244, 0.2);
      }

      .script {
        font-family: "Dancing Script", cursive;
        font-size: 32px;
      }

      a {
        text-decoration: none;
        font-weight: 700;
      }
    </style>
  </head>

  <body>
    <!-- NHẬP TÊN -->
    <div id="nameBox">
      <h2>Cho Quốc Phong biết tên của bạn</h2>
      <input id="txtName" type="text" placeholder="Ví dụ: Đỗ Quốc Phong" />
      <button onclick="start()">Xác Nhận</button>
    </div>

    <!-- ẢNH -->
    <img
      src="img/z7317242070756_6ee59e5429d012f3dd053c8af7d958af.jpg"
      class="avatar"
    />

    <button onclick="showInvite()">✨ Mở Lời Mời ✨</button>

    <div id="invite" class="invite-box"></div>

    <!-- ĐỊA ĐIỂM -->
    <div class="info-box">
      🏫 <span class="script">Địa Điểm</span><br />
      Sân Trường THPT Lý Nhân Tông <br /><br />

      ⏰ <span class="script">Thời Gian</span> <br />
      9:30 AM – Chủ Nhật, 18/01/2026 <br /><br />

      <a
        href="https://maps.app.goo.gl/mBgtegybbqVoiKH5A"
        target="_blank"
        style="
          display: inline-block;
          background: #1d72f3;
          color: white;
          padding: 12px 25px;
          border-radius: 14px;
          font-size: 24px;
        "
      >
        📍 Mở Google Maps
      </a>
    </div>

    <!-- LIÊN HỆ -->
    <div class="contact-box">
      📞 <span class="script">Liên Hệ</span><br /><br />

      <a href="https://zalo.me/0389846825" style="color: #0094ff">
        💬 Zalo: Nhắn Tin Tại Đây
      </a>
      <br /><br />

      <a href="https://m.me/0389846825" style="color: #0055ff">
        📘 Messenger: Nhắn Tin Tại Đây
      </a>
    </div>

    <script>
      let userName = "";
      let textIndex = 0;
      let fullText = "";

      function start() {
        const name = document.getElementById("txtName").value.trim();
        if (name === "") return alert("Vui lòng nhập tên!");

        userName = name;
        document.getElementById("nameBox").style.display = "none";
        document.body.classList.add("fade");
      }

      function showInvite() {
        textIndex = 0;

        fullText = `✨ ${userName} thân mến ✨

Trân trọng kính mời ${userName} đến tham dự buổi lễ kỷ yếu của tôi.

Có ${userName} bên cạnh chắc chắn buổi kỷ yếu sẽ trọn vẹn hơn rất nhiều.
Để cùng nhau lưu lại những khoảnh khắc đẹp của tuổi học trò – khi mọi thứ vẫn còn trong veo và đáng nhớ.
Cùng chụp ảnh, cùng cười, và giữ lại những ký ức mà sau này nghĩ về vẫn thấy mỉm cười.`;

        document.getElementById(
          "invite"
        ).innerHTML = `<div class="typing" id="typingBox"></div>`;

        typeEffect();
      }

      function typeEffect() {
        const box = document.getElementById("typingBox");

        if (textIndex < fullText.length) {
          box.textContent += fullText.charAt(textIndex);
          textIndex++;
          setTimeout(typeEffect, 70);
        }
      }
    </script>

    <!-- NHẠC NỀN -->
    <audio id="bgm" loop>
      <source src="img/hoàn chỉnh.mp4" type="audio/mpeg" />
    </audio>

    <script>
      const bgm = document.getElementById("bgm");

      if (!sessionStorage.getItem("played")) {
        window.addEventListener(
          "click",
          () => {
            bgm.volume = 0.5;
            bgm.play();
            sessionStorage.setItem("played", "yes");
          },
          { once: true }
        );
      }
    </script>

    <!-- FOOTER -->
    <footer
      style="
        text-align: center;
        font-size: 13px;
        color: #aaa;
        margin: 40px 0;
        font-style: italic;
      "
    >
      Website được làm bằng những kỷ niệm nhỏ.<br />
      Nếu còn thiếu sót, mong mọi người thông cảm cho Phong.
    </footer>
  </body>
</html>





