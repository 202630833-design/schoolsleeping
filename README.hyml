<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>랜덤 핑계 생성기 | 오늘만 넘어가자!</title>
  <style>
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Pretendard', -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
    }

    body {
      background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
      min-height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 20px;
      color: #333;
    }

    .card {
      background: #ffffff;
      width: 100%;
      max-width: 520px;
      padding: 35px 25px;
      border-radius: 24px;
      box-shadow: 0 20px 40px rgba(0, 0, 0, 0.2);
      text-align: center;
      position: relative;
      overflow: hidden;
    }

    .badge {
      display: inline-block;
      background: #f1f3f5;
      color: #5c7cfa;
      font-weight: 700;
      font-size: 13px;
      padding: 6px 14px;
      border-radius: 20px;
      margin-bottom: 12px;
    }

    h1 {
      font-size: 26px;
      font-weight: 800;
      color: #2b2c34;
      margin-bottom: 8px;
    }

    p.subtitle {
      font-size: 14px;
      color: #626471;
      margin-bottom: 25px;
    }

    /* Tab controls for category */
    .category-tabs {
      display: flex;
      justify-content: center;
      gap: 8px;
      margin-bottom: 25px;
      flex-wrap: wrap;
    }

    .tab-btn {
      background: #f8f9fa;
      border: 1px solid #e9ecef;
      padding: 8px 16px;
      border-radius: 12px;
      font-size: 13px;
      font-weight: 600;
      color: #495057;
      cursor: pointer;
      transition: all 0.2s ease;
    }

    .tab-btn.active {
      background: #5c7cfa;
      color: #ffffff;
      border-color: #5c7cfa;
      box-shadow: 0 4px 10px rgba(92, 124, 250, 0.3);
    }

    /* Output Display Area */
    .display-box {
      background: #f8f9fa;
      border: 2px dashed #bac8ff;
      border-radius: 18px;
      padding: 30px 20px;
      min-height: 150px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      margin-bottom: 25px;
      position: relative;
    }

    .excuse-text {
      font-size: 18px;
      font-weight: 700;
      color: #343a40;
      line-height: 1.5;
      word-break: keep-all;
      transition: transform 0.2s cubic-bezier(0.175, 0.885, 0.32, 1.275);
    }

    .excuse-tag {
      margin-top: 10px;
      font-size: 12px;
      color: #868e96;
      font-weight: 500;
    }

    /* Buttons Group */
    .btn-group {
      display: flex;
      gap: 10px;
    }

    .action-btn {
      flex: 1;
      padding: 14px;
      border: none;
      border-radius: 14px;
      font-size: 15px;
      font-weight: 700;
      cursor: pointer;
      transition: transform 0.1s ease, box-shadow 0.2s ease;
    }

    .generate-btn {
      background: #5c7cfa;
      color: #ffffff;
      box-shadow: 0 6px 15px rgba(92, 124, 250, 0.4);
    }

    .generate-btn:hover {
      background: #4c6ef5;
    }

    .generate-btn:active {
      transform: scale(0.98);
    }

    .copy-btn {
      background: #e9ecef;
      color: #495057;
      width: 100px;
      flex: none;
    }

    .copy-btn:hover {
      background: #dee2e6;
    }

    /* Toast Notification */
    .toast {
      position: absolute;
      bottom: -50px;
      left: 50%;
      transform: translateX(-50%);
      background: rgba(33, 37, 41, 0.9);
      color: #ffffff;
      padding: 10px 20px;
      border-radius: 20px;
      font-size: 13px;
      font-weight: 500;
      opacity: 0;
      transition: all 0.3s ease;
      pointer-events: none;
    }

    .toast.show {
      bottom: 20px;
      opacity: 1;
    }
  </style>
