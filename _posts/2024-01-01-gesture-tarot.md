---
layout: slide
title: "手势翻开的塔罗体验"
---

<div class="tarot-app" id="tarot-app">
  <div class="tarot-header">
    <p>用手势翻牌，体验一张张塔罗带来的启示。向上滑动/拖动牌面即可翻开，点击或轻点也同样有效。</p>
  </div>
  <div class="tarot-table">
    <div class="tarot-card" id="tarot-card">
      <div class="card-inner">
        <div class="card-face card-back">
          <div class="card-pattern">✨</div>
          <div class="card-label">向上滑动翻牌</div>
        </div>
        <div class="card-face card-front">
          <div class="card-title" id="tarot-name">准备好了吗？</div>
          <div class="card-meaning" id="tarot-meaning">向上滑或轻点卡片即可抽牌。</div>
        </div>
      </div>
    </div>
    <div class="tarot-panel">
      <p class="tarot-status" id="tarot-status">洗牌中……完成后向上滑动翻牌。</p>
      <ul class="tarot-tips">
        <li>向上滑动：翻开下一张牌并给出解释。</li>
        <li>向下滑动：重置到背面，准备重新感受能量。</li>
        <li>左右滑动：轻抚卡面，保持当前抽到的牌。</li>
      </ul>
      <div class="tarot-actions">
        <button type="button" id="tarot-shuffle">重新洗牌</button>
        <button type="button" id="tarot-flip">轻点翻牌</button>
      </div>
    </div>
  </div>
</div>

<style>
.tarot-app {
  max-width: 1000px;
  margin: 0 auto;
  padding: 1.5rem;
  color: #f4f6fb;
  background: radial-gradient(circle at 20% 20%, rgba(255, 255, 255, 0.08), transparent 35%),
    radial-gradient(circle at 80% 0%, rgba(113, 188, 255, 0.1), transparent 30%),
    linear-gradient(135deg, #0c1021 0%, #141a32 60%, #0c1021 100%);
  border-radius: 18px;
  box-shadow: 0 18px 50px rgba(0, 0, 0, 0.55);
}

.tarot-header p {
  margin: 0 0 1rem;
  line-height: 1.6;
  font-size: 1rem;
}

.tarot-table {
  display: grid;
  grid-template-columns: 1fr minmax(260px, 320px);
  gap: 1.5rem;
  align-items: center;
}

.tarot-card {
  width: min(100%, 320px);
  height: 460px;
  margin: 0 auto;
  perspective: 1200px;
  border-radius: 18px;
  position: relative;
}

.card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  transition: transform 0.8s ease;
  transform-style: preserve-3d;
  border-radius: 18px;
  box-shadow: 0 18px 40px rgba(0, 0, 0, 0.4);
}

.tarot-card.flipped .card-inner {
  transform: rotateY(180deg);
}

.card-face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  border-radius: 18px;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 1.5rem;
  box-sizing: border-box;
}

