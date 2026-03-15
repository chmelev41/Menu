<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>KinoSphere - Меню</title>
    <style>
        /* Стили в стиле современных кинотеатров (тёмная тема) */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, sans-serif;
        }

        body {
            background: linear-gradient(145deg, #0b0f1c 0%, #141b2b 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }

        /* Основной контейнер меню */
        .kinosphere-menu {
            width: 320px;
            background: rgba(18, 25, 40, 0.95);
            backdrop-filter: blur(10px);
            border-radius: 24px;
            box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.8), 0 0 0 1px rgba(255, 255, 255, 0.05) inset;
            overflow: hidden;
            border: 1px solid rgba(255, 255, 255, 0.08);
        }

        /* Шапка меню */
        .menu-header {
            padding: 24px 20px;
            background: linear-gradient(90deg, #58C4A6 0%, #58C4A6 100%);
            position: relative;
        }

        .menu-header h2 {
            color: white;
            font-size: 24px;
            font-weight: 700;
            letter-spacing: -0.5px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .menu-header h2 span {
            font-size: 32px;
            filter: drop-shadow(0 4px 6px rgba(0,0,0,0.2));
        }

        .menu-header .subtitle {
            color: rgba(255, 255, 255, 0.9);
            font-size: 14px;
            margin-top: 6px;
            font-weight: 400;
            opacity: 0.9;
        }

        /* Индикатор текущего раздела */
        .current-section {
            padding: 12px 20px;
            background: rgba(0, 0, 0, 0.3);
            border-bottom: 1px solid rgba(255, 255, 255, 0.06);
            font-size: 13px;
            color: #8e9bb3;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        .current-section span {
            color: white;
            font-weight: 500;
            background: #433852;
            padding: 4px 10px;
            border-radius: 30px;
            font-size: 12px;
            border: 1px solid #433852;
        }

        /* Список меню */
        .menu-list {
            list-style: none;
            padding: 8px;
        }

        .menu-item {
            margin: 2px 0;
            border-radius: 16px;
            overflow: hidden;
        }

        /* Кнопки/ссылки меню */
        .menu-button {
            display: flex;
            align-items: center;
            justify-content: space-between;
            width: 100%;
            padding: 14px 16px;
            background: transparent;
            border: none;
            color: #e1e6f0;
            font-size: 15px;
            font-weight: 500;
            text-align: left;
            cursor: pointer;
            transition: all 0.2s ease;
            border-radius: 16px;
        }

        .menu-button:hover {
            background: rgba(255, 255, 255, 0.06);
            color: white;
        }

        .menu-button:active {
            background: rgba(255, 107, 74, 0.15);
        }

        /* Иконка слева */
        .button-icon {
            font-size: 20px;
            margin-right: 12px;
            filter: drop-shadow(0 2px 4px rgba(0,0,0,0.3));
        }

        .button-title {
            flex: 1;
            display: flex;
            align-items: center;
            gap: 8px;
        }

        /* Стрелка для пунктов с подменю */
        .arrow {
            font-size: 16px;
            color: #5f6b84;
            transition: transform 0.25s ease;
        }

        .arrow.open {
            transform: rotate(90deg);
            color: #58C4A6;
        }

        /* Стили для ссылок (без подменю) */
        .menu-link {
            text-decoration: none;
            color: #e1e6f0;
            display: flex;
            align-items: center;
            padding: 14px 16px;
            transition: all 0.2s;
            border-radius: 16px;
        }

        .menu-link:hover {
            background: rgba(255, 255, 255, 0.06);
            color: white;
        }

        .menu-link:active {
            background: rgba(255, 107, 74, 0.15);
        }

        /* Подменю (вложенные списки) */
        .submenu {
            list-style: none;
            margin-left: 20px;
            padding-left: 16px;
            border-left: 1px dashed rgba(255, 107, 74, 0.3);
            display: none;
            animation: fadeIn 0.2s ease;
        }

        .submenu.active {
            display: block;
        }

        .submenu .menu-button,
        .submenu .menu-link {
            padding: 12px 16px;
            font-size: 14px;
        }

        .submenu .submenu {
            margin-left: 24px;
            border-left-color: rgba(255, 170, 92, 0.3);
        }

        /* Уведомление */
        .notification {
            margin: 12px 16px 16px;
            padding: 12px 16px;
            background: rgba(0, 0, 0, 0.4);
            border-radius: 40px;
            font-size: 13px;
            color: #a5b3cc;
            border: 1px solid rgba(255, 255, 255, 0.06);
            backdrop-filter: blur(5px);
            display: flex;
            align-items: center;
            gap: 8px;
            transition: all 0.3s;
            min-height: 48px;
        }

        .notification.has-link {
            background: #2F253E;
            border-color: #56BCA1;
            color: #56BCA1;
        }

        .notification-icon {
            font-size: 20px;
        }

        .notification-text {
            flex: 1;
            line-height: 1.4;
        }

        /* Кнопка сброса */
        .reset-button {
            display: block;
            width: calc(100% - 32px);
            margin: 8px 16px 20px;
            padding: 12px;
            background: rgba(255, 255, 255, 0.04);
            border: 1px solid rgba(255, 255, 255, 0.08);
            border-radius: 40px;
            color: #8e9bb3;
            font-size: 13px;
            font-weight: 500;
            cursor: pointer;
            transition: all 0.2s;
            text-align: center;
            backdrop-filter: blur(5px);
        }

        .reset-button:hover {
            background: #1C122B;
            color: white;
            border-color: #58C4A6;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(-5px); }
            to { opacity: 1; transform: translateY(0); }
        }

        /* Маленький бейдж "новинка" */
        .badge {
            background: #58C4A6;
            color: white;
            font-size: 10px;
            font-weight: 600;
            padding: 3px 8px;
            border-radius: 30px;
            margin-left: 8px;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
    </style>
</head>
<body>
    <div class="kinosphere-menu">
        <!-- Шапка -->
        <div class="menu-header">
            <h2>
                <span>🎬</span> KinoSphere
            </h2>
            <div class="subtitle">кино по клику</div>
        </div>

        <!-- Текущий раздел (будет обновляться) -->
        <div class="current-section" id="currentSection">
            📍 Раздел: <span id="sectionDisplay">Главная</span>
        </div>

        <!-- Контейнер для уведомлений -->
        <div class="notification" id="notification">
            <span class="notification-icon">ℹ️</span>
            <span class="notification-text" id="notificationText">Нажмите на пункт меню</span>
        </div>

        <!-- ОСНОВНОЕ МЕНЮ (три уровня) -->
        <ul class="menu-list" id="mainMenu">
            <!-- УРОВЕНЬ 1: Фильмы (с подменю) -->
            <li class="menu-item">
                <button class="menu-button has-submenu" data-path="Фильмы" data-level="1">
                    <span class="button-title">
                        <span class="button-icon">🎥</span>
                        <span>Фильмы</span>
                    </span>
                    <span class="arrow">▶</span>
                </button>
                <!-- Подменю уровень 2 -->
                <ul class="submenu">
                    <li class="menu-item">
                        <button class="menu-button has-submenu" data-path="Фильмы > Жанры" data-level="2">
                            <span class="button-title">
                                <span class="button-icon">📽️</span>
                                <span>По жанрам</span>
                            </span>
                            <span class="arrow">▶</span>
                        </button>
                        <!-- Подменю уровень 3 -->
                        <ul class="submenu">
                            <li class="menu-item">
                                <a href="#" class="menu-link" data-path="Фильмы > Жанры > Боевики" data-url="/genre/action">🔫 Боевики</a>
                            </li>
                            <li class="menu-item">
                                <a href="#" class="menu-link" data-path="Фильмы > Жанры > Комедии" data-url="/genre/comedy">😂 Комедии</a>
                            </li>
                            <li class="menu-item">
                                <a href="#" class="menu-link" data-path="Фильмы > Жанры > Драмы" data-url="/genre/drama">🎭 Драмы</a>
                            </li>
                        </ul>
                    </li>
                    <li class="menu-item">
                        <a href="#" class="menu-link" data-path="Фильмы > Новинки" data-url="/new-movies">
                            <span class="button-icon">✨</span> Новинки
                            <span class="badge">new</span>
                        </a>
                    </li>
                    <li class="menu-item">
                        <a href="#" class="menu-link" data-path="Фильмы > Подборки" data-url="/collections">
                            <span class="button-icon">📚</span> Подборки для вас
                        </a>
                    </li>
                </ul>
            </li>

            <!-- УРОВЕНЬ 1: Сериалы (с подменю) -->
            <li class="menu-item">
                <button class="menu-button has-submenu" data-path="Сериалы" data-level="1">
                    <span class="button-title">
                        <span class="button-icon">📺</span>
                        <span>Сериалы</span>
                    </span>
                    <span class="arrow">▶</span>
                </button>
                <!-- Подменю уровень 2 -->
                <ul class="submenu">
                    <li class="menu-item">
                        <button class="menu-button has-submenu" data-path="Сериалы > По странам" data-level="2">
                            <span class="button-title">
                                <span class="button-icon">🌍</span>
                                <span>По странам</span>
                            </span>
                            <span class="arrow">▶</span>
                        </button>
                        <!-- Уровень 3 -->
                        <ul class="submenu">
                            <li class="menu-item">
                                <a href="#" class="menu-link" data-path="Сериалы > По странам > Русские" data-url="/series/russian">🇷🇺 Русские</a>
                            </li>
                            <li class="menu-item">
                                <a href="#" class="menu-link" data-path="Сериалы > По странам > Корейские" data-url="/series/korean">🇰🇷 Корейские</a>
                            </li>
                            <li class="menu-item">
                                <a href="#" class="menu-link" data-path="Сериалы > По странам > Американские" data-url="/series/usa">🇺🇸 Американские</a>
                            </li>
                        </ul>
                    </li>
                    <li class="menu-item">
                        <a href="#" class="menu-link" data-path="Сериалы > Популярные" data-url="/series/popular">
                            <span class="button-icon">🔥</span> Популярные
                        </a>
                    </li>
                </ul>
            </li>

            <!-- УРОВЕНЬ 1: Мой профиль (простая ссылка) -->
            <li class="menu-item">
                <a href="#" class="menu-link" data-path="Профиль" data-url="/profile">
                    <span class="button-icon">👤</span>
                    <span>Мой профиль</span>
                </a>
            </li>

            <!-- УРОВЕНЬ 1: Избранное (простая ссылка) -->
            <li class="menu-item">
                <a href="#" class="menu-link" data-path="Избранное" data-url="/favorites">
                    <span class="button-icon">❤️</span>
                    <span>Избранное</span>
                </a>
            </li>
        </ul>

        <!-- Кнопка сброса -->
        <button class="reset-button" id="resetMenu">⟲ Сбросить навигацию</button>
    </div>

    <script>
        document.addEventListener('DOMContentLoaded', function() {
            const mainMenu = document.getElementById('mainMenu');
            const sectionDisplay = document.getElementById('sectionDisplay');
            const notification = document.getElementById('notification');
            const notificationText = document.getElementById('notificationText');
            
            // Текущий путь в меню
            let currentPath = ['Главная'];

            // Функция обновления отображения текущего раздела
            function updateSectionDisplay() {
                sectionDisplay.textContent = currentPath.join(' > ');
            }

            // Функция показа уведомления
            function showNotification(message, isLink = false) {
                notificationText.textContent = message;
                if (isLink) {
                    notification.classList.add('has-link');
                } else {
                    notification.classList.remove('has-link');
                }
            }

            // Функция для закрытия всех подменю
            function closeAllSubmenus() {
                document.querySelectorAll('.submenu').forEach(sub => {
                    sub.classList.remove('active');
                });
                document.querySelectorAll('.arrow').forEach(arrow => {
                    arrow.classList.remove('open');
                });
            }

            // Функция для закрытия подменю начиная с определенного уровня
            function closeDeeperSubmenus(level, element) {
                let parent = element.closest('.submenu');
                while (parent) {
                    const deeperSubs = parent.querySelectorAll('.submenu');
                    deeperSubs.forEach(sub => sub.classList.remove('active'));
                    parent = parent.parentElement.closest('.submenu');
                }
            }

            // Обработка кликов по меню
            mainMenu.addEventListener('click', function(e) {
                const target = e.target.closest('.menu-button, .menu-link');
                if (!target) return;

                e.preventDefault(); // Предотвращаем переход по ссылке для демонстрации

                // ОБРАБОТКА КНОПКИ С ПОДМЕНЮ (has-submenu)
                if (target.classList.contains('has-submenu')) {
                    const path = target.dataset.path || target.querySelector('span span')?.textContent || 'Раздел';
                    const level = parseInt(target.dataset.level) || 1;
                    
                    // Обновляем путь (обрезаем до текущего уровня и добавляем новый)
                    currentPath = currentPath.slice(0, level);
                    currentPath.push(path.split(' > ').pop()); // Берём последнюю часть
                    updateSectionDisplay();

                    // Находим связанное подменю (следующий элемент)
                    const submenu = target.nextElementSibling;
                    if (submenu && submenu.classList.contains('submenu')) {
                        // Закрываем более глубокие подменю
                        closeDeeperSubmenus(level, target);
                        
                        // Переключаем текущее подменю
                        const isOpening = !submenu.classList.contains('active');
                        
                        // Сначала закроем другие подменю на этом же уровне (по желанию)
                        if (isOpening) {
                            const parentLi = target.closest('li');
                            if (parentLi) {
                                const siblings = Array.from(parentLi.parentElement.children);
                                siblings.forEach(li => {
                                    if (li !== parentLi) {
                                        const btn = li.querySelector('.has-submenu');
                                        const subm = li.querySelector('.submenu');
                                        if (btn && subm) {
                                            btn.querySelector('.arrow')?.classList.remove('open');
                                            subm.classList.remove('active');
                                        }
                                    }
                                });
                            }
                        }

                        // Переключаем состояние
                        if (submenu.classList.contains('active')) {
                            submenu.classList.remove('active');
                            target.querySelector('.arrow')?.classList.remove('open');
                            showNotification(`🚪 Закрыт раздел "${path.split(' > ').pop()}"`);
                            
                            // Убираем последний элемент из пути
                            currentPath.pop();
                            updateSectionDisplay();
                        } else {
                            submenu.classList.add('active');
                            target.querySelector('.arrow')?.classList.add('open');
                            showNotification(`📂 Открыт раздел "${path.split(' > ').pop()}"`);
                        }
                    }
                }

                // ОБРАБОТКА ССЫЛКИ (menu-link)
                else if (target.classList.contains('menu-link')) {
                    const path = target.dataset.path || target.innerText.trim();
                    const url = target.dataset.url || '#';
                    
                    // Обновляем путь (разбираем строку path)
                    if (path.includes(' > ')) {
                        currentPath = path.split(' > ');
                    } else {
                        currentPath = [...currentPath.slice(0, -1), path];
                    }
                    updateSectionDisplay();

                    // Показываем уведомление о ссылке
                    showNotification(`✨ Переход: ${path} (${url})`, true);
                    
                    // Здесь можно добавить реальный переход:
                    // window.location.href = url;
                }
            });

            // Сброс навигации
            document.getElementById('resetMenu').addEventListener('click', function() {
                closeAllSubmenus();
                currentPath = ['Главная'];
                updateSectionDisplay();
                showNotification('🏠 Вы на главной');
            });

            // Инициализация
            updateSectionDisplay();
        });
    </script>
</body>
</html>