</head>
<body>

  <div class="card">
    <span class="badge">🔥 위기 탈출 메이커</span>
    <h1>랜덤 핑계 생성기</h1>
    <p class="subtitle">상황을 선택하고 버튼을 누르면 위기 탈출 핑계가 완성됩니다.</p>

    <!-- Category Tabs -->
    <div class="category-tabs">
      <button class="tab-btn active" onclick="setCategory('all')">🎲 전체</button>
      <button class="tab-btn" onclick="setCategory('tardy')">⏰ 지각</button>
      <button class="tab-btn" onclick="setCategory('absent')">🙅‍♂️ 불참/약속취소</button>
      <button class="tab-btn" onclick="setCategory('task')">📝 과제/업무미제출</button>
      <button class="tab-btn" onclick="setCategory('crazy')">👽 엉뚱/황당</button>
    </div>

    <!-- Excuse Display -->
    <div class="display-box">
      <div class="excuse-text" id="excuseDisplay">아래 '핑계 뽑기' 버튼을 눌러보세요!</div>
      <div class="excuse-tag" id="excuseTag">#준비완료</div>
    </div>

    <!-- Controls -->
    <div class="btn-group">
      <button class="action-btn generate-btn" onclick="generateExcuse()">🎲 핑계 뽑기!</button>
      <button class="action-btn copy-btn" onclick="copyExcuse()">📋 복사</button>
    </div>

    <!-- Toast Notice -->
    <div class="toast" id="toast">핑계가 클립보드에 복사되었습니다!</div>
  </div>

  <script>
    const excuses = [
      // 지각 (tardy)
      { text: "엘리베이터가 고장 나서 20층부터 계단으로 걸어 내려왔습니다.", category: "tardy", tag: "#지각 #체력강화" },
      { text: "집 나오자마자 고양이가 길을 막고 안 비켜줘서 설득하느라 늦었습니다.", category: "tardy", tag: "#지각 #귀여움주의" },
      { text: "버스 기사님이 오늘따라 안전운전을 너무 철저하게 하셔서 정시 도착이 불가능했습니다.", category: "tardy", tag: "#지각 #안전제일" },
      { text: "신발 끈을 묶는데 무한 루프에 빠져서 풀어내느라 시간이 걸렸습니다.", category: "tardy", tag: "#지각 #패션의완성" },
      { text: "알람 소리가 너무 좋아서 꿈속에서 리듬 타고 감상하느라 늦었습니다.", category: "tardy", tag: "#지각 #음악감상" },

      // 불참/약속취소 (absent)
      { text: "갑자기 집에 급한 일이 생겨서 오늘 약속은 어려울 것 같습니다. 죄송합니다!", category: "absent", tag: "#약속취소 #정석" },
      { text: "갑자기 식중독 증세가 살짝 있어서 오늘은 집에서 쉬어야 할 것 같아요.", category: "absent", tag: "#약속취소 #환자모드" },
      { text: "집에 보일러가 터져서 지금 물을 퍼내야 하는 긴급 상황입니다.", category: "absent", tag: "#약속취소 #재난상황" },
      { text: "오늘따라 기운이 너무 빠져서 나가면 민폐만 될 것 같아요. 다음에 맛있는 거 살게요!", category: "absent", tag: "#약속취소 #에너지고갈" },

      // 과제/업무미제출 (task)
      { text: "파일을 열심히 만들었는데 저장을 안 하고 컴퓨터가 재부팅되어 버렸습니다...", category: "task", tag: "#업무 #블루스크린" },
      { text: "최종본 파일명이 '진짜최종_final_v2.docx'였는데 실수로 삭제해 버렸습니다.", category: "task", tag: "#과제 #휴지통복구중" },
      { text: "자료 조사를 너무 깊게 하다 보니 논문의 바다에 빠져서 아직 정리 중입니다.", category: "task", tag: "#과제 #학구열폭발" },
      { text: "어제 작성한 데이터가 인공지능에 의해 보안 조치되어 승인 대기 중입니다.", category: "task", tag: "#업무 #하이테크" },

      // 엉뚱/황당 (crazy)
      { text: "지구 평화를 위해 비밀 임무를 수행하느라 연락이 늦어졌습니다.", category: "crazy", tag: "#황당 #히어로" },
      { text: "오늘 운세에서 집 밖으로 나가면 대흉이라고 해서 침대에서 자숙 중입니다.", category: "crazy", tag: "#황당 #토속신앙" },
      { text: "평행세계의 내가 오늘 일을 다 끝냈다고 해서 쉬고 있었습니다.", category: "crazy", tag: "#황당 #SF영화" },
      { text: "외계인이 신호를 보내와서 그거 해석하느라 잠시 정신을 잃었습니다.", category: "crazy", tag: "#황당 #UFO" }
    ];

    let currentCategory = 'all';

    function setCategory(cat) {
      currentCategory = cat;
      const buttons = document.querySelectorAll('.tab-btn');
      buttons.forEach(btn => btn.classList.remove('active'));
      event.target.classList.add('active');
    }

    function generateExcuse() {
      let filtered = excuses;
      if (currentCategory !== 'all') {
        filtered = excuses.filter(e => e.category === currentCategory);
      }

      const randomIndex = Math.floor(Math.random() * filtered.length);
      const selected = filtered[randomIndex];

      const display = document.getElementById('excuseDisplay');
      const tag = document.getElementById('excuseTag');

      display.style.transform = 'scale(0.95)';
      setTimeout(() => {
        display.innerText = `"${selected.text}"`;
        tag.innerText = selected.tag;
        display.style.transform = 'scale(1)';
      }, 100);
    }

    function copyExcuse() {
      const text = document.getElementById('excuseDisplay').innerText;
      if (text.includes("버튼을 눌러보세요")) return;

      navigator.clipboard.writeText(text).then(() => {
        showToast();
      });
    }

    function showToast() {
      const toast = document.getElementById('toast');
      toast.classList.add('show');
      setTimeout(() => {
        toast.classList.remove('show');
      }, 2000);
    }
  </script>
</body>
</html>
