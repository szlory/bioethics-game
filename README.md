# bioethics-game
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <title>💊 당신의 선택은? - 3억짜리 바이오의약품</title>
  <style>
    body {
      font-family: "Arial", sans-serif;
      padding: 30px;
      background-color: #f4f4f4;
    }
    .patient {
      background: white;
      padding: 15px;
      margin: 10px 0;
      border-left: 5px solid #007acc;
    }
    button {
      margin-top: 10px;
      padding: 8px 15px;
      font-size: 14px;
    }
    #reasonBox, #result, #bioInfo {
      margin-top: 30px;
      padding: 15px;
      background: #e3f2fd;
      border: 1px solid #90caf9;
      border-radius: 8px;
    }
  </style>
</head>
<body>

  <h1>💊 당신의 선택은? - 3억짜리 바이오의약품</h1>
  <p>치료 자원이 한 명에게만 주어진다면, 당신은 누구를 선택하시겠습니까?</p>

  <div id="patients">
    <div class="patient">
      <strong>A. 65세 치매 초기 환자</strong><br>
      손자는 매일 편지를 써주며 함께 살고 싶어합니다. 가족은 가난하지만 치료를 원합니다.<br>
      <em>✔ 완치율: 95%</em><br>
      <q>가끔 이름은 잊어도…. 손자의 웃음만은 아직, 내 마음이 기억합니다.</q><br>
      <button onclick="selectPatient('A')">A 선택</button>
    </div>

    <div class="patient">
      <strong>B. 40세 암환자 (세 아이의 아버지)</strong><br>
      가족 생계를 홀로 책임지고 있으며, 회복 가능성 80%입니다.<br>
      <q>아이들은 제가 없으면 돌볼 사람이 없어요.. 아이들 졸업까진 보고 싶어요</q><br>
      <button onclick="selectPatient('B')">B 선택</button>
    </div>

    <div class="patient">
      <strong>C. 19세 희귀병 환자</strong><br>
      대학 입시 앞두고 있으며 치료 시 정상 생활 가능.<br>
      <q>저도 대학교 가서 친구들과 캠퍼스 생활을 즐기고 싶어요</q><br>
      <button onclick="selectPatient('C')">C 선택</button>
    </div>

    <div class="patient">
      <strong>D. 5세 파킨슨병 남아</strong><br>
      치료 가능성은 50%, 복지 사각지대에 있음.<br>
      <q>병원 말고… 진짜 우리 집에서, 엄마 아빠랑 같이 자면 안 돼요?</q><br>
      <button onclick="selectPatient('D')">D 선택</button>
    </div>

    <div class="patient">
      <strong>E. 결혼을 앞둔 28세 신부</strong><br>
      치료 가능성 40%, 복지 사각지대. 손끝이 점점 굳어가는 중.<br>
      <q>결혼하면 같이 여행도 가고, 아이도 낳고… 그날 반지나 제대로 끼울 수 있을까 그게 걱정이에요.</q><br>
      <button onclick="selectPatient('E')">E 선택</button>
    </div>
  </div>

  <div id="reasonBox" style="display:none;">
    <h3>선택 이유를 작성해주세요</h3>
    <textarea id="reasonInput" rows="4" cols="50" placeholder="왜 이 사람을 선택했나요?"></textarea><br>
    <button onclick="submitReason()">제출하기</button>
  </div>

  <div id="result" style="display:none;"></div>
  <div id="bioInfo" style="display:none;"></div>

  <script>
    let stats = { A: 0, B: 0, C: 0, D: 0, E: 0 };
    let selectedPatient = "";

    function selectPatient(id) {
      selectedPatient = id;
      document.getElementById("reasonBox").style.display = "block";
    }

    function submitReason() {
      stats[selectedPatient]++;
      const reason = document.getElementById("reasonInput").value;

      const bioMap = {
        A: `
          <h3>🧬 관련 생명공학 기술</h3>
          <p>치매 치료에는 아두카누맙(Aducanumab) 같은 항체 기반 치료제가 사용됩니다.  
          알츠하이머를 타겟으로 한 단백질 응집 억제 연구도 활발히 진행되고 있습니다.</p>
        `,
        B: `
          <h3>🧬 관련 생명공학 기술</h3>
          <p>암환자의 경우 CAR-T 세포 치료, 면역관문 억제제, 암백신 등의 면역항암제가 주요 치료 기술로 활용됩니다.</p>
        `,
        C: `
          <h3>🧬 관련 생명공학 기술</h3>
          <p>희귀 유전질환에는 mRNA 치료제, 유전자 편집(CRISPR), 항센스 올리고(Antisense Oligo) 등이 적용됩니다.</p>
        `,
        D: `
          <h3>🧬 관련 생명공학 기술</h3>
          <p>파킨슨병 치료를 위해 도파민 뉴런을 유도하는 줄기세포 치료, 뇌심부자극(DBS) 기술이 연구되고 있습니다.</p>
        `,
        E: `
          <h3>🧬 관련 생명공학 기술</h3>
          <p>자가면역 질환 완화 및 염증 조절을 위한 바이오의약품(항체제제)과 이를 대체할 바이오시밀러 개발이 활발합니다.</p>
        `
      };

      const drugPriceInfo = `
        <h3>💰 고가의약품의 현실</h3>
        <p>이러한 생명공학 치료제는 평균 수억 원에 달하는 고가의약품입니다.  
        복잡한 세포/유전자 기반 제조 공정과 연구개발비가 반영되기 때문입니다.</p>
      `;

      const biosimilarInfo = `
        <h3>💡 해결책: 바이오시밀러</h3>
        <p>바이오시밀러는 기존 바이오의약품과 유사한 효능을 가진 복제약으로,  
        가격은 대폭 낮지만 효과는 거의 동일합니다.  
        정부와 기업이 바이오시밀러 개발을 촉진하면 치료 접근성을 높일 수 있습니다.</p>
      `;

      const fullResult = `
        <h3>✔ 당신의 선택: ${selectedPatient}</h3>
        <p><strong>선택 이유:</strong> ${reason}</p>
        <p><strong>전체 통계:</strong> A: ${stats.A}, B: ${stats.B}, C: ${stats.C}, D: ${stats.D}, E: ${stats.E}</p>
      `;
      document.getElementById("result").innerHTML = fullResult;
      document.getElementById("result").style.display = "block";

      const fullInfo = bioMap[selectedPatient] + drugPriceInfo + biosimilarInfo;
      document.getElementById("bioInfo").innerHTML = fullInfo;
      document.getElementById("bioInfo").style.display = "block";
    }
  </script>

</body>
</html>