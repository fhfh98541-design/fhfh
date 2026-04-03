# fhfh

<div class="main-scroll-wrapper" id="scroll-area">
    <nav class="nav-bar">
        <a href="#process" class="nav-link">PROCESS</a> <a href="#price" class="nav-link">PRICE</a> <a href="#work" class="nav-link">WORK</a> <a href="#notice" class="nav-link">NOTICE</a> <a href="#order" class="nav-link active">ORDER</a>
    </nav>

    <div id="scrollHint" class="scroll-floating-hint hidden">
        <span>내용이 더 있어요! 아래로 스크롤</span>
        <span style="animation: bounce 1.2s infinite; display: inline-block;">↓</span>
    </div>

    <div class="container">
        <section id="process" class="visible">
            <h2>PROCESS</h2>
            <div class="process-container">
                <div class="process-step"><div class="step-num">01</div><div class="step-text">입금 확인</div></div>
                <div class="process-step"><div class="step-num">02</div><div class="step-text">작업 시작</div></div>
                <div class="process-step"><div class="step-num">03</div><div class="step-text">러프<div class="step-sub">컨펌 1회</div></div></div>
                <div class="process-step"><div class="step-num">04</div><div class="step-text">컬러 러프<div class="step-sub">컨펌 1회</div></div></div>
                <div class="process-step"><div class="step-num">05</div><div class="step-text">완성 후 조정<div class="step-sub">컨펌 1회</div></div></div>
                <div class="process-step"><div class="step-num">06</div><div class="step-text">최종 전달</div></div>
            </div>
        </section>

        <section id="price" class="visible">
            <h2>PRICE</h2>
            <div class="type-container">
                <div class="type-card"><div class="step-text">비상업용</div><div class="type-price">15.0 ~</div><div class="step-sub">개인 소장용</div></div>
                <div class="type-card"><div class="step-text">방송용</div><div class="type-price">25.0 ~</div><div class="step-sub">유튜브 / 방송화면</div></div>
                <div class="type-card"><div class="step-text">상업용</div><div class="type-price">60.0 ~</div><div class="step-sub">외부 수익 목적(문의)</div></div>
            </div>
        </section>

        <section id="work" class="visible">
            <h2>PORTFOLIO</h2>
            <div class="portfolio-grid">
                <div class="portfolio-item"><a href="1.jpg" target="_blank"><img src="1.jpg" alt="Work 1"></a></div>
                <div class="portfolio-item"><a href="2.png" target="_blank"><img src="2.png" alt="Work 2"></a></div>
                <div class="portfolio-item"><a href="3.png" target="_blank"><img src="3.png" alt="Work 3"></a></div>
                <div class="portfolio-item"><a href="4.png" target="_blank"><img src="4.png" alt="Work 4"></a></div>
                <div class="portfolio-item"><a href="5.png" target="_blank"><img src="5.png" alt="Work 5"></a></div>
                <div class="portfolio-item"><a href="6.png" target="_blank"><img src="6.png" alt="Work 6"></a></div>
            </div>
        </section>

        <section id="notice" class="visible">
            <h2>NOTICE</h2>
            <div class="notice-top-text">공지 미숙지로 인해 발생하는 문제에 대해서는<br>작가가 책임지지 않습니다.</div>
            <div class="notice-content">
                <div class="notice-box"><h4>GUIDE</h4><ul><li>상업용 외 저작권은 작가에게 귀속됩니다.</li><li>2차 가공 및 리터칭을 금지합니다.</li><li>모든 작품은 포트폴리오로 사용될 수 있습니다.</li></ul></div>
                <div class="notice-box"><h4>OPTION</h4><ul><li>복잡한 배경, 장신구, 소품 등 작업량에 따라 가격이 변동될 수 있습니다.</li><li>단순 변심으로 인한 이후 수정은 불가능 합니다.</li></ul></div>
            </div>
        </section>

        <section id="order" class="visible">
            <h2>ORDER FORM</h2>
            <p style="font-size: 0.8rem; color: var(--text-sub); text-align: center; margin-bottom: 10px; word-break: keep-all;">내용 작성 후 <b>[양식 복사하기]</b>를 눌러 문의창에 붙여넣어 주세요.</p>
            <div class="order-box">
                <div class="order-row"><label>신청 타입 / 범위</label><div style="display: flex; gap: 10px;"><select id="type" style="flex: 1;"><option>비상업</option><option>방송용</option><option>상업용</option></select><select id="range" style="flex: 1;"><option>흉상</option><option>반신</option><option>전신</option></select></div></div>
             
                <div style="display: flex; gap: 15px;" class="mobile-row">
                    <div class="order-row" style="flex: 1;"><label>신청자 닉네임</label><input type="text" id="nickname" placeholder="플랫폼 닉네임 등"></div>
                    <div class="order-row" style="flex: 1;"><label>사용 목적</label><input type="text" id="purpose" placeholder="ex) 유튜브 썸네일, 개인 소장 등"></div>
                </div>
                <div class="order-row"><label>캔버스 사이즈</label><input type="text" id="canvas" placeholder="ex) 1920 x 1080, 16:9 비율 등"></div>
                <div class="order-row"><label>캐릭터 자료</label><textarea id="details" rows="3" placeholder="외형, 설정 등(이미지 자료 필수!)"></textarea></div>
                <div class="order-row"><label>구도 및 포즈</label><textarea id="pose" rows="3" placeholder="원하시는 구도나 포즈를 적어주세요!"></textarea></div>
                <div class="order-row"><label>배경</label><textarea id="background" rows="3" placeholder="원하시는 배경 요소나 분위기를 적어주세요!"></textarea></div>
                <div class="order-row"><label>기타 문의사항</label><textarea id="etc" rows="3" placeholder="기타 궁금하신 점이나 요청사항을 적어주세요!"></textarea></div>
                <button id="copyBtn" class="copy-btn">양식 복사하기</button>
            </div>
        </section>
    </div>
</div>
