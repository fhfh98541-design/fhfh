<html lang="ko"><head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Illustrator Commission</title>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700&amp;display=swap" rel="stylesheet">
    <style>
        /* [기본 설정] */
        html, body { margin: 0; padding: 0; height: 100%; overflow: auto; background-color: #fffcf9; font-family: 'Noto Sans KR', sans-serif; }
        .main-scroll-wrapper { width: 100%; height: 100vh; overflow-y: auto; -webkit-overflow-scrolling: touch; display: flex; flex-direction: column; align-items: center; position: relative; }
        html { scroll-behavior: smooth; }
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: #fdf6f6; }
        ::-webkit-scrollbar-thumb { background: #ff8e8e; border-radius: 10px; }

        :root { --main-coral: #ff8e8e; --card-bg: #ffffff; --text-main: #444444; --text-sub: #777777; --border-radius: 24px; --soft-shadow: 0 10px 40px rgba(255, 142, 142, 0.1); }
        
        .container { width: 100%; max-width: 850px; display: flex; flex-direction: column; gap: 40px; padding: 100px 20px 60px 20px; box-sizing: border-box; }

        /* [플로팅 스크롤 안내 바] */
        .scroll-floating-hint {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            background: var(--main-coral);
            color: white;
            padding: 12px 25px;
            border-radius: 50px;
            font-size: 0.85rem;
            font-weight: 700;
            box-shadow: 0 8px 25px rgba(255, 142, 142, 0.4);
            z-index: 2000;
            display: flex;
            align-items: center;
            gap: 10px;
            transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
            pointer-events: none;
        }

        .scroll-floating-hint.hidden {
            opacity: 0;
            transform: translateX(-50%) translateY(20px);
            visibility: hidden;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(4px); }
        }

        section { background: var(--card-bg); padding: 50px; border-radius: var(--border-radius); box-shadow: var(--soft-shadow); scroll-margin-top: 120px; opacity: 0; transform: translateY(20px); transition: 0.8s ease-out; }
        section.visible { opacity: 1; transform: translateY(0); }

        /* [네비게이션] */
        .nav-bar { position: fixed; top: 20px; left: 50%; transform: translateX(-50%); background: rgba(255, 255, 255, 0.75); backdrop-filter: blur(15px); padding: 10px 30px; border-radius: 50px; box-shadow: var(--soft-shadow); display: flex; gap: 20px; z-index: 1000; border: 1px solid rgba(255, 255, 255, 0.5); }
        .nav-bar a { text-decoration: none; color: var(--text-main); font-size: 0.8rem; font-weight: 600; opacity: 0.6; transition: 0.3s; padding: 5px 10px; border-radius: 20px; }
        .nav-bar a.active { opacity: 1; color: var(--main-coral); background: rgba(255, 142, 142, 0.1); }

        h2 { font-size: 1.6rem; margin-bottom: 40px; text-align: center; color: var(--main-coral); letter-spacing: 0.15em; font-weight: 700; }
        #notice h2, #order h2 { margin-bottom: 15px !important; }

        /* [PROCESS] */
        .process-container { display: flex; align-items: flex-start; justify-content: space-between; width: 100%; position: relative; box-sizing: border-box; padding: 0 10px; }
        .process-container::before { content: ''; position: absolute; top: 14px; left: calc(100% / 12); right: calc(100% / 12); height: 2px; background: #ffe5e5; z-index: 0; }
        .process-step { position: relative; z-index: 1; display: flex; flex-direction: column; align-items: center; text-align: center; flex: 1; }
        .step-num { width: 28px; height: 28px; background: var(--main-coral); color: white; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 0.75rem; font-weight: 700; margin-bottom: 15px; box-shadow: 0 4px 10px rgba(255, 142, 142, 0.3); border: 3px solid #fff; }
        .step-text { font-size: 0.85rem; font-weight: 700; color: var(--text-main); word-break: keep-all; }
        .step-sub { font-size: 0.7rem; color: var(--text-sub); margin-top: 2px; white-space: nowrap; }

        /* [PRICE] */
        .type-container { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; }
        .type-card { background: #fff5f5; padding: 35px 20px; border-radius: 20px; display: flex; flex-direction: column; align-items: center; text-align: center; transition: 0.3s; border: 1px solid transparent; }
        .type-price { font-size: 1.4rem; font-weight: 700; color: var(--main-coral); margin: 2px 0; line-height: 1.2; }

        /* [PORTFOLIO] */
        .portfolio-grid { column-count: 2; column-gap: 20px; }
        .portfolio-item { position: relative; break-inside: avoid; margin-bottom: 20px; border-radius: 16px; overflow: hidden; background: #000; }
        .portfolio-item img { width: 100%; display: block; transition: 0.5s; height: auto; }

        /* [NOTICE / ORDER] */
        .notice-top-text { text-align: center; font-size: 0.9rem; font-weight: 700; color: #222; border-bottom: 1px solid #eee; padding-bottom: 20px; margin-bottom: 25px; line-height: 1.6; word-break: keep-all; overflow-wrap: break-word; }
        .notice-content { display: grid; grid-template-columns: 1fr 1fr; gap: 30px; font-size: 0.9rem; }
        .notice-box h4 { color: var(--main-coral); margin-bottom: 15px; font-size: 1.1rem; border-left: 4px solid var(--main-coral); padding-left: 10px; }
        .notice-box ul { padding-left: 18px; color: var(--text-sub); line-height: 1.8; list-style-type: none; }
        .notice-box li::before { content: "•"; color: var(--main-coral); font-weight: bold; display: inline-block; width: 1em; margin-left: -1em; }
        
        .order-box { display: flex; flex-direction: column; gap: 18px; }
        .order-row { display: flex; flex-direction: column; gap: 8px; }
        .order-row label { font-size: 0.85rem; font-weight: 600; color: var(--text-main); }
        .order-box input, .order-box select, .order-box textarea { width: 100%; padding: 14px; border: 1px solid #eee; border-radius: 12px; background: #fafafa; font-family: inherit; font-size: 0.9rem; box-sizing: border-box; outline: none; transition: 0.3s; }
        .order-box input:focus, .order-box select:focus, .order-box textarea:focus { border-color: var(--main-coral); background: #fff; box-shadow: 0 0 0 4px rgba(255, 142, 142, 0.1); }
        
        .copy-btn { background: var(--main-coral); color: white; border: none; padding: 18px; border-radius: 14px; font-weight: 700; cursor: pointer; transition: 0.2s; margin-top: 10px; font-size: 1rem; }
        .copy-btn.active-state { background: #ff9e9e; transform: scale(0.98); }

        @media (max-width: 650px) {
            .nav-bar { width: 92%; padding: 8px 5px; gap: 2px; top: 15px; left: 50%; transform: translateX(-50%); display: flex; justify-content: center; box-sizing: border-box; }
            .nav-bar a { font-size: 0.7rem; padding: 4px 6px; flex-shrink: 0; }
            .container { padding-top: 80px; }
            .process-container { flex-direction: column; align-items: flex-start; gap: 35px; padding-left: 15px; }
            .process-container::before { left: 28px; top: 10px; bottom: 10px; width: 2px; height: auto; display: block; }
            .process-step { flex-direction: row; text-align: left; gap: 20px; width: 100%; justify-content: flex-start; }
            .step-num { margin-bottom: 0; flex-shrink: 0; }
            .portfolio-grid { column-count: 1; }
            .type-container, .notice-content { grid-template-columns: 1fr; }
            section { padding: 30px 20px; }
            .mobile-row { flex-direction: column !important; }
        }
    </style>
</head>
<body>
<div class="main-scroll-wrapper" id="scroll-area">
    <nav class="nav-bar">
        <a href="#process" class="nav-link active">PROCESS</a> <a href="#price" class="nav-link">PRICE</a> <a href="#work" class="nav-link">WORK</a> <a href="#notice" class="nav-link">NOTICE</a> <a href="#order" class="nav-link">ORDER</a>
    </nav>

    <div id="scrollHint" class="scroll-floating-hint">
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

<script>
    document.addEventListener('DOMContentLoaded', function() {
        const btn = document.getElementById('copyBtn');
        const scrollArea = document.getElementById('scroll-area');
        const hint = document.getElementById('scrollHint');
        const sections = document.querySelectorAll('section');
        const navLinks = document.querySelectorAll('.nav-bar a');

        // 복사 기능
        if (btn) {
            btn.addEventListener('click', function() {
                const f = (id) => document.getElementById(id).value;
  const text = `[Commission Form]\n- 신청 타입: ${f('type')}\n- 캐릭터 범위: ${f('range')}\n- 닉네임: ${f('nickname')}\n- 사용 목적: ${f('purpose')}\n- 캔버스 사이즈: ${f('canvas')}\n- 캐릭터 자료: ${f('details')}\n- 구도 및 포즈: ${f('pose')}\n- 배경: ${f('background')}\n- 기타 문의사항: ${f('etc')}\n\n* 모든 사항은 이미지 자료가 있으면 더 정확한 작업이 가능합니다!`;
                const textArea = document.createElement("textarea");
                textArea.value = text;
                textArea.style.position = "fixed";
                textArea.style.left = "-9999px";
                textArea.style.top = "0";
                textArea.setAttribute('readonly', '');
                document.body.appendChild(textArea);
                textArea.focus();
                textArea.select();
                textArea.setSelectionRange(0, 99999);
                try {
                    document.execCommand('copy');
                    const originalText = btn.innerText; 
                    btn.innerText = "복사 완료!"; 
                    btn.classList.add('active-state');
                    setTimeout(() => { 
                        btn.innerText = originalText; 
                        btn.classList.remove('active-state'); 
                    }, 1000);
                } catch (err) {}
                document.body.removeChild(textArea);
            });
        }

        // 스크롤 이벤트 통합
        scrollArea.addEventListener('scroll', () => {
            // 1. 안내 힌트 숨기기
            if (scrollArea.scrollTop > 50) {
                hint.classList.add('hidden');
            } else {
                hint.classList.remove('hidden');
            }

            // 2. 섹션 등장 애니메이션 및 네비 활성화
            let current = "";
            sections.forEach(section => {
                const sectionTop = section.offsetTop;
                if (scrollArea.scrollTop > sectionTop - scrollArea.offsetHeight * 0.85) section.classList.add('visible');
                if (scrollArea.scrollTop >= sectionTop - 150) current = section.getAttribute('id');
            });
            navLinks.forEach(link => {
                link.classList.remove('active');
                if (link.getAttribute('href').includes(current)) link.classList.add('active');
            });
        });

        // 네비 클릭 스무스 스크롤
        navLinks.forEach(anchor => {
            anchor.addEventListener('click', function(e) {
                e.preventDefault(); 
                const targetId = this.getAttribute('href');
                const targetElement = document.querySelector(targetId);
                if (targetElement && scrollArea) {
                    const targetOffset = targetElement.offsetTop - 100; 
                    scrollArea.scrollTo({ top: targetOffset, behavior: 'smooth' });
                }
            });
        });
    });

    window.onload = () => { 
        const sections = document.querySelectorAll('section');
        if(sections[0]) sections[0].classList.add('visible'); 
    };
</script>


</body></html>

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Illustrator Commission</title>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700&amp;display=swap" rel="stylesheet">
    <style>
        /* [기본 설정] */
        html, body { margin: 0; padding: 0; height: 100%; overflow: auto; background-color: #fffcf9; font-family: 'Noto Sans KR', sans-serif; }
        .main-scroll-wrapper { width: 100%; height: 100vh; overflow-y: auto; -webkit-overflow-scrolling: touch; display: flex; flex-direction: column; align-items: center; position: relative; }
        html { scroll-behavior: smooth; }
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: #fdf6f6; }
        ::-webkit-scrollbar-thumb { background: #ff8e8e; border-radius: 10px; }

        :root { --main-coral: #ff8e8e; --card-bg: #ffffff; --text-main: #444444; --text-sub: #777777; --border-radius: 24px; --soft-shadow: 0 10px 40px rgba(255, 142, 142, 0.1); }
        
        .container { width: 100%; max-width: 850px; display: flex; flex-direction: column; gap: 40px; padding: 100px 20px 60px 20px; box-sizing: border-box; }

        /* [플로팅 스크롤 안내 바] */
        .scroll-floating-hint {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            background: var(--main-coral);
            color: white;
            padding: 12px 25px;
            border-radius: 50px;
            font-size: 0.85rem;
            font-weight: 700;
            box-shadow: 0 8px 25px rgba(255, 142, 142, 0.4);
            z-index: 2000;
            display: flex;
            align-items: center;
            gap: 10px;
            transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
            pointer-events: none;
        }

        .scroll-floating-hint.hidden {
            opacity: 0;
            transform: translateX(-50%) translateY(20px);
            visibility: hidden;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(4px); }
        }

        section { background: var(--card-bg); padding: 50px; border-radius: var(--border-radius); box-shadow: var(--soft-shadow); scroll-margin-top: 120px; opacity: 0; transform: translateY(20px); transition: 0.8s ease-out; }
        section.visible { opacity: 1; transform: translateY(0); }

        /* [네비게이션] */
        .nav-bar { position: fixed; top: 20px; left: 50%; transform: translateX(-50%); background: rgba(255, 255, 255, 0.75); backdrop-filter: blur(15px); padding: 10px 30px; border-radius: 50px; box-shadow: var(--soft-shadow); display: flex; gap: 20px; z-index: 1000; border: 1px solid rgba(255, 255, 255, 0.5); }
        .nav-bar a { text-decoration: none; color: var(--text-main); font-size: 0.8rem; font-weight: 600; opacity: 0.6; transition: 0.3s; padding: 5px 10px; border-radius: 20px; }
        .nav-bar a.active { opacity: 1; color: var(--main-coral); background: rgba(255, 142, 142, 0.1); }

        h2 { font-size: 1.6rem; margin-bottom: 40px; text-align: center; color: var(--main-coral); letter-spacing: 0.15em; font-weight: 700; }
        #notice h2, #order h2 { margin-bottom: 15px !important; }

        /* [PROCESS] */
        .process-container { display: flex; align-items: flex-start; justify-content: space-between; width: 100%; position: relative; box-sizing: border-box; padding: 0 10px; }
        .process-container::before { content: ''; position: absolute; top: 14px; left: calc(100% / 12); right: calc(100% / 12); height: 2px; background: #ffe5e5; z-index: 0; }
        .process-step { position: relative; z-index: 1; display: flex; flex-direction: column; align-items: center; text-align: center; flex: 1; }
        .step-num { width: 28px; height: 28px; background: var(--main-coral); color: white; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 0.75rem; font-weight: 700; margin-bottom: 15px; box-shadow: 0 4px 10px rgba(255, 142, 142, 0.3); border: 3px solid #fff; }
        .step-text { font-size: 0.85rem; font-weight: 700; color: var(--text-main); word-break: keep-all; }
        .step-sub { font-size: 0.7rem; color: var(--text-sub); margin-top: 2px; white-space: nowrap; }

        /* [PRICE] */
        .type-container { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; }
        .type-card { background: #fff5f5; padding: 35px 20px; border-radius: 20px; display: flex; flex-direction: column; align-items: center; text-align: center; transition: 0.3s; border: 1px solid transparent; }
        .type-price { font-size: 1.4rem; font-weight: 700; color: var(--main-coral); margin: 2px 0; line-height: 1.2; }

        /* [PORTFOLIO] */
        .portfolio-grid { column-count: 2; column-gap: 20px; }
        .portfolio-item { position: relative; break-inside: avoid; margin-bottom: 20px; border-radius: 16px; overflow: hidden; background: #000; }
        .portfolio-item img { width: 100%; display: block; transition: 0.5s; height: auto; }

        /* [NOTICE / ORDER] */
        .notice-top-text { text-align: center; font-size: 0.9rem; font-weight: 700; color: #222; border-bottom: 1px solid #eee; padding-bottom: 20px; margin-bottom: 25px; line-height: 1.6; word-break: keep-all; overflow-wrap: break-word; }
        .notice-content { display: grid; grid-template-columns: 1fr 1fr; gap: 30px; font-size: 0.9rem; }
        .notice-box h4 { color: var(--main-coral); margin-bottom: 15px; font-size: 1.1rem; border-left: 4px solid var(--main-coral); padding-left: 10px; }
        .notice-box ul { padding-left: 18px; color: var(--text-sub); line-height: 1.8; list-style-type: none; }
        .notice-box li::before { content: "•"; color: var(--main-coral); font-weight: bold; display: inline-block; width: 1em; margin-left: -1em; }
        
        .order-box { display: flex; flex-direction: column; gap: 18px; }
        .order-row { display: flex; flex-direction: column; gap: 8px; }
        .order-row label { font-size: 0.85rem; font-weight: 600; color: var(--text-main); }
        .order-box input, .order-box select, .order-box textarea { width: 100%; padding: 14px; border: 1px solid #eee; border-radius: 12px; background: #fafafa; font-family: inherit; font-size: 0.9rem; box-sizing: border-box; outline: none; transition: 0.3s; }
        .order-box input:focus, .order-box select:focus, .order-box textarea:focus { border-color: var(--main-coral); background: #fff; box-shadow: 0 0 0 4px rgba(255, 142, 142, 0.1); }
        
        .copy-btn { background: var(--main-coral); color: white; border: none; padding: 18px; border-radius: 14px; font-weight: 700; cursor: pointer; transition: 0.2s; margin-top: 10px; font-size: 1rem; }
        .copy-btn.active-state { background: #ff9e9e; transform: scale(0.98); }

        @media (max-width: 650px) {
            .nav-bar { width: 92%; padding: 8px 5px; gap: 2px; top: 15px; left: 50%; transform: translateX(-50%); display: flex; justify-content: center; box-sizing: border-box; }
            .nav-bar a { font-size: 0.7rem; padding: 4px 6px; flex-shrink: 0; }
            .container { padding-top: 80px; }
            .process-container { flex-direction: column; align-items: flex-start; gap: 35px; padding-left: 15px; }
            .process-container::before { left: 28px; top: 10px; bottom: 10px; width: 2px; height: auto; display: block; }
            .process-step { flex-direction: row; text-align: left; gap: 20px; width: 100%; justify-content: flex-start; }
            .step-num { margin-bottom: 0; flex-shrink: 0; }
            .portfolio-grid { column-count: 1; }
            .type-container, .notice-content { grid-template-columns: 1fr; }
            section { padding: 30px 20px; }
            .mobile-row { flex-direction: column !important; }
        }
    </style>
</head>
<body>
<div class="main-scroll-wrapper" id="scroll-area">
    <nav class="nav-bar">
        <a href="#process" class="nav-link active">PROCESS</a> <a href="#price" class="nav-link">PRICE</a> <a href="#work" class="nav-link">WORK</a> <a href="#notice" class="nav-link">NOTICE</a> <a href="#order" class="nav-link">ORDER</a>
    </nav>

    <div id="scrollHint" class="scroll-floating-hint">
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

<script>
    document.addEventListener('DOMContentLoaded', function() {
        const btn = document.getElementById('copyBtn');
        const scrollArea = document.getElementById('scroll-area');
        const hint = document.getElementById('scrollHint');
        const sections = document.querySelectorAll('section');
        const navLinks = document.querySelectorAll('.nav-bar a');

        // 복사 기능
        if (btn) {
            btn.addEventListener('click', function() {
                const f = (id) => document.getElementById(id).value;
  const text = `[Commission Form]\n- 신청 타입: ${f('type')}\n- 캐릭터 범위: ${f('range')}\n- 닉네임: ${f('nickname')}\n- 사용 목적: ${f('purpose')}\n- 캔버스 사이즈: ${f('canvas')}\n- 캐릭터 자료: ${f('details')}\n- 구도 및 포즈: ${f('pose')}\n- 배경: ${f('background')}\n- 기타 문의사항: ${f('etc')}\n\n* 모든 사항은 이미지 자료가 있으면 더 정확한 작업이 가능합니다!`;
                const textArea = document.createElement("textarea");
                textArea.value = text;
                textArea.style.position = "fixed";
                textArea.style.left = "-9999px";
                textArea.style.top = "0";
                textArea.setAttribute('readonly', '');
                document.body.appendChild(textArea);
                textArea.focus();
                textArea.select();
                textArea.setSelectionRange(0, 99999);
                try {
                    document.execCommand('copy');
                    const originalText = btn.innerText; 
                    btn.innerText = "복사 완료!"; 
                    btn.classList.add('active-state');
                    setTimeout(() => { 
                        btn.innerText = originalText; 
                        btn.classList.remove('active-state'); 
                    }, 1000);
                } catch (err) {}
                document.body.removeChild(textArea);
            });
        }

        // 스크롤 이벤트 통합
        scrollArea.addEventListener('scroll', () => {
            // 1. 안내 힌트 숨기기
            if (scrollArea.scrollTop > 50) {
                hint.classList.add('hidden');
            } else {
                hint.classList.remove('hidden');
            }

            // 2. 섹션 등장 애니메이션 및 네비 활성화
            let current = "";
            sections.forEach(section => {
                const sectionTop = section.offsetTop;
                if (scrollArea.scrollTop > sectionTop - scrollArea.offsetHeight * 0.85) section.classList.add('visible');
                if (scrollArea.scrollTop >= sectionTop - 150) current = section.getAttribute('id');
            });
            navLinks.forEach(link => {
                link.classList.remove('active');
                if (link.getAttribute('href').includes(current)) link.classList.add('active');
            });
        });

        // 네비 클릭 스무스 스크롤
        navLinks.forEach(anchor => {
            anchor.addEventListener('click', function(e) {
                e.preventDefault(); 
                const targetId = this.getAttribute('href');
                const targetElement = document.querySelector(targetId);
                if (targetElement && scrollArea) {
                    const targetOffset = targetElement.offsetTop - 100; 
                    scrollArea.scrollTo({ top: targetOffset, behavior: 'smooth' });
                }
            });
        });
    });

    window.onload = () => { 
        const sections = document.querySelectorAll('section');
        if(sections[0]) sections[0].classList.add('visible'); 
    };
</script>


</body>
<div class="main-scroll-wrapper" id="scroll-area">
    <nav class="nav-bar">
        <a href="#process" class="nav-link active">PROCESS</a> <a href="#price" class="nav-link">PRICE</a> <a href="#work" class="nav-link">WORK</a> <a href="#notice" class="nav-link">NOTICE</a> <a href="#order" class="nav-link">ORDER</a>
    </nav>

    <div id="scrollHint" class="scroll-floating-hint">
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
<script>
    document.addEventListener('DOMContentLoaded', function() {
        const btn = document.getElementById('copyBtn');
        const scrollArea = document.getElementById('scroll-area');
        const hint = document.getElementById('scrollHint');
        const sections = document.querySelectorAll('section');
        const navLinks = document.querySelectorAll('.nav-bar a');

        // 복사 기능
        if (btn) {
            btn.addEventListener('click', function() {
                const f = (id) => document.getElementById(id).value;
  const text = `[Commission Form]\n- 신청 타입: ${f('type')}\n- 캐릭터 범위: ${f('range')}\n- 닉네임: ${f('nickname')}\n- 사용 목적: ${f('purpose')}\n- 캔버스 사이즈: ${f('canvas')}\n- 캐릭터 자료: ${f('details')}\n- 구도 및 포즈: ${f('pose')}\n- 배경: ${f('background')}\n- 기타 문의사항: ${f('etc')}\n\n* 모든 사항은 이미지 자료가 있으면 더 정확한 작업이 가능합니다!`;
                const textArea = document.createElement("textarea");
                textArea.value = text;
                textArea.style.position = "fixed";
                textArea.style.left = "-9999px";
                textArea.style.top = "0";
                textArea.setAttribute('readonly', '');
                document.body.appendChild(textArea);
                textArea.focus();
                textArea.select();
                textArea.setSelectionRange(0, 99999);
                try {
                    document.execCommand('copy');
                    const originalText = btn.innerText; 
                    btn.innerText = "복사 완료!"; 
                    btn.classList.add('active-state');
                    setTimeout(() => { 
                        btn.innerText = originalText; 
                        btn.classList.remove('active-state'); 
                    }, 1000);
                } catch (err) {}
                document.body.removeChild(textArea);
            });
        }

        // 스크롤 이벤트 통합
        scrollArea.addEventListener('scroll', () => {
            // 1. 안내 힌트 숨기기
            if (scrollArea.scrollTop > 50) {
                hint.classList.add('hidden');
            } else {
                hint.classList.remove('hidden');
            }

            // 2. 섹션 등장 애니메이션 및 네비 활성화
            let current = "";
            sections.forEach(section => {
                const sectionTop = section.offsetTop;
                if (scrollArea.scrollTop > sectionTop - scrollArea.offsetHeight * 0.85) section.classList.add('visible');
                if (scrollArea.scrollTop >= sectionTop - 150) current = section.getAttribute('id');
            });
            navLinks.forEach(link => {
                link.classList.remove('active');
                if (link.getAttribute('href').includes(current)) link.classList.add('active');
            });
        });

        // 네비 클릭 스무스 스크롤
        navLinks.forEach(anchor => {
            anchor.addEventListener('click', function(e) {
                e.preventDefault(); 
                const targetId = this.getAttribute('href');
                const targetElement = document.querySelector(targetId);
                if (targetElement && scrollArea) {
                    const targetOffset = targetElement.offsetTop - 100; 
                    scrollArea.scrollTo({ top: targetOffset, behavior: 'smooth' });
                }
            });
        });
    });

    window.onload = () => { 
        const sections = document.querySelectorAll('section');
        if(sections[0]) sections[0].classList.add('visible'); 
    };
</script>
<body>
<div class="main-scroll-wrapper" id="scroll-area">
    <nav class="nav-bar">
        <a href="#process" class="nav-link active">PROCESS</a> <a href="#price" class="nav-link">PRICE</a> <a href="#work" class="nav-link">WORK</a> <a href="#notice" class="nav-link">NOTICE</a> <a href="#order" class="nav-link">ORDER</a>
    </nav>

    <div id="scrollHint" class="scroll-floating-hint">
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

<script>
    document.addEventListener('DOMContentLoaded', function() {
        const btn = document.getElementById('copyBtn');
        const scrollArea = document.getElementById('scroll-area');
        const hint = document.getElementById('scrollHint');
        const sections = document.querySelectorAll('section');
        const navLinks = document.querySelectorAll('.nav-bar a');

        // 복사 기능
        if (btn) {
            btn.addEventListener('click', function() {
                const f = (id) => document.getElementById(id).value;
  const text = `[Commission Form]\n- 신청 타입: ${f('type')}\n- 캐릭터 범위: ${f('range')}\n- 닉네임: ${f('nickname')}\n- 사용 목적: ${f('purpose')}\n- 캔버스 사이즈: ${f('canvas')}\n- 캐릭터 자료: ${f('details')}\n- 구도 및 포즈: ${f('pose')}\n- 배경: ${f('background')}\n- 기타 문의사항: ${f('etc')}\n\n* 모든 사항은 이미지 자료가 있으면 더 정확한 작업이 가능합니다!`;
                const textArea = document.createElement("textarea");
                textArea.value = text;
                textArea.style.position = "fixed";
                textArea.style.left = "-9999px";
                textArea.style.top = "0";
                textArea.setAttribute('readonly', '');
                document.body.appendChild(textArea);
                textArea.focus();
                textArea.select();
                textArea.setSelectionRange(0, 99999);
                try {
                    document.execCommand('copy');
                    const originalText = btn.innerText; 
                    btn.innerText = "복사 완료!"; 
                    btn.classList.add('active-state');
                    setTimeout(() => { 
                        btn.innerText = originalText; 
                        btn.classList.remove('active-state'); 
                    }, 1000);
                } catch (err) {}
                document.body.removeChild(textArea);
            });
        }

        // 스크롤 이벤트 통합
        scrollArea.addEventListener('scroll', () => {
            // 1. 안내 힌트 숨기기
            if (scrollArea.scrollTop > 50) {
                hint.classList.add('hidden');
            } else {
                hint.classList.remove('hidden');
            }

            // 2. 섹션 등장 애니메이션 및 네비 활성화
            let current = "";
            sections.forEach(section => {
                const sectionTop = section.offsetTop;
                if (scrollArea.scrollTop > sectionTop - scrollArea.offsetHeight * 0.85) section.classList.add('visible');
                if (scrollArea.scrollTop >= sectionTop - 150) current = section.getAttribute('id');
            });
            navLinks.forEach(link => {
                link.classList.remove('active');
                if (link.getAttribute('href').includes(current)) link.classList.add('active');
            });
        });

        // 네비 클릭 스무스 스크롤
        navLinks.forEach(anchor => {
            anchor.addEventListener('click', function(e) {
                e.preventDefault(); 
                const targetId = this.getAttribute('href');
                const targetElement = document.querySelector(targetId);
                if (targetElement && scrollArea) {
                    const targetOffset = targetElement.offsetTop - 100; 
                    scrollArea.scrollTo({ top: targetOffset, behavior: 'smooth' });
                }
            });
        });
    });

    window.onload = () => { 
        const sections = document.querySelectorAll('section');
        if(sections[0]) sections[0].classList.add('visible'); 
    };
</script>


</body>
<html lang="ko"><head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Illustrator Commission</title>
    <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+KR:wght@300;400;500;700&amp;display=swap" rel="stylesheet">
    <style>
        /* [기본 설정] */
        html, body { margin: 0; padding: 0; height: 100%; overflow: auto; background-color: #fffcf9; font-family: 'Noto Sans KR', sans-serif; }
        .main-scroll-wrapper { width: 100%; height: 100vh; overflow-y: auto; -webkit-overflow-scrolling: touch; display: flex; flex-direction: column; align-items: center; position: relative; }
        html { scroll-behavior: smooth; }
        ::-webkit-scrollbar { width: 6px; }
        ::-webkit-scrollbar-track { background: #fdf6f6; }
        ::-webkit-scrollbar-thumb { background: #ff8e8e; border-radius: 10px; }

        :root { --main-coral: #ff8e8e; --card-bg: #ffffff; --text-main: #444444; --text-sub: #777777; --border-radius: 24px; --soft-shadow: 0 10px 40px rgba(255, 142, 142, 0.1); }
        
        .container { width: 100%; max-width: 850px; display: flex; flex-direction: column; gap: 40px; padding: 100px 20px 60px 20px; box-sizing: border-box; }

        /* [플로팅 스크롤 안내 바] */
        .scroll-floating-hint {
            position: fixed;
            bottom: 30px;
            left: 50%;
            transform: translateX(-50%);
            background: var(--main-coral);
            color: white;
            padding: 12px 25px;
            border-radius: 50px;
            font-size: 0.85rem;
            font-weight: 700;
            box-shadow: 0 8px 25px rgba(255, 142, 142, 0.4);
            z-index: 2000;
            display: flex;
            align-items: center;
            gap: 10px;
            transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
            pointer-events: none;
        }

        .scroll-floating-hint.hidden {
            opacity: 0;
            transform: translateX(-50%) translateY(20px);
            visibility: hidden;
        }

        @keyframes bounce {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(4px); }
        }

        section { background: var(--card-bg); padding: 50px; border-radius: var(--border-radius); box-shadow: var(--soft-shadow); scroll-margin-top: 120px; opacity: 0; transform: translateY(20px); transition: 0.8s ease-out; }
        section.visible { opacity: 1; transform: translateY(0); }

        /* [네비게이션] */
        .nav-bar { position: fixed; top: 20px; left: 50%; transform: translateX(-50%); background: rgba(255, 255, 255, 0.75); backdrop-filter: blur(15px); padding: 10px 30px; border-radius: 50px; box-shadow: var(--soft-shadow); display: flex; gap: 20px; z-index: 1000; border: 1px solid rgba(255, 255, 255, 0.5); }
        .nav-bar a { text-decoration: none; color: var(--text-main); font-size: 0.8rem; font-weight: 600; opacity: 0.6; transition: 0.3s; padding: 5px 10px; border-radius: 20px; }
        .nav-bar a.active { opacity: 1; color: var(--main-coral); background: rgba(255, 142, 142, 0.1); }

        h2 { font-size: 1.6rem; margin-bottom: 40px; text-align: center; color: var(--main-coral); letter-spacing: 0.15em; font-weight: 700; }
        #notice h2, #order h2 { margin-bottom: 15px !important; }

        /* [PROCESS] */
        .process-container { display: flex; align-items: flex-start; justify-content: space-between; width: 100%; position: relative; box-sizing: border-box; padding: 0 10px; }
        .process-container::before { content: ''; position: absolute; top: 14px; left: calc(100% / 12); right: calc(100% / 12); height: 2px; background: #ffe5e5; z-index: 0; }
        .process-step { position: relative; z-index: 1; display: flex; flex-direction: column; align-items: center; text-align: center; flex: 1; }
        .step-num { width: 28px; height: 28px; background: var(--main-coral); color: white; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 0.75rem; font-weight: 700; margin-bottom: 15px; box-shadow: 0 4px 10px rgba(255, 142, 142, 0.3); border: 3px solid #fff; }
        .step-text { font-size: 0.85rem; font-weight: 700; color: var(--text-main); word-break: keep-all; }
        .step-sub { font-size: 0.7rem; color: var(--text-sub); margin-top: 2px; white-space: nowrap; }

        /* [PRICE] */
        .type-container { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; }
        .type-card { background: #fff5f5; padding: 35px 20px; border-radius: 20px; display: flex; flex-direction: column; align-items: center; text-align: center; transition: 0.3s; border: 1px solid transparent; }
        .type-price { font-size: 1.4rem; font-weight: 700; color: var(--main-coral); margin: 2px 0; line-height: 1.2; }

        /* [PORTFOLIO] */
        .portfolio-grid { column-count: 2; column-gap: 20px; }
        .portfolio-item { position: relative; break-inside: avoid; margin-bottom: 20px; border-radius: 16px; overflow: hidden; background: #000; }
        .portfolio-item img { width: 100%; display: block; transition: 0.5s; height: auto; }

        /* [NOTICE / ORDER] */
        .notice-top-text { text-align: center; font-size: 0.9rem; font-weight: 700; color: #222; border-bottom: 1px solid #eee; padding-bottom: 20px; margin-bottom: 25px; line-height: 1.6; word-break: keep-all; overflow-wrap: break-word; }
        .notice-content { display: grid; grid-template-columns: 1fr 1fr; gap: 30px; font-size: 0.9rem; }
        .notice-box h4 { color: var(--main-coral); margin-bottom: 15px; font-size: 1.1rem; border-left: 4px solid var(--main-coral); padding-left: 10px; }
        .notice-box ul { padding-left: 18px; color: var(--text-sub); line-height: 1.8; list-style-type: none; }
        .notice-box li::before { content: "•"; color: var(--main-coral); font-weight: bold; display: inline-block; width: 1em; margin-left: -1em; }
        
        .order-box { display: flex; flex-direction: column; gap: 18px; }
        .order-row { display: flex; flex-direction: column; gap: 8px; }
        .order-row label { font-size: 0.85rem; font-weight: 600; color: var(--text-main); }
        .order-box input, .order-box select, .order-box textarea { width: 100%; padding: 14px; border: 1px solid #eee; border-radius: 12px; background: #fafafa; font-family: inherit; font-size: 0.9rem; box-sizing: border-box; outline: none; transition: 0.3s; }
        .order-box input:focus, .order-box select:focus, .order-box textarea:focus { border-color: var(--main-coral); background: #fff; box-shadow: 0 0 0 4px rgba(255, 142, 142, 0.1); }
        
        .copy-btn { background: var(--main-coral); color: white; border: none; padding: 18px; border-radius: 14px; font-weight: 700; cursor: pointer; transition: 0.2s; margin-top: 10px; font-size: 1rem; }
        .copy-btn.active-state { background: #ff9e9e; transform: scale(0.98); }

        @media (max-width: 650px) {
            .nav-bar { width: 92%; padding: 8px 5px; gap: 2px; top: 15px; left: 50%; transform: translateX(-50%); display: flex; justify-content: center; box-sizing: border-box; }
            .nav-bar a { font-size: 0.7rem; padding: 4px 6px; flex-shrink: 0; }
            .container { padding-top: 80px; }
            .process-container { flex-direction: column; align-items: flex-start; gap: 35px; padding-left: 15px; }
            .process-container::before { left: 28px; top: 10px; bottom: 10px; width: 2px; height: auto; display: block; }
            .process-step { flex-direction: row; text-align: left; gap: 20px; width: 100%; justify-content: flex-start; }
            .step-num { margin-bottom: 0; flex-shrink: 0; }
            .portfolio-grid { column-count: 1; }
            .type-container, .notice-content { grid-template-columns: 1fr; }
            section { padding: 30px 20px; }
            .mobile-row { flex-direction: column !important; }
        }
    </style>
</head>
<body>
<div class="main-scroll-wrapper" id="scroll-area">
    <nav class="nav-bar">
        <a href="#process" class="nav-link active">PROCESS</a> <a href="#price" class="nav-link">PRICE</a> <a href="#work" class="nav-link">WORK</a> <a href="#notice" class="nav-link">NOTICE</a> <a href="#order" class="nav-link">ORDER</a>
    </nav>

    <div id="scrollHint" class="scroll-floating-hint">
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

<script>
    document.addEventListener('DOMContentLoaded', function() {
        const btn = document.getElementById('copyBtn');
        const scrollArea = document.getElementById('scroll-area');
        const hint = document.getElementById('scrollHint');
        const sections = document.querySelectorAll('section');
        const navLinks = document.querySelectorAll('.nav-bar a');

        // 복사 기능
        if (btn) {
            btn.addEventListener('click', function() {
                const f = (id) => document.getElementById(id).value;
  const text = `[Commission Form]\n- 신청 타입: ${f('type')}\n- 캐릭터 범위: ${f('range')}\n- 닉네임: ${f('nickname')}\n- 사용 목적: ${f('purpose')}\n- 캔버스 사이즈: ${f('canvas')}\n- 캐릭터 자료: ${f('details')}\n- 구도 및 포즈: ${f('pose')}\n- 배경: ${f('background')}\n- 기타 문의사항: ${f('etc')}\n\n* 모든 사항은 이미지 자료가 있으면 더 정확한 작업이 가능합니다!`;
                const textArea = document.createElement("textarea");
                textArea.value = text;
                textArea.style.position = "fixed";
                textArea.style.left = "-9999px";
                textArea.style.top = "0";
                textArea.setAttribute('readonly', '');
                document.body.appendChild(textArea);
                textArea.focus();
                textArea.select();
                textArea.setSelectionRange(0, 99999);
                try {
                    document.execCommand('copy');
                    const originalText = btn.innerText; 
                    btn.innerText = "복사 완료!"; 
                    btn.classList.add('active-state');
                    setTimeout(() => { 
                        btn.innerText = originalText; 
                        btn.classList.remove('active-state'); 
                    }, 1000);
                } catch (err) {}
                document.body.removeChild(textArea);
            });
        }

        // 스크롤 이벤트 통합
        scrollArea.addEventListener('scroll', () => {
            // 1. 안내 힌트 숨기기
            if (scrollArea.scrollTop > 50) {
                hint.classList.add('hidden');
            } else {
                hint.classList.remove('hidden');
            }

            // 2. 섹션 등장 애니메이션 및 네비 활성화
            let current = "";
            sections.forEach(section => {
                const sectionTop = section.offsetTop;
                if (scrollArea.scrollTop > sectionTop - scrollArea.offsetHeight * 0.85) section.classList.add('visible');
                if (scrollArea.scrollTop >= sectionTop - 150) current = section.getAttribute('id');
            });
            navLinks.forEach(link => {
                link.classList.remove('active');
                if (link.getAttribute('href').includes(current)) link.classList.add('active');
            });
        });

        // 네비 클릭 스무스 스크롤
        navLinks.forEach(anchor => {
            anchor.addEventListener('click', function(e) {
                e.preventDefault(); 
                const targetId = this.getAttribute('href');
                const targetElement = document.querySelector(targetId);
                if (targetElement && scrollArea) {
                    const targetOffset = targetElement.offsetTop - 100; 
                    scrollArea.scrollTo({ top: targetOffset, behavior: 'smooth' });
                }
            });
        });
    });

    window.onload = () => { 
        const sections = document.querySelectorAll('section');
        if(sections[0]) sections[0].classList.add('visible'); 
    };
</script>


</body>
</html>