.card-back {
  background: radial-gradient(circle at 30% 30%, rgba(255, 255, 255, 0.1), transparent 40%),
    linear-gradient(135deg, #0f1a3d, #1f2f60 45%, #0f1a3d);
  color: #cfe8ff;
  border: 2px solid rgba(180, 206, 255, 0.4);
  letter-spacing: 0.08em;
  text-transform: uppercase;
  text-align: center;
}

.card-pattern {
  font-size: 3rem;
  margin-bottom: 1rem;
  filter: drop-shadow(0 0 6px rgba(255, 255, 255, 0.6));
}

.card-label {
  font-size: 1.1rem;
  opacity: 0.9;
}

.card-front {
  background: linear-gradient(135deg, #f6e9d2 0%, #f6f1e1 45%, #f6e9d2 100%);
  color: #1b1b1b;
  transform: rotateY(180deg);
  border: 2px solid rgba(139, 110, 76, 0.4);
  box-shadow: inset 0 0 0 2px rgba(255, 255, 255, 0.5);
}

.card-title {
  font-size: 1.4rem;
  font-weight: 700;
  text-align: center;
  margin-bottom: 0.75rem;
  color: #3c2a1d;
}

.card-meaning {
  font-size: 1rem;
  line-height: 1.6;
  color: #45362b;
  text-align: left;
}

.tarot-panel {
  background: rgba(255, 255, 255, 0.04);
  border: 1px solid rgba(255, 255, 255, 0.08);
  padding: 1rem 1.25rem;
  border-radius: 14px;
  backdrop-filter: blur(4px);
}

.tarot-status {
  margin: 0 0 0.75rem;
  font-weight: 600;
}

.tarot-tips {
  margin: 0 0 1rem 1.2rem;
  padding: 0;
  line-height: 1.5;
}

.tarot-actions {
  display: flex;
  gap: 0.75rem;
  flex-wrap: wrap;
}

.tarot-actions button {
  background: linear-gradient(135deg, #6c8cff, #8aa5ff);
  border: none;
  color: #0c0f1e;
  padding: 0.65rem 1rem;
  border-radius: 10px;
  font-weight: 700;
  cursor: pointer;
  transition: transform 0.15s ease, box-shadow 0.15s ease;
}

.tarot-actions button:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 18px rgba(0, 0, 0, 0.2);
}

.tarot-actions button:active {
  transform: translateY(0);
  box-shadow: none;
}

@media (max-width: 900px) {
  .tarot-table {
    grid-template-columns: 1fr;
  }

  .tarot-card {
    height: 400px;
  }
}
</style>

<script>
(() => {
  const app = document.getElementById('tarot-app');
  if (!app) return;

  const card = document.getElementById('tarot-card');
  const cardName = document.getElementById('tarot-name');
  const cardMeaning = document.getElementById('tarot-meaning');
  const statusEl = document.getElementById('tarot-status');
  const shuffleBtn = document.getElementById('tarot-shuffle');
  const flipBtn = document.getElementById('tarot-flip');

  const tarotCards = [
    { name: '愚人 · The Fool', meaning: '新的开始、勇气与信任直觉的邀约，提醒你踏出第一步。' },
    { name: '魔术师 · The Magician', meaning: '掌握资源、运用技能，把灵感转化为行动，你拥有开启局面的力量。' },
    { name: '女祭司 · The High Priestess', meaning: '倾听内心的声音、保持静默与洞察，答案在潜意识里等你发觉。' },
    { name: '恋人 · The Lovers', meaning: '关系、价值观与选择的课题，真诚沟通与共鸣将带来和谐。' },
    { name: '战车 · The Chariot', meaning: '决心、意志与前进的驱动力，朝目标稳定推进，你会赢得主动权。' },
    { name: '力量 · Strength', meaning: '温柔的力量与耐心，接受脆弱并以爱化解阻力，勇敢且温柔。' },
    { name: '隐者 · The Hermit', meaning: '暂停与沉思，独处带来清晰，看见真正的需求后再出发。' },
    { name: '命运之轮 · Wheel of Fortune', meaning: '周期与转折的节点，拥抱变化，顺势调整，你正站在新的分岔口。' },
    { name: '星星 · The Star', meaning: '希望、疗愈与灵感的流动，相信宇宙的指引，愿望正在成形。' },
    { name: '太阳 · The Sun', meaning: '光明、喜悦与成功，勇敢展露自我，能量被看见也被祝福。' },
    { name: '审判 · Judgement', meaning: '觉醒与召唤，回应内心的声音，迎接一个更贴近真实自我的阶段。' },
    { name: '世界 · The World', meaning: '完成、整合与新的循环，庆祝你的成就，同时准备迎接全新的起点。' }
  ];

  let deck = [];
  let drawnCount = 0;
  let startPoint = null;
  let isAnimating = false;

  const setStatus = (text) => {
    statusEl.textContent = text;
  };

  const shuffle = () => {
    deck = [...tarotCards].sort(() => Math.random() - 0.5);
    drawnCount = 0;
    card.classList.remove('flipped');
    cardName.textContent = '准备好了吗？';
    cardMeaning.textContent = '向上滑或轻点卡片即可抽牌。';
    setStatus('洗牌完成，向上滑动牌面翻开。');
  };

  const flipNext = (trigger = 'gesture') => {
    if (isAnimating) return;
    if (drawnCount >= deck.length) {
      setStatus('牌组已抽完，点击“重新洗牌”重新开始。');
      return;
    }

    const cardData = deck[drawnCount++];
    isAnimating = true;

    card.classList.remove('flipped');
    window.setTimeout(() => {
      cardName.textContent = cardData.name;
      cardMeaning.textContent = cardData.meaning;
      card.classList.add('flipped');
      setStatus(`你抽到了：${cardData.name}（${trigger === 'tap' ? '轻点' : '手势'}翻牌）`);
      window.setTimeout(() => {
        isAnimating = false;
      }, 400);
    }, 80);
  };

  const handleGesture = (endX, endY) => {
    if (!startPoint) return;
    const deltaX = endX - startPoint.x;
    const deltaY = endY - startPoint.y;

    const isVertical = Math.abs(deltaY) > Math.abs(deltaX);
    const swipeUp = deltaY < -40 && isVertical;
    const swipeDown = deltaY > 50 && isVertical;
    const softTouch = Math.abs(deltaX) < 15 && Math.abs(deltaY) < 15;

    if (swipeUp) {
      flipNext('gesture');
    } else if (swipeDown) {
      card.classList.remove('flipped');
      setStatus('已回到牌背，感受一下能量再翻开。');
    } else if (softTouch) {
      flipNext('tap');
    } else {
      setStatus('向上滑动以翻牌，或轻点卡面。');
    }

    startPoint = null;
  };

  card.addEventListener('pointerdown', (event) => {
    startPoint = { x: event.clientX, y: event.clientY };
    card.setPointerCapture(event.pointerId);
  });

  card.addEventListener('pointerup', (event) => {
    handleGesture(event.clientX, event.clientY);
    card.releasePointerCapture(event.pointerId);
  });

  card.addEventListener('pointercancel', () => {
    startPoint = null;
  });

  card.addEventListener('keydown', (event) => {
    if (event.key === 'Enter' || event.key === ' ' || event.key.toLowerCase() === 'w' || event.key === 'ArrowUp') {
      flipNext('keyboard');
    }
    if (event.key === 's' || event.key === 'ArrowDown') {
      card.classList.remove('flipped');
      setStatus('已回到牌背，轻点或上滑再次翻牌。');
    }
  });

  card.tabIndex = 0;

  shuffleBtn.addEventListener('click', () => shuffle());
  flipBtn.addEventListener('click', () => flipNext('tap'));

  shuffle();
})();
</script>
