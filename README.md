<!DOCTYPE html>
<html>
<head>
  <title>لعبة اصطياد النجوم المتطورة</title>
  <style>
    body {
      display: flex; justify-content: center; align-items: center; height: 100vh;
      background: #222; color: white; font-family: Arial, sans-serif;
      margin: 0;
      user-select: none;
      position: relative;
      overflow: hidden;
    }
    #star {
      width: 60px; height: 60px; border-radius: 50%;
      position: absolute; cursor: pointer;
      display: flex; justify-content: center; align-items: center;
      font-size: 36px;
      transition: left 0.3s ease, top 0.3s ease, background-color 0.5s ease;
      box-shadow: 0 0 15px rgba(255, 255, 255, 0.7);
      color: white;
      user-select: none;
    }
    #score {
      position: fixed; top: 10px; left: 10px; font-size: 24px;
      font-weight: bold;
    }
    #timer {
      position: fixed; top: 10px; right: 10px; font-size: 24px;
      font-weight: bold;
    }
  </style>
</head>
<body>
  <div id="score">النقاط: 0</div>
  <div id="timer">الوقت: 30</div>
  <div id="star">★</div>

<script>
  const star = document.getElementById('star');
  const scoreDisplay = document.getElementById('score');
  const timerDisplay = document.getElementById('timer');

  let score = 0;
  let timeLeft = 30;
  let hideTimeout;

  const colors = ['#e74c3c', '#f1c40f', '#2ecc71', '#3498db', '#9b59b6', '#e67e22', '#1abc9c'];

  function randomColor() {
    return colors[Math.floor(Math.random() * colors.length)];
  }

  function moveStar() {
    clearTimeout(hideTimeout);
    const maxX = window.innerWidth - 60;
    const maxY = window.innerHeight - 60;
    const randomX = Math.floor(Math.random() * maxX);
    const randomY = Math.floor(Math.random() * maxY);

    star.style.left = randomX + 'px';
    star.style.top = randomY + 'px';
    star.style.backgroundColor = randomColor();
    star.style.boxShadow = '0 0 15px rgba(255, 255, 255, 0.7)';

    // النجمة تختفي إذا ما ضغطت عليها خلال 1.5 ثانية
    hideTimeout = setTimeout(() => {
      star.style.backgroundColor = 'transparent';
      star.style.boxShadow = 'none';
      setTimeout(() => {
        star.style.backgroundColor = randomColor();
        star.style.boxShadow = '0 0 15px rgba(255, 255, 255, 0.7)';
        moveStar();
      }, 300);
    }, 1500);
  }

  star.addEventListener('click', () => {
    score++;
    scoreDisplay.textContent = 'النقاط: ' + score;
    clearTimeout(hideTimeout);
    moveStar();
  });

  function countdown() {
    if (timeLeft <= 0) {
      alert('انتهت اللعبة! نقاطك: ' + score);
      clearInterval(timerInterval);
      star.style.display = 'none';
    } else {
      timerDisplay.textContent = 'الوقت: ' + timeLeft;
      timeLeft--;
    }
  }

  moveStar();
  const timerInterval = setInterval(countdown, 1000);
</script>
</body>
</html>
