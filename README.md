Добавление Bootstrap:
Самый простой способ подключить Bootstrap — использовать CDN-ссылку. Вам нужно добавить эту ссылку в тег <head> вашего HTML-документа

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Таймер с анимацией</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.0-alpha1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-GLhlTQ8iRABdZLl6O3oVMWSktQXK1xIjWoKUIE3iIGMigmgfE4jaqniHkGnkXhFNy" crossorigin="anonymous">
    <style>
        .timer-container {
            position: relative;
            width: 200px;
            height: 200px;
            margin: auto;
        }

        #timer-text {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-size: 24px;
            color: #333;
            z-index: 1;
        }

        .timer-container svg circle {
            transform: rotate(-90deg);
            transform-origin: center;
            transition: all 0.25s linear;
        }

        .timer-container svg #progress-circle {
            stroke-dasharray: 565;
            stroke-dashoffset: 565;
            stroke: #007bff;
        }
    </style>
</head>
<body>
    <div class="container d-flex justify-content-center mt-5">
        <div class="timer-container">
            <span id="timer-text" class="fw-bold fs-3 text-dark">00:00</span>
            <svg width="200" height="200" viewBox="0 0 200 200">
                <circle cx="100" cy="100" r="90" stroke-width="20" fill="none" />
                <circle id="progress-circle" cx="100" cy="100" r="90" stroke-width="20" fill="none" />
            </svg>
        </div>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const timerText = document.getElementById('timer-text');
            const progressCircle = document.getElementById('progress-circle');
            let currentTime = 0;
            const totalDuration = 180; // 3 минуты = 180 секунд

            function formatTime(minutes, seconds) {
                minutes = minutes.toString().padStart(2, '0');
                seconds = seconds.toString().padStart(2, '0');
                return `${minutes}:${seconds}`;
            }

            function updateTimer() {
                let minutes = Math.floor(currentTime / 60);
                let seconds = currentTime % 60;

                timerText.textContent = formatTime(minutes, seconds);
            }

            function updateProgress() {
                const percent = currentTime / totalDuration;
                const offset = 565 - (percent * 565);
                progressCircle.style.strokeDashoffset = offset;
            }

            function tick() {
                if (currentTime < totalDuration) {
                    currentTime += 1;
                    updateTimer();
                    updateProgress();
                    setTimeout(tick, 1000);
                }
            }

            tick(); // Начинаем отсчёт
        });
    </script>
</body>
</html>

Изменения в разметке:
Мы добавили класс container из Bootstrap для центрирования контента на странице.
Использовали классы d-flex justify-content-center mt-5 для выравнивания таймера по центру и добавления отступа сверху.
Применили классы fw-bold fs-3 text-dark к тексту таймера для изменения размера шрифта и цвета.s
