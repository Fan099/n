<!DOCTYPE html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Genshin Impact — Калькулятор и Сборки</title>
  <!-- Подключаем Tailwind CSS для шикарного дизайна -->
  <script src="https://cdn.tailwindcss.com"></script>
  <!-- Шрифт Inter для идеальной читаемости -->
  <link href="https://fonts.googleapis.com/css2?family=Inter:wght=300;400;500;600;700;800&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Inter', sans-serif;
      background-color: #0c0e17;
    }
    /* Кастомный скроллбар в стиле Genshin */
    ::-webkit-scrollbar {
      width: 6px;
    }
    ::-webkit-scrollbar-track {
      background: #11131e;
    }
    ::-webkit-scrollbar-thumb {
      background: #2d3142;
      border-radius: 3px;
    }
    ::-webkit-scrollbar-thumb:hover {
      background: #4a506b;
    }
  </style>
</head>
<body class="text-slate-200 min-h-screen flex flex-col">

  <!-- ШАПКА И НАВИГАЦИЯ -->
  <header class="bg-[#11131e] border-b border-slate-800 sticky top-0 z-50">
    <div class="max-w-7xl mx-auto px-4 py-4 flex flex-col lg:flex-row items-center justify-between gap-4">
      <div class="flex items-center gap-3">
        <span class="text-2xl text-amber-400">✨</span>
        <div>
          <h1 class="text-xl font-extrabold tracking-tight text-amber-400">Genshin Companion</h1>
          <p class="text-xs text-slate-400">Планировщик ресурсов, редактор материалов и персональные сборки</p>
        </div>
      </div>
      
      <!-- Главное меню (Табы) -->
      <nav class="flex flex-wrap gap-1 bg-[#161925] p-1 rounded-xl border border-slate-800">
        <button id="btn-characters" class="menu-btn px-4 py-2 rounded-lg text-sm font-semibold transition-all duration-200 bg-amber-500 text-slate-950 shadow-lg" onclick="switchTab('characters')">
          Персонажи
        </button>
        <button id="btn-calculator" class="menu-btn px-4 py-2 rounded-lg text-sm font-semibold text-slate-400 hover:text-slate-100 transition-all duration-200" onclick="switchTab('calculator')">
          Прокачка (Калькулятор)
        </button>
        <button id="btn-builds" class="menu-btn px-4 py-2 rounded-lg text-sm font-semibold text-slate-400 hover:text-slate-100 transition-all duration-200" onclick="switchTab('builds')">
          Сборки (Билды)
        </button>
        <button id="btn-editor" class="menu-btn px-4 py-2 rounded-lg text-sm font-semibold text-slate-400 hover:text-slate-100 transition-all duration-200" onclick="switchTab('editor')">
          ⚙️ Редактор базы
        </button>
      </nav>
    </div>
  </header>

  <!-- ГЛАВНЫЙ КОНТЕНТ -->
  <main class="flex-grow max-w-7xl w-full mx-auto px-4 py-8">

    <!-- Вкладка 1: Сетка персонажей -->
    <section id="section-characters" class="tab-content block">
      <div class="mb-6 flex flex-col md:flex-row md:items-center justify-between gap-4">
        <div>
          <h2 class="text-2xl font-bold text-slate-100">Выберите персонажа</h2>
          <p class="text-sm text-slate-400 mt-1">Выберите героя, чтобы открыть его реальный гайд, настроить ресурсы или изменить его карточку.</p>
        </div>
        <!-- Фильтр по стихиям -->
        <div class="flex flex-wrap gap-1.5 bg-[#11131e] p-1.5 rounded-xl border border-slate-800">
          <button onclick="filterElements('all')" class="element-filter-btn px-3 py-1.5 text-xs font-semibold rounded-lg bg-slate-800 text-amber-400">Все</button>
          <button onclick="filterElements('Pyro')" class="element-filter-btn px-3 py-1.5 text-xs font-semibold rounded-lg hover:bg-slate-800 text-red-400">Pyro</button>
          <button onclick="filterElements('Hydro')" class="element-filter-btn px-3 py-1.5 text-xs font-semibold rounded-lg hover:bg-slate-800 text-sky-400">Hydro</button>
          <button onclick="filterElements('Dendro')" class="element-filter-btn px-3 py-1.5 text-xs font-semibold rounded-lg hover:bg-slate-800 text-emerald-400">Dendro</button>
          <button onclick="filterElements('Electro')" class="element-filter-btn px-3 py-1.5 text-xs font-semibold rounded-lg hover:bg-slate-800 text-purple-400">Electro</button>
          <button onclick="filterElements('Anemo')" class="element-filter-btn px-3 py-1.5 text-xs font-semibold rounded-lg hover:bg-slate-800 text-teal-400">Anemo</button>
          <button onclick="filterElements('Geo')" class="element-filter-btn px-3 py-1.5 text-xs font-semibold rounded-lg hover:bg-slate-800 text-amber-500">Geo</button>
          <button onclick="filterElements('Cryo')" class="element-filter-btn px-3 py-1.5 text-xs font-semibold rounded-lg hover:bg-slate-800 text-cyan-400">Cryo</button>
        </div>
      </div>

      <div id="characters-grid" class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-6 gap-5">
        <!-- Сюда JS вставит карточки героев -->
      </div>
    </section>

    <!-- Вкладка 2: Калькулятор ресурсов -->
    <section id="section-calculator" class="tab-content hidden">
      <div id="calc-placeholder" class="text-center py-20 bg-[#11131e] rounded-2xl border border-slate-800">
        <span class="text-5xl block mb-4">🔍</span>
        <h3 class="text-xl font-bold text-slate-300">Персонаж не выбран</h3>
        <p class="text-slate-500 mt-2 max-w-sm mx-auto text-sm">Пожалуйста, перейдите на вкладку «Персонажи» и выберите героя для калькуляции.</p>
        <button onclick="switchTab('characters')" class="mt-6 px-5 py-2.5 bg-amber-500 text-slate-950 font-semibold rounded-xl hover:bg-amber-400 transition-all shadow-lg text-sm">
          Выбрать персонажа
        </button>
      </div>

      <div id="calc-container" class="hidden grid grid-cols-1 lg:grid-cols-3 gap-8">
        <!-- Левая часть: Настройки уровней и талантов -->
        <div class="lg:col-span-1 space-y-6">
          <div class="bg-[#11131e] p-6 rounded-2xl border border-slate-800 space-y-6 shadow-xl">
            <!-- Визуальная карточка активного героя -->
            <div id="calc-hero-badge" class="flex items-center gap-4 pb-6 border-b border-slate-800">
              <!-- Сюда запишется инфо активного героя -->
            </div>

            <!-- Уровни -->
            <div>
              <div class="flex justify-between items-center mb-4">
                <h4 class="text-sm font-bold text-amber-400 tracking-wider uppercase">Настройка уровней</h4>
              </div>
              <div class="space-y-4">
                <div>
                  <div class="flex justify-between text-xs font-semibold mb-1 text-slate-400">
                    <span>Текущий уровень:</span>
                    <span id="label-curr-lvl" class="text-slate-100">1</span>
                  </div>
                  <input type="range" id="input-curr-lvl" min="1" max="90" value="1" class="w-full h-1.5 bg-slate-800 rounded-lg appearance-none cursor-pointer accent-amber-400" oninput="updateLevels()">
                </div>
                <div>
                  <div class="flex justify-between text-xs font-semibold mb-1 text-slate-400">
                    <span>Целевой уровень:</span>
                    <span id="label-target-lvl" class="text-slate-100">90</span>
                  </div>
                  <input type="range" id="input-target-lvl" min="1" max="90" value="90" class="w-full h-1.5 bg-slate-800 rounded-lg appearance-none cursor-pointer accent-amber-400" oninput="updateLevels()">
                </div>
              </div>
            </div>

            <!-- Таланты -->
            <div>
              <h4 class="text-sm font-bold text-amber-400 tracking-wider uppercase mb-4">Настройка талантов</h4>
              <div class="space-y-4">
                <div>
                  <label class="block text-xs font-semibold text-slate-400 mb-1">Обычная атака:</label>
                  <div class="flex items-center gap-2">
                    <select id="talent-curr-1" class="bg-[#161925] border border-slate-800 text-sm rounded-lg p-2 w-full text-slate-200" onchange="recalculate()">
                      <!-- 1-10 options -->
                    </select>
                    <span class="text-slate-500">➔</span>
                    <select id="talent-target-1" class="bg-[#161925] border border-slate-800 text-sm rounded-lg p-2 w-full text-slate-200" onchange="recalculate()">
                      <!-- 1-10 options -->
                    </select>
                  </div>
                </div>

                <div>
                  <label class="block text-xs font-semibold text-slate-400 mb-1">Элементальный навык (Е):</label>
                  <div class="flex items-center gap-2">
                    <select id="talent-curr-2" class="bg-[#161925] border border-slate-800 text-sm rounded-lg p-2 w-full text-slate-200" onchange="recalculate()">
                      <!-- 1-10 options -->
                    </select>
                    <span class="text-slate-500">➔</span>
                    <select id="talent-target-2" class="bg-[#161925] border border-slate-800 text-sm rounded-lg p-2 w-full text-slate-200" onchange="recalculate()">
                      <!-- 1-10 options -->
                    </select>
                  </div>
                </div>

                <div>
                  <label class="block text-xs font-semibold text-slate-400 mb-1">Взрыв стихий (Q):</label>
                  <div class="flex items-center gap-2">
                    <select id="talent-curr-3" class="bg-[#161925] border border-slate-800 text-sm rounded-lg p-2 w-full text-slate-200" onchange="recalculate()">
                      <!-- 1-10 options -->
                    </select>
                    <span class="text-slate-500">➔</span>
                    <select id="talent-target-3" class="bg-[#161925] border border-slate-800 text-sm rounded-lg p-2 w-full text-slate-200" onchange="recalculate()">
                      <!-- 1-10 options -->
                    </select>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Правая часть: Результаты и Чекбоксы ресурсов -->
        <div class="lg:col-span-2 space-y-6">
          <div class="bg-[#11131e] p-6 rounded-2xl border border-slate-800 shadow-xl space-y-6">
            <div class="flex items-center justify-between flex-wrap gap-4">
              <div>
                <h3 class="text-xl font-bold">Сводный чек-лист ресурсов</h3>
                <p class="text-xs text-slate-400 mt-1">Отмечайте собранное. Прогресс сохраняется локально.</p>
              </div>
              <div class="flex items-center gap-4">
                <button onclick="resetCharacterProgress()" class="px-3 py-1.5 text-xs font-semibold bg-red-950/40 hover:bg-red-900/60 border border-red-800/60 rounded-xl text-red-300 transition-all">
                  Сбросить сбор
                </button>
                <div class="text-right">
                  <span id="checklist-progress" class="text-2xl font-extrabold text-emerald-400">0%</span>
                  <span class="block text-[10px] uppercase font-bold text-slate-500 tracking-wider">Прогресс сбора</span>
                </div>
              </div>
            </div>

            <!-- Шкала прогресса -->
            <div class="w-full bg-slate-800 h-2.5 rounded-full overflow-hidden">
              <div id="checklist-progress-bar" class="bg-gradient-to-r from-emerald-500 to-teal-400 h-full w-0 transition-all duration-300"></div>
            </div>

            <!-- Фильтры разделения ресурсов -->
            <div class="flex flex-wrap gap-1 bg-[#161925] p-1 rounded-xl border border-slate-800 self-start mb-2">
              <button id="btn-mats-all" onclick="filterMatsTab('all')" class="mats-filter-btn px-4 py-1.5 rounded-lg text-xs font-semibold transition-all bg-amber-500 text-slate-950 shadow-md">
                Все вместе
              </button>
              <button id="btn-mats-level" onclick="filterMatsTab('level')" class="mats-filter-btn px-4 py-1.5 rounded-lg text-xs font-semibold transition-all text-slate-400 hover:text-slate-100">
                Уровень и Возвышение
              </button>
              <button id="btn-mats-talents" onclick="filterMatsTab('talents')" class="mats-filter-btn px-4 py-1.5 rounded-lg text-xs font-semibold transition-all text-slate-400 hover:text-slate-100">
                Таланты героя
              </button>
            </div>

            <!-- Список ресурсов по категориям -->
            <div id="mats-list" class="space-y-4">
              <!-- Сюда динамически добавятся группы материалов -->
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Вкладка 3: Сборки -->
    <section id="section-builds" class="tab-content hidden">
      <div id="builds-placeholder" class="text-center py-20 bg-[#11131e] rounded-2xl border border-slate-800">
        <span class="text-5xl block mb-4">⚔️</span>
        <h3 class="text-xl font-bold text-slate-300">Сборка не открыта</h3>
        <p class="text-slate-500 mt-2 max-w-sm mx-auto text-sm">Пожалуйста, выберите героя на главной вкладке, чтобы увидеть гайд на артефакты и лучшее оружие.</p>
        <button onclick="switchTab('characters')" class="mt-6 px-5 py-2.5 bg-amber-500 text-slate-950 font-semibold rounded-xl hover:bg-amber-400 transition-all shadow-lg text-sm">
          Посмотреть сборки
        </button>
      </div>

      <div id="builds-container" class="hidden grid grid-cols-1 md:grid-cols-3 gap-8">
        <!-- Сюда JS вставит сборку выбранного персонажа -->
      </div>
    </section>

    <!-- Вкладка 4: Редактор базы данных -->
    <section id="section-editor" class="tab-content hidden">
      <div class="bg-[#11131e] p-6 rounded-2xl border border-slate-800 shadow-xl space-y-6">
        <div class="flex flex-col sm:flex-row justify-between items-start sm:items-center gap-4 pb-6 border-b border-slate-800">
          <div>
            <h2 class="text-2xl font-bold text-slate-100">⚙️ Редактор базы данных</h2>
            <p class="text-sm text-slate-400 mt-1">Отредактируйте материалы любого персонажа или создайте собственного героя с уникальными ресурсами.</p>
          </div>
          <div class="flex gap-2">
            <button onclick="initNewCharacterForm()" class="px-4 py-2 bg-emerald-600 hover:bg-emerald-500 text-white font-bold rounded-xl text-xs transition-all shadow-lg">
              + Новый персонаж
            </button>
            <button onclick="resetDbToDefault()" class="px-4 py-2 bg-red-950/40 hover:bg-red-900/60 border border-red-800/60 text-red-300 font-bold rounded-xl text-xs transition-all">
              Сбросить всю базу
            </button>
          </div>
        </div>

        <div class="grid grid-cols-1 lg:grid-cols-4 gap-8">
          <!-- Левая колонка редактора: Выбор редактируемого героя -->
          <div class="lg:col-span-1 space-y-4">
            <h3 class="text-sm font-bold text-amber-400 uppercase tracking-wider">Выберите для изменения</h3>
            <div id="editor-char-list" class="space-y-2 max-h-[500px] overflow-y-auto pr-2">
              <!-- Сюда JS выведет кнопки выбора персонажей -->
            </div>
          </div>

          <!-- Правая колонка редактора: Форма редактирования -->
          <div class="lg:col-span-3 bg-[#161925]/50 p-6 rounded-2xl border border-slate-800/80">
            <form id="editor-form" onsubmit="saveCharacterEdits(event)" class="space-y-6">
              <input type="hidden" id="edit-char-id">
              
              <!-- Основная информация -->
              <div>
                <h4 class="text-xs font-extrabold text-amber-400 uppercase tracking-wider mb-4 border-b border-slate-800 pb-2">1. Главные параметры</h4>
                <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
                  <div>
                    <label class="block text-xs text-slate-400 font-semibold mb-1">Имя (RU):</label>
                    <input type="text" id="edit-name" required class="w-full bg-[#0c0e17] border border-slate-800 rounded-lg p-2.5 text-sm text-slate-100 focus:outline-none focus:border-amber-400">
                  </div>
                  <div>
                    <label class="block text-xs text-slate-400 font-semibold mb-1">Стихия (Элемент):</label>
                    <select id="edit-element" class="w-full bg-[#0c0e17] border border-slate-800 rounded-lg p-2.5 text-sm text-slate-100 focus:outline-none focus:border-amber-400">
                      <option value="Hydro">Hydro 💧</option>
                      <option value="Pyro">Pyro 🔥</option>
                      <option value="Dendro">Dendro 🌿</option>
                      <option value="Electro">Electro ⚡</option>
                      <option value="Anemo">Anemo 🍃</option>
                      <option value="Geo">Geo ☄️</option>
                      <option value="Cryo">Cryo ❄️</option>
                    </select>
                  </div>
                  <div>
                    <label class="block text-xs text-slate-400 font-semibold mb-1">Редкость:</label>
                    <select id="edit-rarity" class="w-full bg-[#0c0e17] border border-slate-800 rounded-lg p-2.5 text-sm text-slate-100 focus:outline-none focus:border-amber-400">
                      <option value="5">5 Звезд ★★★★★</option>
                      <option value="4">4 Звезды ★★★★</option>
                    </select>
                  </div>
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4 mt-4">
                  <div>
                    <label class="block text-xs text-slate-400 font-semibold mb-1">Ссылка на иконку (Wiki URL):</label>
                    <input type="text" id="edit-image" placeholder="https://genshin-impact.fandom.com/wiki/..." class="w-full bg-[#0c0e17] border border-slate-800 rounded-lg p-2.5 text-xs text-slate-100 focus:outline-none focus:border-amber-400">
                  </div>
                  
                </div>
              </div>

              <!-- Материалы персонажа -->
              <div>
                <h4 class="text-xs font-extrabold text-amber-400 uppercase tracking-wider mb-4 border-b border-slate-800 pb-2">2. Карта ресурсов прокачки</h4>
                <p class="text-[11px] text-slate-400 mb-4">Вводите корректные названия ресурсов на английском, чтобы автоматически скачивались иконки!</p>
                
                <div class="p-4 bg-[#11131e] rounded-xl border border-slate-800/60 mb-6 space-y-4">
                  <span class="text-xs font-extrabold text-amber-400 uppercase block">💎 Кастомизация драгоценных камней стихии</span>
                  <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                    <div>
                      <label class="block text-[10px] text-slate-500 mb-1">Название серии камней (RU, Родительный падеж. Например: Агнидус / Варунада):</label>
                      <input type="text" id="edit-gem-series-ru" placeholder="Варунада" class="w-full bg-[#0c0e17] border border-slate-800 rounded-lg p-2 text-xs text-slate-100">
                    </div>
                    <div>
                      <label class="block text-[10px] text-slate-500 mb-1">Английский корень камня (EN. Например: Agnidus Agate / Varunada Lazurite):</label>
                      <input type="text" id="edit-gem-series-en" placeholder="Varunada Lazurite" class="w-full bg-[#0c0e17] border border-slate-800 rounded-lg p-2 text-xs text-slate-100">
                    </div>
                  </div>
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-2 gap-6">
                  <!-- Диковина -->
                  <div class="p-4 bg-[#11131e] rounded-xl border border-slate-800/60 space-y-3">
                    <span class="text-xs font-extrabold text-slate-400 uppercase">Местная диковина</span>
                    <div>
                      <label class="block text-[10px] text-slate-500 mb-1">Название на русском:</label>
                      <input type="text" id="edit-spec-ru" placeholder="Лилия озёрного света" required class="w-full bg-[#0c0e17] border border-slate-800/80 rounded-lg p-2 text-xs text-slate-100">
                    </div>
                    <div>
                      <label class="block text-[10px] text-slate-500 mb-1">На английском (для иконки):</label>
                      <input type="text" id="edit-spec-en" placeholder="Lakelight Lily" required class="w-full bg-[#0c0e17] border border-slate-800/80 rounded-lg p-2 text-xs text-slate-100">
                    </div>
                  </div>

                  <!-- Босс -->
                  <div class="p-4 bg-[#11131e] rounded-xl border border-slate-800/60 space-y-3">
                    <span class="text-xs font-extrabold text-slate-400 uppercase">Материал обычного босса</span>
                    <div>
                      <label class="block text-[10px] text-slate-500 mb-1">Название на русском:</label>
                      <input type="text" id="edit-boss-ru" placeholder="Очищающий родник" required class="w-full bg-[#0c0e17] border border-slate-800/80 rounded-lg p-2 text-xs text-slate-100">
                    </div>
                    <div>
                      <label class="block text-[10px] text-slate-500 mb-1">На английском (для иконки):</label>
                      <input type="text" id="edit-boss-en" placeholder="Water That Failed to Transcend" required class="w-full bg-[#0c0e17] border border-slate-800/80 rounded-lg p-2 text-xs text-slate-100">
                    </div>
                  </div>

                  <!-- Книги талантов -->
                  <div class="p-4 bg-[#11131e] rounded-xl border border-slate-800/60 space-y-3">
                    <span class="text-xs font-extrabold text-slate-400 uppercase">Серия книг талантов</span>
                    <div>
                      <label class="block text-[10px] text-slate-500 mb-1">Название серии на русском (в предложном падеже):</label>
                      <input type="text" id="edit-books-ru" placeholder="Справедливости" required class="w-full bg-[#0c0e17] border border-slate-800/80 rounded-lg p-2 text-xs text-slate-100">
                    </div>
                    <div>
                      <label class="block text-[10px] text-slate-500 mb-1">Оригинал на английском (без артикля, например: Justice):</label>
                      <input type="text" id="edit-books-en" placeholder="Justice" required class="w-full bg-[#0c0e17] border border-slate-800/80 rounded-lg p-2 text-xs text-slate-100">
                    </div>
                  </div>

                  <!-- Еженедельный босс -->
                  <div class="p-4 bg-[#11131e] rounded-xl border border-slate-800/60 space-y-3">
                    <span class="text-xs font-extrabold text-slate-400 uppercase">Материал еженедельного босса</span>
                    <div>
                      <label class="block text-[10px] text-slate-500 mb-1">Название на русском:</label>
                      <input type="text" id="edit-weekly-ru" placeholder="Темный глаз вихря" required class="w-full bg-[#0c0e17] border border-slate-800/80 rounded-lg p-2 text-xs text-slate-100">
                    </div>
                    <div>
                      <label class="block text-[10px] text-slate-500 mb-1">На английском (для иконки):</label>
                      <input type="text" id="edit-weekly-en" placeholder="Lightless Eye" required class="w-full bg-[#0c0e17] border border-slate-800/80 rounded-lg p-2 text-xs text-slate-100">
                    </div>
                  </div>
                </div>

                <div class="p-4 bg-[#11131e] rounded-xl border border-slate-800/60 mb-6 space-y-4">
                  <span class="text-xs font-extrabold text-amber-400 uppercase block">💎 Драгоценные камни стихии (4 уровня редкости)</span>
                  <p class="text-[10px] text-slate-400">Настройте названия камней вручную для соблюдения грамматики (например: Осколок..., Фрагмент..., Кусок..., Драгоценный...). Если оставить пустыми, применятся стандартные по стихии.</p>
                  
                  <div class="grid grid-cols-1 md:grid-cols-4 gap-4">
                    <!-- Тир 1 -->
                    <div class="space-y-2">
                      <span class="text-[11px] text-slate-400 font-bold">Осколок (2★)</span>
                      <input type="text" id="edit-gem1-ru" placeholder="Осколок лазурита Варунада" class="w-full bg-[#0c0e17] border border-slate-800 p-2 text-xs text-slate-100 rounded-lg">
                      <input type="text" id="edit-gem1-en" placeholder="Varunada Lazurite Sliver" class="w-full bg-[#0c0e17] border border-slate-800 p-2 text-xs text-slate-100 rounded-lg">
                    </div>
                    <!-- Тир 2 -->
                    <div class="space-y-2">
                      <span class="text-[11px] text-sky-400 font-bold">Фрагмент (3★)</span>
                      <input type="text" id="edit-gem2-ru" placeholder="Фрагмент лазурита Варунада" class="w-full bg-[#0c0e17] border border-slate-800 p-2 text-xs text-slate-100 rounded-lg">
                      <input type="text" id="edit-gem2-en" placeholder="Varunada Lazurite Fragment" class="w-full bg-[#0c0e17] border border-slate-800 p-2 text-xs text-slate-100 rounded-lg">
                    </div>
                    <!-- Тир 3 -->
                    <div class="space-y-2">
                      <span class="text-[11px] text-purple-400 font-bold">Кусок (4★)</span>
                      <input type="text" id="edit-gem3-ru" placeholder="Кусок лазурита Варунада" class="w-full bg-[#0c0e17] border border-slate-800 p-2 text-xs text-slate-100 rounded-lg">
                      <input type="text" id="edit-gem3-en" placeholder="Varunada Lazurite Chunk" class="w-full bg-[#0c0e17] border border-slate-800 p-2 text-xs text-slate-100 rounded-lg">
                    </div>
                    <!-- Тир 4 -->
                    <div class="space-y-2">
                      <span class="text-[11px] text-amber-400 font-bold">Драгоценный (5★)</span>
                      <input type="text" id="edit-gem4-ru" placeholder="Драгоценный лазурит Варунада" class="w-full bg-[#0c0e17] border border-slate-800 p-2 text-xs text-slate-100 rounded-lg">
                      <input type="text" id="edit-gem4-en" placeholder="Varunada Lazurite Gemstone" class="w-full bg-[#0c0e17] border border-slate-800 p-2 text-xs text-slate-100 rounded-lg">
                    </div>
                  </div>
                </div>

                <!-- Обычные мобы -->
                <div class="p-4 bg-[#11131e] rounded-xl border border-slate-800/60 mt-6 space-y-4">
                  <span class="text-xs font-extrabold text-slate-400 uppercase block">Материалы врагов (Обычный дроп — 3 уровня редкости)</span>
                  
                  <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
                    <!-- Уровень 1 -->
                    <div class="space-y-2">
                      <span class="text-[11px] text-emerald-400 font-bold">Обычный (Низкий ур.)</span>
                      <input type="text" id="edit-drop1-ru" placeholder="Нектар попрыгуньи (RU)" required class="w-full bg-[#0c0e17] border border-slate-800 p-2 text-xs text-slate-100 rounded-lg">
                      <input type="text" id="edit-drop1-en" placeholder="Whopperflower Nectar (EN)" required class="w-full bg-[#0c0e17] border border-slate-800 p-2 text-xs text-slate-100 rounded-lg">
                    </div>
                    <!-- Уровень 2 -->
                    <div class="space-y-2">
                      <span class="text-[11px] text-sky-400 font-bold">Улучшенный (Средний ур.)</span>
                      <input type="text" id="edit-drop2-ru" placeholder="Мерцающий нектар (RU)" required class="w-full bg-[#0c0e17] border border-slate-800 p-2 text-xs text-slate-100 rounded-lg">
                      <input type="text" id="edit-drop2-en" placeholder="Shimmering Nectar (EN)" required class="w-full bg-[#0c0e17] border border-slate-800 p-2 text-xs text-slate-100 rounded-lg">
                    </div>
                    <!-- Уровень 3 -->
                    <div class="space-y-2">
                      <span class="text-[11px] text-purple-400 font-bold">Редкий (Высокий ур.)</span>
                      <input type="text" id="edit-drop3-ru" placeholder="Элементальный нектар (RU)" required class="w-full bg-[#0c0e17] border border-slate-800 p-2 text-xs text-slate-100 rounded-lg">
                      <input type="text" id="edit-drop3-en" placeholder="Energy Nectar (EN)" required class="w-full bg-[#0c0e17] border border-slate-800 p-2 text-xs text-slate-100 rounded-lg">
                    </div>
                  </div>
                </div>
              </div>

              <!-- Билд персонажа -->
              <div>
                <h4 class="text-xs font-extrabold text-amber-400 uppercase tracking-wider mb-4 border-b border-slate-800 pb-2">3. Сборка (Билд)</h4>
                <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
                  <div>
                    <label class="block text-xs text-slate-400 font-semibold mb-1">Роль персонажа:</label>
                    <input type="text" id="edit-build-role" placeholder="Sub-DPS / Буфер" class="w-full bg-[#0c0e17] border border-slate-800 rounded-lg p-2.5 text-xs text-slate-100">
                  </div>
                  <div>
                    <label class="block text-xs text-slate-400 font-semibold mb-1">Лучший набор артефактов:</label>
                    <input type="text" id="edit-build-artifacts" placeholder="4x Золотая труппа" class="w-full bg-[#0c0e17] border border-slate-800 rounded-lg p-2.5 text-xs text-slate-100">
                  </div>
                </div>

                <div class="grid grid-cols-1 sm:grid-cols-3 gap-4 mt-4">
                  <div>
                    <label class="block text-[10px] text-slate-400 mb-1">Стат в Часах:</label>
                    <input type="text" id="edit-stat-sands" placeholder="HP% / Восстановление энергии%" class="w-full bg-[#0c0e17] border border-slate-800 rounded-lg p-2 text-xs text-slate-100">
                  </div>
                  <div>
                    <label class="block text-[10px] text-slate-400 mb-1">Стат в Кубке:</label>
                    <input type="text" id="edit-stat-goblet" placeholder="HP% / Гидро урон%" class="w-full bg-[#0c0e17] border border-slate-800 rounded-lg p-2 text-xs text-slate-100">
                  </div>
                  <div>
                    <label class="block text-[10px] text-slate-400 mb-1">Стат в Шапке:</label>
                    <input type="text" id="edit-stat-circlet" placeholder="Крит. урон / Крит. шанс" class="w-full bg-[#0c0e17] border border-slate-800 rounded-lg p-2 text-xs text-slate-100">
                  </div>
                </div>
              </div>

              <!-- Кнопка действия -->
              <div class="pt-4 flex justify-end">
                <button type="submit" class="px-6 py-3 bg-amber-500 hover:bg-amber-400 text-slate-950 font-bold rounded-xl text-sm transition-all shadow-lg flex items-center gap-2">
                  💾 Сохранить изменения
                </button>
              </div>

            </form>
          </div>
        </div>
      </div>
    </section>

  </main>

  <footer class="bg-[#11131e] border-t border-slate-800 py-6 mt-12">
    <div class="max-w-7xl mx-auto px-4 text-center text-xs text-slate-500 space-y-1">
      <p>© 2026 Genshin Companion. Данный сайт не является аффилированным с HoYoverse.</p>
      <p>Калькулятор ресурсов прокачки персонажей с оригинальным оформлением редкости материалов и официальными игровыми иконками.</p>
    </div>
  </footer>

  <!-- ЛОГИКА ПРИЛОЖЕНИЯ -->
  <script>
    // РЕАЛЬНЫЕ ДРАГОЦЕННЫЕ КАМНИ ДЛЯ ВСЕХ СТИХИЙ В ИГРЕ С ENGLISH ТРАНСЛЯЦИЕЙ
    const ELEMENTAL_GEMSTONES = {
      Hydro: {
        tier1: "Осколок лазурита Варунада",
        tier2: "Фрагмент лазурита Варунада",
        tier3: "Кусок лазурита Варунада",
        tier4: "Драгоценный лазурит Варунада",
        enRoot: "Varunada Lazurite",
        emoji: "💧"
      },
      Pyro: {
        tier1: "Осколок агата Агнидус",
        tier2: "Фрагмент агата Агнидус",
        tier3: "Кусок агата Агнидус",
        tier4: "Драгоценный агат Агнидус",
        enRoot: "Agnidus Agate",
        emoji: "🔥"
      },
      Dendro: {
        tier1: "Осколок изумруда Нагадус",
        tier2: "Фрагмент изумруда Нагадус",
        tier3: "Кусок изумруда Нагадус",
        tier4: "Драгоценный изумруд Нагадус",
        enRoot: "Nagadus Emerald",
        emoji: "🌿"
      },
      Electro: {
        tier1: "Осколок аметиста Ваджрада",
        tier2: "Фрагмент аметиста Ваджрада",
        tier3: "Кусок аметиста Ваджрада",
        tier4: "Драгоценный аметист Ваджрада",
        enRoot: "Vajrada Amethyst",
        emoji: "⚡"
      },
      Anemo: {
        tier1: "Осколок бирюзы Вайюда",
        tier2: "Фрагмент бирюзы Вайюда",
        tier3: "Кусок бирюзы Вайюда",
        tier4: "Драгоценная бирюза Вайюда",
        enRoot: "Vayuda Turquoise",
        emoji: "🍃"
      },
      Geo: {
        tier1: "Осколок топаза Притхиви",
        tier2: "Фрагмент топаза Притхиви",
        tier3: "Кусок топаза Притхиви",
        tier4: "Драгоценный топаз Притхиви",
        enRoot: "Prithivi Topaz",
        emoji: "☄️"
      },
      Cryo: {
        tier1: "Осколок нефрита Шивада",
        tier2: "Фрагмент нефрита Шивада",
        tier3: "Кусок нефрита Шивада",
        tier4: "Драгоценный нефрит Шивада",
        enRoot: "Shivada Jade",
        emoji: "❄️"
      }
    };

    function generateFallbackSVG(type, element, rarity) {
      const colors = {
        Hydro: { primary: "#38bdf8", secondary: "#0369a1" },
        Pyro: { primary: "#f87171", secondary: "#b91c1c" },
        Dendro: { primary: "#34d399", secondary: "#047857" },
        Electro: { primary: "#c084fc", secondary: "#6b21a8" },
        Anemo: { primary: "#2dd4bf", secondary: "#0f766e" },
        Geo: { primary: "#fbbf24", secondary: "#b45309" },
        Cryo: { primary: "#22d3ee", secondary: "#0369a1" }
      };

      const elColor = colors[element] || colors.Hydro;

      if (type === 'mora') {
        return `
          <svg viewBox="0 0 64 64" class="w-10 h-10 drop-shadow-md">
            <circle cx="32" cy="32" r="26" fill="#f59e0b" stroke="#d97706" stroke-width="3"/>
            <circle cx="32" cy="32" r="18" fill="none" stroke="#fef08a" stroke-width="2"/>
            <rect x="25" y="25" width="14" height="14" rx="2" fill="#78350f" stroke="#fef08a" stroke-width="2"/>
          </svg>
        `;
      }
      
      if (type === 'wit') {
        return `
          <svg viewBox="0 0 64 64" class="w-10 h-10 drop-shadow-md">
            <rect x="16" y="8" width="32" height="48" rx="4" fill="#ef4444" stroke="#b91c1c" stroke-width="3"/>
            <rect x="22" y="14" width="20" height="36" fill="none" stroke="#fca5a5" stroke-dasharray="4 2"/>
            <path d="M32 20 L35 28 L43 28 L37 33 L39 41 L32 36 L25 41 L27 33 L21 28 L29 28 Z" fill="#fbbf24"/>
          </svg>
        `;
      }

      if (type === 'crown') {
        return `
          <svg viewBox="0 0 64 64" class="w-10 h-10 drop-shadow-md">
            <path d="M10 44 L16 20 L26 32 L32 14 L38 32 L48 20 L54 44 Z" fill="#fbbf24" stroke="#d97706" stroke-width="3"/>
            <rect x="14" y="44" width="36" height="6" rx="1" fill="#d97706"/>
            <circle cx="16" cy="18" r="3" fill="#ef4444"/>
            <circle cx="32" cy="12" r="3" fill="#3b82f6"/>
            <circle cx="48" cy="18" r="3" fill="#ef4444"/>
          </svg>
        `;
      }

      // Element Gemstones (Sliver, Fragment, Chunk, Gemstone)
      let pathD = "M32 12 L46 32 L32 52 L18 32 Z"; // Diamond shard
      if (rarity === 3) pathD = "M32 10 Q48 25 32 54 Q16 25 32 10 Z"; // Droplet/Flame Cluster
      if (rarity >= 4) pathD = "M32 8 L48 24 L42 48 L22 48 L16 24 Z"; // Complex facet

      return `
        <svg viewBox="0 0 64 64" class="w-10 h-10 drop-shadow-md">
          <path d="${pathD}" fill="${elColor.primary}" stroke="${elColor.secondary}" stroke-width="3" stroke-linejoin="round"/>
          <circle cx="32" cy="30" r="6" fill="#ffffff" opacity="0.4" filter="blur(1px)"/>
        </svg>
      `;
    }

    // БАЗА ДАННЫХ ПЕРСОНАЖЕЙ С ОФИЦИАЛЬНЫМИ ИЗОБРАЖЕНИЯМИ И РЕАЛЬНЫМИ МАТЕРИАЛАМИ (RU И EN НАЗВАНИЯ ДЛЯ ПОЛУЧЕНИЯ ИКОНОК)
    const DEFAULT_CHARACTERS = [
      {
        "id": "furina",
        "name": "Фурина",
        "element": "Hydro",
        "rarity": 5,
        "emoji": "💧",
        "image": "https://genshin-impact.fandom.com/wiki/Special:FilePath/Furina_Icon.png",
        "color": "sky-400",
        "materials": {
          "boss_drop": { "ru": "Очищающий родник", "en": "Water That Failed to Transcend" },
          "local_specialty": { "ru": "Лилия озёрного света", "en": "Lakelight Lily" },
          "weekly_boss": { "ru": "Темный глаз вихря", "en": "Lightless Eye" },
          "book_series": { "ru": "Справедливости", "en": "Justice" },
          "enemy_drop": {
            "tier1": { "ru": "Нектар попрыгуньи", "en": "Whopperflower Nectar" },
            "tier2": { "ru": "Мерцающий нектар", "en": "Shimmering Nectar" },
            "tier3": { "ru": "Элементальный нектар", "en": "Energy Nectar" }
          }
        },
        "builds": {
          "role": "Sub-DPS / Карманный Аппликатор / Баффер",
          "weapons": [
            { "name": "Блеск тихих вод (5★)", "rank": "S+", "desc": "Сигнатурный меч. Огромные криты и бафф урона навыка." },
            { "name": "Переправа Флёв Сандр (4★)", "rank": "S (F2P)", "desc": "Лучший бесплатный вариант за рыбалку в Фонтейне. Дает восстановление энергии." },
            { "name": "Осквернённое желание (4★)", "rank": "S (Ивент)", "desc": "Старый ивентовый меч, дает шанс крита и ВЭ." }
          ],
          "artifacts": {
            "sets": ["4x Золотая труппа (Золотой стандарт для урона карманных фамильяров)"],
            "main_stats": {
              "sands": "HP% / Восстановление энергии%",
              "goblet": "HP% / Гидро урон%",
              "circlet": "Крит. урон / Крит. шанс"
            },
            "sub_stats": ["Крит. урон", "Крит. шанс", "Восстановление энергии (от 160% до 190%)", "HP%"]
          }
        }
      },
      {
        "id": "arlecchino",
        "name": "Арлекино",
        "element": "Pyro",
        "rarity": 5,
        "emoji": "🔥",
        "image": "https://genshin-impact.fandom.com/wiki/Special:FilePath/Arlecchino_Icon.png",
        "color": "red-400",
        "materials": {
          "boss_drop": { "ru": "Фрагмент золотой мелодии", "en": "Fragment of a Golden Melody" },
          "local_specialty": { "ru": "Радужная роза", "en": "Rainbow Rose" },
          "weekly_boss": { "ru": "Угасающая свеча", "en": "Fading Candle" },
          "book_series": { "ru": "Порядке", "en": "Order" },
          "enemy_drop": {
            "tier1": { "ru": "Шеврон рядового", "en": "Recruit's Chevron" },
            "tier2": { "ru": "Шеврон сержанта", "en": "Sergeant's Chevron" },
            "tier3": { "ru": "Шеврон офицера", "en": "Lieutenant's Chevron" }
          }
        },
        "builds": {
          "role": "Main-DPS (Основной урон на поле боя через Обычные атаки)",
          "weapons": [
            { "name": "Очертания алой луны (5★)", "rank": "S+", "desc": "Сигнатурная коса. Максимальный урон и уникальная механика Долга жизни." },
            { "name": "Нефритовый коршун (5★)", "rank": "S", "desc": "Стандартное копье, дает крит. шанс и сильный бафф силы атаки." },
            { "name": "Смертельный бой (4★)", "rank": "A (БП)", "desc": "Покупное копье из Боевого пропуска. Стабильный шанс крита." },
            { "name": "Белая кисть (3★)", "rank": "B (F2P)", "desc": "Лучшая дешевая альтернатива из сундуков Ли Юэ на урон обычных атак." }
          ],
          "artifacts": {
            "sets": ["4x Фрагменты гармонической фантазии (Топ-1)", "4x Конец гладиатора (Топ-2, если статы идеальные)"],
            "main_stats": {
              "sands": "Сила Атаки%",
              "goblet": "Пиро урон%",
              "circlet": "Крит. урон / Крит. шанс"
            },
            "sub_stats": ["Крит. шанс", "Крит. урон", "Сила Атаки%", "Мастерство стихий (если в реакциях парения)"]
          }
        }
      },
      {
        "id": "nahida",
        "name": "Нахида",
        "element": "Dendro",
        "rarity": 5,
        "emoji": "🌿",
        "image": "https://genshin-impact.fandom.com/wiki/Special:FilePath/Nahida_Icon.png",
        "color": "emerald-400",
        "materials": {
          "boss_drop": { "ru": "Подавленная лоза", "en": "Quelled Creeper" },
          "local_specialty": { "ru": "Гриб руккхашава", "en": "Rukkhashava Mushrooms" },
          "weekly_boss": { "ru": "Нити марионетки", "en": "Puppet Strings" },
          "book_series": { "ru": "Остроумии", "en": "Ingenuity" },
          "enemy_drop": {
            "tier1": { "ru": "Споры плесенника", "en": "Fungal Spores" },
            "tier2": { "ru": "Светящаяся пыльца", "en": "Luminescent Pollen" },
            "tier3": { "ru": "Пыльца кристаллизации", "en": "Crystalline Cyst Dust" }
          } 
        },
        "builds": {
          "role": "Дендро Драйвер / Саппорт / Карманный дамагер",
          "weapons": [
            { "name": "Сновидения тысячи ночей (5★)", "rank": "S+", "desc": "Дает колоссальное количество МС себе и команде." },
            { "name": "Песнь странника (4★)", "rank": "S", "desc": "Криты в доп. стате и рандомные убойные баффы при выходе на поле." },
            { "name": "Мемуары церемониального оружия (4★)", "rank": "A (F2P)", "desc": "Позволяет дважды прожать Е-шку и дает море МС." }
          ],
          "artifacts": {
            "sets": ["4x Воспоминания дремучего леса (Для среза Дендро резистов)", "4x Позолоченные сны (Для разгона МС до 1000)"],
            "main_stats": {
              "sands": "Мастерство стихий",
              "goblet": "Мастерство стихий / Дендро урон%",
              "circlet": "Мастерство стихий / Крит. шанс"
            },
            "sub_stats": ["Мастерство стихий", "Крит. шанс / Крит. урон", "Восстановление энергии", "Атака%"]
          }
        }
      },
      {
        "id": "neuvillette",
        "name": "Невиллет",
        "element": "Hydro",
        "rarity": 5,
        "emoji": "🐳",
        "image": "https://genshin-impact.fandom.com/wiki/Special:FilePath/Neuvillette_Icon.png",
        "color": "sky-400",
        "materials": {
          "boss_drop": { "ru": "Рог единорога", "en": "Fontemer Unihorn" },
          "local_specialty": { "ru": "Темнозвездная ракушка", "en": "Lumitoile" },
          "weekly_boss": { "ru": "Вечный янтарь", "en": "Everamber" },
          "book_series": { "ru": "Беспристрастии", "en": "Equity" },
          "enemy_drop": {
            "tier1": { "ru": "Жемчужина инородца", "en": "Transoceanic Pearl" },
            "tier2": { "ru": "Обломок расщелины", "en": "Transoceanic Chunk" },
            "tier3": { "ru": "Ксенохромный кристалл", "en": "Xenochromatic Crystal" }
          }
        },
        "builds": {
          "role": "Гидро Гиперкерри (Убойный урон заряженными атаками-гидропушкой)",
          "weapons": [
            { "name": "Обряд вечного течения (5★)", "rank": "S+", "desc": "Максимальный урон и восстановление энергии от изменения здоровья." },
            { "name": "Жертвенный нефрит (4★)", "rank": "S (БП)", "desc": "Колоссальный бафф здоровья и крит. шанса при нахождении в кармане." },
            { "name": "Янтарь прототипа (4★)", "rank": "A (Крафт)", "desc": "Лучший бесплатный крафтовый катализатор. Лечит отряд и дает ВЭ." }
          ],
          "artifacts": {
            "sets": ["4x Охотник Сумеречного двора (Безусловный Топ-1, бесплатно дает 36% шанса крита)"],
            "main_stats": {
              "sands": "HP%",
              "goblet": "Гидро урон% / HP%",
              "circlet": "Крит. урон"
            },
            "sub_stats": ["Крит. урон", "HP%", "Восстановление энергии (около 120-130%)", "Крит. шанс"]
          }
        }
      },
      {
        "id": "raiden",
        "name": "Райдэн",
        "element": "Electro",
        "rarity": 5,
        "emoji": "⚡",
        "image": "https://genshin-impact.fandom.com/wiki/Special:FilePath/Raiden_Shogun_Icon.png",
        "color": "purple-400",
        "materials": {
          "boss_drop": { "ru": "Штормовой жемчуг", "en": "Storm Beads" },
          "local_specialty": { "ru": "Плод облачной травы", "en": "Amakumo Fruit" },
          "weekly_boss": { "ru": "Расплавленный миг", "en": "Molten Moment" },
          "book_series": { "ru": "Свете", "en": "Light" },
          "enemy_drop": {
            "tier1": { "ru": "Старая гарда", "en": "Old Handguard" },
            "tier2": { "ru": "Гарда кагэути", "en": "Kageuchi Handguard" },
            "tier3": { "ru": "Прославленная гарда", "en": "Famed Handguard" }
          }
        },
        "builds": {
          "role": "Реактор / Драйвер / Баффер ульты",
          "weapons": [
            { "name": "Сияющая жатва (5★)", "rank": "S+", "desc": "Дает космический прирост силы атаки от твоего восстановления энергии." },
            { "name": "«Улов» (4★)", "rank": "S (F2P)", "desc": "Копье за рыбалку в Инадзуме. Баффает урон и шанс крита ультимейта." },
            { "name": "Гроза драконов (4★)", "rank": "A (Бутон)", "desc": "Для сборки исключительно в Дендро вегетацию (на Мастерство стихий)." }
          ],
          "artifacts": {
            "sets": ["4x Эмблема рассечённой судьбы (Единственный верный сет для классической сборки)"],
            "main_stats": {
              "sands": "Восстановление энергии%",
              "goblet": "Сила Атаки% / Электро урон%",
              "circlet": "Крит. шанс / Крит. урон"
            },
            "sub_stats": ["Восстановление энергии (до 250%+)", "Крит. шанс", "Крит. урон", "Атака%"]
          }
        }
      },
      {
        "id": "zhongli",
        "name": "Чжун Ли",
        "element": "Geo",
        "rarity": 5,
        "emoji": "☄️",
        "image": "https://genshin-impact.fandom.com/wiki/Special:FilePath/Zhongli_Icon.png",
        "color": "amber-500",
        "materials": {
          "boss_drop": { "ru": "Базальтовая колонна", "en": "Basalt Pillar" },
          "local_specialty": { "ru": "Кор ляпис", "en": "Cor Lapis" },
          "weekly_boss": { "ru": "Корона лорда драконов", "en": "Dragon Lord's Crown" },
          "book_series": { "ru": "Золоте", "en": "Gold" },
          "enemy_drop": {
            "tier1": { "ru": "Слизь слайма", "en": "Slime Condensate" },
            "tier2": { "ru": "Выделения слайма", "en": "Slime Secretions" },
            "tier3": { "ru": "Концентрат слайма", "en": "Slime Concentrate" }
          }
        },
        "builds": {
          "role": "Лучший щитовик игры / Срез резистов",
          "weapons": [
            { "name": "Посох Хомы (5★)", "rank": "A", "desc": "Вариант для сборки в гибридный урон от ульты (планетария)." },
            { "name": "Черная кисть (3★)", "rank": "S (F2P)", "desc": "Удивительно, но это 3★ копье дает больше всего HP% для максимальной прочности щита." }
          ],
          "artifacts": {
            "sets": ["4x Стойкость Миллелита (Баффает атаку союзников от попаданий колонны)"],
            "main_stats": {
              "sands": "HP%",
              "goblet": "HP% (для щита) / Гео урон%",
              "circlet": "HP% / Крит. шанс"
            },
            "sub_stats": ["HP%", "HP (числовое)", "Восстановление энергии", "Крит. шанс"]
          }
        }
      },
      {
        "id": "kazuha",
        "name": "Кадзуха",
        "element": "Anemo",
        "rarity": 5,
        "emoji": "🍃",
        "image": "https://genshin-impact.fandom.com/wiki/Special:FilePath/Kaedehara_Kazuha_Icon.png",
        "color": "teal-400",
        "materials": {
          "boss_drop": { "ru": "Ядро кукольного устройства", "en": "Marionette Core" },
          "local_specialty": { "ru": "Морской гриб", "en": "Sea Ganoderma" },
          "weekly_boss": { "ru": "Позолоченная чешуя", "en": "Gilded Scale" },
          "book_series": { "ru": "Усердии", "en": "Diligence" },
          "enemy_drop": {
            "tier1": { "ru": "Печать похитителей сокровищ", "en": "Treasure Hoarder Insignia" },
            "tier2": { "ru": "Печать серебряного ворона", "en": "Silver Raven Insignia" },
            "tier3": { "ru": "Печать золотого ворона", "en": "Golden Raven Insignia" }
          }
        },
        "builds": {
          "role": "Anemo стяжка / Баффер стихий / Урон по площади",
          "weapons": [
            { "name": "Клятва свободы (5★)", "rank": "S+", "desc": "Сигнатурный меч. Мощные баффы силы атаки команды и куча МС." },
            { "name": "Ксифос взаимного согласия (4★)", "rank": "S", "desc": "Прекрасный меч на МС, конвертирует его в восстановление энергии для всей команды." },
            { "name": "Стальное жало (4★)", "rank": "A (Крафт)", "desc": "Базовый бесплатный крафтовый меч на Мастерство Стихий." }
          ],
          "artifacts": {
            "sets": ["4x Изумрудная тень (Снижает сопротивление врагов к раздуваемой стихии на 40%)"],
            "main_stats": {
              "sands": "Мастерство стихий / Восстановление энергии",
              "goblet": "Мастерство стихий",
              "circlet": "Мастерство стихий"
            },
            "sub_stats": ["Мастерство стихий", "Восстановление энергии (желательно от 160% и выше)", "Крит. шанс (под Фавоний)"]
          }
        }
      },
      {
        "id": "ayaka",
        "name": "Аяка",
        "element": "Cryo",
        "rarity": 5,
        "emoji": "❄️",
        "image": "https://genshin-impact.fandom.com/wiki/Special:FilePath/Kamisato_Ayaka_Icon.png",
        "color": "cyan-400",
        "materials": {
          "boss_drop": { "ru": "Сердце бесконечного механизма", "en": "Perpetual Heart" },
          "local_specialty": { "ru": "Цвет сакуры", "en": "Sakura Bloom" },
          "weekly_boss": { "ru": "Кровь нефрита", "en": "Bloodjade Branch" },
          "book_series": { "ru": "Изяществе", "en": "Elegance" },
          "enemy_drop": {
            "tier1": { "ru": "Старая гарда", "en": "Old Handguard" },
            "tier2": { "ru": "Гарда кагэути", "en": "Kageuchi Handguard" },
            "tier3": { "ru": "Прославленная гарда", "en": "Famed Handguard" }
          }
        },
        "builds": {
          "role": "Крио Main-DPS (Главный дамагер через Крио инфузию и ульт)",
          "weapons": [
            { "name": "Рассекающий туман (5★)", "rank": "S+", "desc": "Сигнатурный меч с огромным Крит. уроном и бонусом ко всем элементам." },
            { "name": "Амэнома Кагэути (4★)", "rank": "S (F2P)", "desc": "Лучший крафтовый меч. Облегчает набор ультимейта по КД." },
            { "name": "Черногорский длинный меч (4★)", "rank": "A (Магазин)", "desc": "Дает отличный Крит. урон, покупается в магазине Паймон за блеск." }
          ],
          "artifacts": {
            "sets": ["4x Заблудший в метели (Позволяет почти полностью забыть про шанс крита в статусах заморозки)"],
            "main_stats": {
              "sands": "Сила Атаки%",
              "goblet": "Крио урон%",
              "circlet": "Крит. урон"
            },
            "sub_stats": ["Крит. урон", "Сила Атаки%", "Восстановление энергии (около 130-140%)", "Крит. шанс (до 30-40% максимум)"]
          }
        }
      },
      {
        "id": "kaeya",
        "name": "Кэйа",
        "element": "Cryo",
        "rarity": 4,
        "emoji": "❄️",
        "image": "https://genshin-impact.fandom.com/wiki/Special:FilePath/Kaeya_Icon.png",
        "color": "cyan-400",
        "materials": {
          "boss_drop": { "ru": "Инеевое ядро", "en": "Hoar­frost Core" },
          "local_specialty": { "ru": "Лилия калла", "en": "Calla Lily" },
          "weekly_boss": { "ru": "Шкатулка с духом Борея", "en": "Spirit Locket of Boreas" },
          "book_series": { "ru": "Поэзии", "en": "Ballad" },
          "enemy_drop": {
            "tier1": { "ru": "Печать Похитителей сокровищ", "en": "Treasure Hoarder Insignia" },
            "tier2": { "ru": "Печать серебряного ворона", "en": "Silver Raven Insignia" },
            "tier3": { "ru": "Печать золотого ворона", "en": "Golden Raven Insignia" }
          }
        },
        "builds": {
          "role": "Крио Main-DPS (Он выполняет роль карманного DPS героя, который способен оказывать поддержку остальному отряду, дамажа элементальным навыком на поле, а также активировать взрыв стихий и уходить из битвы. Кроме того, он может самостоятельно бить с руки, находясь в сражении большое количество времени. Сборка Кэйи сильно зависит от его роли в отряде, а также на самого состава команды.)",
          "weapons": [
            { "name": "Драгоценный омут (5★)", "rank": "S+", "desc": "Увеличивает HP на 20-40% Также дает бонус атаки, равный 1,2-2,4% от макс. HP экипированного этим оружием персонажа." },
            { "name": "Переправа Флев Сандре (4★)", "rank": "S (F2P)", "desc": "Увеличивает шанс крит. попадания элементального навыка на 8-16%. Кроме того, после применения элементального навыка восстановление энергии повышается на 16-32% на 5 сек." },
            { "name": "Церемониальный меч", "rank": "A", "desc": "Попадание по врагу элементальным навыком с шансом в 40-80% может мгновенно откатить время восстановления данного скилла. Эффект срабатывает раз в 30-16 секунд." }
          ],
          "artifacts": {
            "sets": ["4x Заблудший в метели (Позволяет почти полностью забыть про шанс крита в статусах заморозки), 4x Эмблема рассеченной судьбы (Увеличивает урон взрыва стихии на величину, равную 25% от значения восстановления энергии. Эффект можно увеличить максимум до 75%), 4x Церемония древней знати (Активация взрыва стихии увеличивает силу атаки всех членов отряда на 20% в течении 12 сек.)"],
            "main_stats": {
              "sands": "Сила Атаки%",
              "goblet": "Крио урон%",
              "circlet": "Крит. урон"
            },
            "sub_stats": ["Крит. урон", "Сила Атаки%", "Восстановление энергии", "Крит. шанс"]
          }
        }
      },
      {
        "id": "amber",
        "name": "Эмбер",
        "element": "Pyro",
        "rarity": 4,
        "emoji": "🔥",
        "image": "https://genshin-impact.fandom.com/wiki/Special:FilePath/Amber_Icon.png",
        "color": "red-400",
        "materials": {
          "boss_drop": { "ru": "Пылающее семя", "en": "Ever­flame Seed" },
          "local_specialty": { "ru": "Трава-светяшка", "en": "Small Lamp Grass" },
          "weekly_boss": { "ru": "Вздох Двалина", "en": "Dvalin's Sigh" },
          "book_series": { "ru": "Свободе", "en": "Freedom" },
          "enemy_drop": {
            "tier1": { "ru": "рочный наконечник стрелы", "en": "Firm Arrowhead" },
            "tier2": { "ru": "Острый наконечник стрелы", "en": "Sharp Arrowhead" },
            "tier3": { "ru": "Старый наконечник стрелы", "en": "Weathered Arrowhead" }
          }
        },
        "builds": {
          "role": "Sub-DPS ( Наносит урон вне поля (призывает существ, Пиро-торнадо и т. д.), следует за основным дамагером и помогает создавать реакции)",
          "weapons": [
            { "name": "Лук Амоса (5★)", "rank": "S+", "desc": "Увеличивает повреждения от обычных и заряженных атак на 12%. Чем дольше летит стрела, тем больше она наносит урона." },
            { "name": "Небесное крыло (5★)", "rank": "S", "desc": "Повышает критический урон на 20% и с вероятностью 60% наносит 125% повреждений противникам, которые находятся неподалёку." },
            { "name": "Прототип: Полумесяц (4★)", "rank": "A", "desc": "При успешной заряженной атаке по уязвимым местам противника скорость перемещения персонажа повышается на 10%, а сила удара — на 36%." },
            { "name": "Посыльный  (3★)", "rank": "B", "desc": "При успешной заряженной атаке по слабым местам противника персонаж наносит дополнительные 100% критического урона." }
          ],
          "artifacts": {
            "sets": ["4x Церемония древней знати", "4x Позолоченные сны, 2x Горящая алая ведьма"],
            "main_stats": {
              "sands": "Сила Атаки%",
              "goblet": "Пиро урон%",
              "circlet": "Крит. урон / Крит. шанс"
            },
            "sub_stats": ["Крит. шанс", "Крит. урон", "Сила Атаки%", "Мастерство стихий"]
          }
        }
      }      
  ];  

    // Глобальное состояние
    let selectedChar = null;
    let currentTab = 'characters';
    let CHARACTERS_DATABASE = [];
    let activeMatsTab = 'all'; // Хранит активный фильтр ресурсов

    // Загрузка динамической базы из LocalStorage
    function initDatabase() {
      const storedDb = localStorage.getItem('genshin_custom_db');
      if (storedDb) {
        try {
          CHARACTERS_DATABASE = JSON.parse(storedDb);
        } catch (e) {
          CHARACTERS_DATABASE = [...DEFAULT_CHARACTERS];
        }
      } else {
        CHARACTERS_DATABASE = [...DEFAULT_CHARACTERS];
      }
    }

    // Сохранение базы в LocalStorage
    function saveDatabase() {
      localStorage.setItem('genshin_custom_db', JSON.stringify(CHARACTERS_DATABASE));
    }

    // Сброс базы к заводским настройкам
    function resetDbToDefault() {
      if (confirm("Вы уверены, что хотите восстановить базу данных по умолчанию? Все созданные вами персонажи и изменения будут удалены!")) {
        localStorage.removeItem('genshin_custom_db');
        initDatabase();
        renderCharactersGrid();
        renderEditorCharList();
        switchTab('characters');
      }
    }

    // МАТЕМАТИКА Genshin (Стоимость повышения уровней и талантов)
    function calculateRequirements(start, target, talCurrent, talTarget) {
      // Инициализируем отдельные требования для Уровней
      let lvlMora = 0;
      let heroWit = 0;
      let bossDrop = 0;
      let specialty = 0;
      let lvlCommonDrop = { tier1: 0, tier2: 0, tier3: 0 };
      let gemstoneCount = { tier1: 0, tier2: 0, tier3: 0, tier4: 0 };

      // Инициализируем отдельные требования для Талантов
      let talMora = 0;
      let talentBooks = { tier1: 0, tier2: 0, tier3: 0 };
      let talCommonDrop = { tier1: 0, tier2: 0, tier3: 0 };
      let talentWeekly = 0;
      let talentCrown = 0;

      // Константы уровней (возвышение + прокачка)
      const milestones = [
        { lvl: 20, mora: 20000, sliver: 1, fragment: 0, chunk: 0, gemstone: 0, boss: 0, specialty: 3, tier1: 3, tier2: 0, tier3: 0 },
        { lvl: 40, mora: 40000, sliver: 0, fragment: 3, chunk: 0, gemstone: 0, boss: 2, specialty: 10, tier1: 15, tier2: 0, tier3: 0 },
        { lvl: 50, mora: 60000, sliver: 0, fragment: 6, chunk: 0, gemstone: 0, boss: 4, specialty: 20, tier1: 0, tier2: 12, tier3: 0 },
        { lvl: 60, mora: 80000, sliver: 0, fragment: 0, chunk: 3, gemstone: 0, boss: 8, specialty: 30, tier1: 0, tier2: 18, tier3: 0 },
        { lvl: 70, mora: 100000, sliver: 0, fragment: 0, chunk: 6, gemstone: 0, boss: 12, specialty: 45, tier1: 0, tier2: 0, tier3: 12 },
        { lvl: 80, mora: 120000, sliver: 0, fragment: 0, chunk: 0, gemstone: 6, boss: 20, specialty: 60, tier1: 0, tier2: 0, tier3: 24 }
      ];

      // 1. Расчет уровней
      const levelsToCover = Math.max(0, target - start);
      const stepCostWit = 4.6; 
      const stepCostMora = 18500;

      heroWit += Math.round(levelsToCover * stepCostWit);
      lvlMora += Math.round(levelsToCover * stepCostMora);

      milestones.forEach(m => {
        if (start < m.lvl && target >= m.lvl) {
          lvlMora += m.mora;
          bossDrop += m.boss;
          specialty += m.specialty;
          
          gemstoneCount.tier1 += m.sliver;
          gemstoneCount.tier2 += m.fragment;
          gemstoneCount.tier3 += m.chunk;
          gemstoneCount.tier4 += m.gemstone;

          lvlCommonDrop.tier1 += m.tier1 || 0;
          lvlCommonDrop.tier2 += m.tier2 || 0;
          lvlCommonDrop.tier3 += m.tier3 || 0;
        }
      });

      // Константы повышения талантов
      const talentSteps = [
        { from: 1, to: 2, mora: 12500, books: { tier1: 3, tier2: 0, tier3: 0 }, common: { tier1: 6, tier2: 0, tier3: 0 }, weekly: 0, crown: 0 },
        { from: 2, to: 3, mora: 17500, books: { tier1: 0, tier2: 2, tier3: 0 }, common: { tier1: 0, tier2: 3, tier3: 0 }, weekly: 0, crown: 0 },
        { from: 3, to: 4, mora: 25000, books: { tier1: 0, tier2: 4, tier3: 0 }, common: { tier1: 0, tier2: 4, tier3: 0 }, weekly: 0, crown: 0 },
        { from: 4, to: 5, mora: 30000, books: { tier1: 0, tier2: 6, tier3: 0 }, common: { tier1: 0, tier2: 6, tier3: 0 }, weekly: 0, crown: 0 },
        { from: 5, to: 6, mora: 37500, books: { tier1: 0, tier2: 9, tier3: 0 }, common: { tier1: 0, tier2: 9, tier3: 0 }, weekly: 0, crown: 0 },
        { from: 6, to: 7, mora: 120000, books: { tier1: 0, tier2: 0, tier3: 4 }, common: { tier1: 0, tier2: 0, tier3: 4 }, weekly: 1, crown: 0 },
        { from: 7, to: 8, mora: 260000, books: { tier1: 0, tier2: 0, tier3: 6 }, common: { tier1: 0, tier2: 0, tier3: 6 }, weekly: 1, crown: 0 },
        { from: 8, to: 9, mora: 450000, books: { tier1: 0, tier2: 0, tier3: 12 }, common: { tier1: 0, tier2: 0, tier3: 9 }, weekly: 2, crown: 0 },
        { from: 9, to: 10, mora: 700000, books: { tier1: 0, tier2: 0, tier3: 16 }, common: { tier1: 0, tier2: 0, tier3: 12 }, weekly: 2, crown: 1 }
      ];

      // 2. Расчет талантов
      for (let t = 0; t < 3; t++) {
        const currentT = talCurrent[t];
        const targetT = talTarget[t];
        
        talentSteps.forEach(step => {
          if (currentT <= step.from && targetT >= step.to) {
            talMora += step.mora;
            talentBooks.tier1 += step.books.tier1;
            talentBooks.tier2 += step.books.tier2;
            talentBooks.tier3 += step.books.tier3;
            
            talCommonDrop.tier1 += step.common.tier1;
            talCommonDrop.tier2 += step.common.tier2;
            talCommonDrop.tier3 += step.common.tier3;

            talentWeekly += step.weekly;
            talentCrown += step.crown;
          }
        });
      }

      // Возвращаем разделенные структуры
      return {
        level: { mora: lvlMora, heroWit, bossDrop, specialty, commonDrop: lvlCommonDrop, gemstoneCount },
        talents: { mora: talMora, talentBooks, commonDrop: talCommonDrop, talentWeekly, talentCrown }
      };
    }

    // ИНИЦИАЛИЗАЦИЯ И ТАБЫ
    function switchTab(tabName) {
      currentTab = tabName;
      document.querySelectorAll('.tab-content').forEach(section => {
        section.classList.add('hidden');
      });
      
      const activeSection = document.getElementById(`section-${tabName}`);
      if (activeSection) activeSection.classList.remove('hidden');

      // Обновляем визуальные классы кнопок меню
      document.querySelectorAll('.menu-btn').forEach(btn => {
        btn.className = "menu-btn px-4 py-2 rounded-lg text-sm font-semibold text-slate-400 hover:text-slate-100 transition-all duration-200";
      });

      const activeBtn = document.getElementById(`btn-${tabName}`);
      if (activeBtn) {
        activeBtn.className = "menu-btn px-4 py-2 rounded-lg text-sm font-semibold transition-all duration-200 bg-amber-500 text-slate-950 shadow-lg";
      }

      if (tabName === 'editor') {
        renderEditorCharList();
      }
    }

    // Загрузка грида персонажей с красивыми золотыми звездами
    function renderCharactersGrid(list = CHARACTERS_DATABASE) {
      const grid = document.getElementById("characters-grid");
      grid.innerHTML = "";

      list.forEach(char => {
        const card = document.createElement("div");
        card.className = "group relative bg-[#11131e] border border-slate-800 rounded-2xl p-4 text-center cursor-pointer hover:border-amber-400/50 hover:shadow-xl hover:shadow-amber-500/5 transition-all duration-300 transform hover:-translate-y-1.5";
        
        let borderEl = 'border-l-4';
        if (char.element === 'Hydro') borderEl += ' border-l-sky-500';
        else if (char.element === 'Pyro') borderEl += ' border-l-red-500';
        else if (char.element === 'Dendro') borderEl += ' border-l-emerald-500';
        else if (char.element === 'Electro') borderEl += ' border-l-purple-500';
        else if (char.element === 'Anemo') borderEl += ' border-l-teal-400';
        else if (char.element === 'Geo') borderEl += ' border-l-amber-600';
        else if (char.element === 'Cryo') borderEl += ' border-l-cyan-400';

        const starStars = '★'.repeat(char.rarity);

        card.innerHTML = `
          <div class="absolute inset-0 rounded-2xl ${borderEl} opacity-80"></div>
          
          <div class="relative w-24 h-24 mx-auto mb-4 mt-1 rounded-full overflow-hidden border-2 border-slate-700/60 bg-[#161925] group-hover:border-amber-400 transition-all duration-300 shadow-lg flex items-center justify-center">
            <!-- Официальная иконка игры -->
            <img src="${char.image}" alt="${char.name}" class="w-full h-full object-cover" onerror="this.style.display='none'; this.nextElementSibling.style.display='flex';">
            <!-- Резервный эмодзи -->
            <div class="absolute inset-0 hidden items-center justify-center text-4xl bg-[#161925]">${char.emoji}</div>
          </div>
          
          <h3 class="font-extrabold text-slate-100 text-base group-hover:text-amber-400 transition-colors">${char.name}</h3>
          <div class="text-xs font-semibold text-slate-400 mt-1 flex flex-col gap-1 items-center">
            <span>${char.element}</span>
            <span class="text-amber-400 tracking-wider text-sm leading-none">${starStars}</span>
          </div>
        `;

        card.onclick = () => {
          selectCharacter(char);
        };

        grid.appendChild(card);
      });
    }

    // Фильтр по стихиям
    function filterElements(elem) {
      document.querySelectorAll('.element-filter-btn').forEach(btn => {
        btn.className = "element-filter-btn px-3 py-1.5 text-xs font-semibold rounded-lg hover:bg-slate-800 text-slate-400";
      });
      event.target.className = "element-filter-btn px-3 py-1.5 text-xs font-semibold rounded-lg bg-slate-800 text-amber-400";

      if (elem === 'all') {
        renderCharactersGrid(CHARACTERS_DATABASE);
      } else {
        const filtered = CHARACTERS_DATABASE.filter(c => c.element === elem);
        renderCharactersGrid(filtered);
      }
    }

    // Выбор конкретного персонажа
    function selectCharacter(char) {
      selectedChar = char;

      document.getElementById("calc-placeholder").classList.add("hidden");
      document.getElementById("calc-container").classList.remove("hidden");
      
      document.getElementById("builds-placeholder").classList.add("hidden");
      document.getElementById("builds-container").classList.remove("hidden");

      // Сбрасываем фильтр материалов при смене персонажа
      filterMatsTab('all');

      // Рендерим плашку с превью персонажа
      const badge = document.getElementById("calc-hero-badge");
      badge.innerHTML = `
        <div class="relative w-16 h-16 rounded-full border-2 border-slate-700 bg-[#161925] flex items-center justify-center shadow-md">
          <img src="${char.image || ''}" alt="${char.name}" class="w-full h-full object-cover rounded-full" onerror="this.style.display='none'; this.nextElementSibling.style.display='flex';">
          <div class="absolute inset-0 hidden items-center justify-center text-3xl bg-[#161925] rounded-full">${char.emoji || '✨'}</div>
          <!-- Круглый бейдж эмодзи -->
          <div class="absolute -top-1 -right-1 w-6 h-6 bg-slate-900 border border-slate-700 rounded-full flex items-center justify-center text-xs shadow-sm z-20">
            ${char.emoji || '✨'}
          </div>
        </div>
        <div>
          <h3 class="text-lg font-extrabold text-slate-100">${char.name}</h3>
          <span class="inline-block text-[10px] uppercase tracking-wider font-extrabold bg-slate-800 text-slate-400 px-2 py-0.5 rounded-full mt-1">${char.element}</span>
        </div>
      `;

      populateTalentSelectors();

      // Настройки уровней
      document.getElementById("input-curr-lvl").value = 1;
      document.getElementById("input-target-lvl").value = 90;
      updateLevels();

      renderBuildCard(char);
      switchTab("calculator");
    }

    // Переключение разделов чек-листа ресурсов
    function filterMatsTab(tabName) {
      activeMatsTab = tabName;

      // Обновляем визуальное выделение кнопок фильтрации ресурсов
      document.querySelectorAll('.mats-filter-btn').forEach(btn => {
        btn.className = "mats-filter-btn px-4 py-1.5 rounded-lg text-xs font-semibold transition-all text-slate-400 hover:text-slate-100";
      });

      const activeBtn = document.getElementById(`btn-mats-${tabName}`);
      if (activeBtn) {
        activeBtn.className = "mats-filter-btn px-4 py-1.5 rounded-lg text-xs font-semibold transition-all bg-amber-500 text-slate-950 shadow-md";
      }

      recalculate();
    }

    // Наполнение дропдаунов талантов
    function populateTalentSelectors() {
      const selects = [
        "talent-curr-1", "talent-target-1",
        "talent-curr-2", "talent-target-2",
        "talent-curr-3", "talent-target-3"
      ];

      selects.forEach(id => {
        const select = document.getElementById(id);
        select.innerHTML = "";
        const isTarget = id.includes("target");
        
        for (let i = 1; i <= 10; i++) {
          const opt = document.createElement("option");
          opt.value = i;
          opt.text = `Ур. ${i}`;
          if (isTarget && i === 10) opt.selected = true;
          select.appendChild(opt);
        }
      });
    }

    // Обновление лейблов уровней
    function updateLevels() {
      let start = parseInt(document.getElementById("input-curr-lvl").value);
      let target = parseInt(document.getElementById("input-target-lvl").value);

      if (target < start) {
        target = start;
        document.getElementById("input-target-lvl").value = target;
      }

      document.getElementById("label-curr-lvl").innerText = start;
      document.getElementById("label-target-lvl").innerText = target;

      recalculate();
    }

    // Функция пересчета ресурсов и отрисовки чек-листа
    function recalculate() {
      if (!selectedChar) return;

      const currLvl = parseInt(document.getElementById("input-curr-lvl").value);
      const targetLvl = parseInt(document.getElementById("input-target-lvl").value);

      const talCurr = [
        parseInt(document.getElementById("talent-curr-1").value),
        parseInt(document.getElementById("talent-curr-2").value),
        parseInt(document.getElementById("talent-curr-3").value)
      ];

      const talTarget = [
        parseInt(document.getElementById("talent-target-1").value),
        parseInt(document.getElementById("talent-target-2").value),
        parseInt(document.getElementById("talent-target-3").value)
      ];

      const req = calculateRequirements(currLvl, targetLvl, talCurr, talTarget);
      renderRequirementsList(req);
    }

    // Получить классы свечения для редкости
    function getRarityGlowClasses(rarity) {
      // Возвращает градиенты в стиле Genshin
      if (rarity === 5) return "from-amber-500/20 to-[#1e191d] border-amber-500/50";
      if (rarity === 4) return "from-purple-500/20 to-[#181622] border-purple-500/50";
      if (rarity === 3) return "from-sky-500/20 to-[#121921] border-sky-500/50";
      if (rarity === 2) return "from-emerald-500/20 to-[#121b19] border-emerald-500/50";
      return "from-slate-600/10 to-[#11131e] border-slate-700/50";
    }

    // Автоматическая генерация ссылок на иконки с Fandom Wiki
    function getMaterialIconUrl(enName) {
      if (!enName) return "";
      if (enName === "Mora") return "https://genshin-impact.fandom.com/wiki/Special:FilePath/Item_Mora.png";
      if (enName === "Hero's Wit") return "https://genshin-impact.fandom.com/wiki/Special:FilePath/Item_Hero's_Wit.png";
      if (enName === "Crown of Insight") return "https://genshin-impact.fandom.com/wiki/Special:FilePath/Item_Crown_of_Insight.png";

      // Очистка названия для получения валидной ссылки
      let cleanName = enName.trim().replace(/\s+/g, '_');
      return `https://genshin-impact.fandom.com/wiki/Special:FilePath/Item_${cleanName}.png`;
    }

    function renderRequirementsList(req) {
      const container = document.getElementById("mats-list");
      container.innerHTML = "";

      const getGem = (tierKey, defaultNameRu, defaultNameEn) => {
        if (selectedChar.materials && selectedChar.materials.gemstones && selectedChar.materials.gemstones[tierKey]) {
          return {
            ru: selectedChar.materials.gemstones[tierKey].ru || defaultNameRu,
            en: selectedChar.materials.gemstones[tierKey].en || defaultNameEn
          };
        }
        return { ru: defaultNameRu, en: defaultNameEn };
      };

      const defaultGem = ELEMENTAL_GEMSTONES[selectedChar.element] || ELEMENTAL_GEMSTONES.Hydro;
      const gem1 = getGem('tier1', defaultGem.tier1, defaultGem.enRoot + " Sliver");
      const gem2 = getGem('tier2', defaultGem.tier2, defaultGem.enRoot + " Fragment");
      const gem3 = getGem('tier3', defaultGem.tier3, defaultGem.enRoot + " Chunk");
      const gem4 = getGem('tier4', defaultGem.tier4, defaultGem.enRoot + " Gemstone");

      // Собираем группы ресурсов в зависимости от выбранного фильтра (all / level / talents)
      const groups = [];

      if (activeMatsTab === 'all' || activeMatsTab === 'level') {
        groups.push(
          {
            title: "🌌 Уровень и Опыт Персонажа",
            items: [
              { id: "mora_lvl", label: "Мора (Прокачка уровня)", qty: req.level.mora, emoji: "🪙", enName: "Mora", rarity: 3, type: 'mora' },
              { id: "wit", label: "Опыт героя", qty: req.level.heroWit, emoji: "📕", enName: "Hero's Wit", rarity: 4, type: 'wit' }
            ]
          },
          {
            title: "💎 Драгоценные Камни Стихии (" + selectedChar.element + ")",
            items: [
              { id: "gem_1", label: gem1.ru, qty: req.level.gemstoneCount.tier1, emoji: "🟢", enName: gem1.en, rarity: 2, type: 'gemstone' },
              { id: "gem_2", label: gem2.ru, qty: req.level.gemstoneCount.tier2, emoji: "🔵", enName: gem2.en, rarity: 3, type: 'gemstone' },
              { id: "gem_3", label: gem3.ru, qty: req.level.gemstoneCount.tier3, emoji: "🟣", enName: gem3.en, rarity: 4, type: 'gemstone' },
              { id: "gem_4", label: gem4.ru, qty: req.level.gemstoneCount.tier4, emoji: "👑", enName: gem4.en, rarity: 5, type: 'gemstone' }
            ]
          },
          {
            title: "🌸 Боссы и Местные Диковины",
            items: [
              { id: "boss", label: `${selectedChar.materials.boss_drop.ru} (Обычный босс)`, qty: req.level.bossDrop, emoji: "⛰️", enName: selectedChar.materials.boss_drop.en, rarity: 4, type: 'boss' },
              { id: "specialty", label: `${selectedChar.materials.local_specialty.ru} (Диковина)`, qty: req.level.specialty, emoji: "🌸", enName: selectedChar.materials.local_specialty.en, rarity: 1, type: 'specialty' }
            ]
          },
          {
            title: "🗡️ Возвышение: Враги на карте",
            items: [
              { id: "common_1_lvl", label: `${selectedChar.materials.enemy_drop.tier1.ru} (Возвышение)`, qty: req.level.commonDrop.tier1, emoji: "🗡️", enName: selectedChar.materials.enemy_drop.tier1.en, rarity: 1, type: 'enemy' },
              { id: "common_2_lvl", label: `${selectedChar.materials.enemy_drop.tier2.ru} (Возвышение)`, qty: req.level.commonDrop.tier2, emoji: "⚔️", enName: selectedChar.materials.enemy_drop.tier2.en, rarity: 2, type: 'enemy' },
              { id: "common_3_lvl", label: `${selectedChar.materials.enemy_drop.tier3.ru} (Возвышение)`, qty: req.level.commonDrop.tier3, emoji: "🛡️", enName: selectedChar.materials.enemy_drop.tier3.en, rarity: 3, type: 'enemy' }
            ]
          }
        );
      }

      if (activeMatsTab === 'all' || activeMatsTab === 'talents') {
        groups.push(
          {
            title: "🪙 Валюта развития талантов",
            items: [
              { id: "mora_tal", label: "Мора (Прокачка талантов)", qty: req.talents.mora, emoji: "🪙", enName: "Mora", rarity: 3, type: 'mora' }
            ]
          },
          {
            title: "📘 Книги развития талантов",
            items: [
              { id: "books_1", label: `Учения о «${selectedChar.materials.book_series.ru}»`, qty: req.talents.talentBooks.tier1, emoji: "📄", enName: "Teachings of " + selectedChar.materials.book_series.en, rarity: 2, type: 'book' },
              { id: "books_2", label: `Указания о «${selectedChar.materials.book_series.ru}»`, qty: req.talents.talentBooks.tier2, emoji: "📜", enName: "Guide to " + selectedChar.materials.book_series.en, rarity: 3, type: 'book' },
              { id: "books_3", label: `Философия о «${selectedChar.materials.book_series.ru}»`, qty: req.talents.talentBooks.tier3, emoji: "📘", enName: "Philosophies of " + selectedChar.materials.book_series.en, rarity: 4, type: 'book' }
            ]
          },
          {
            title: "🐉 Еженедельные боссы и Короны",
            items: [
              { id: "weekly", label: `${selectedChar.materials.weekly_boss.ru} (Еженедельный босс)`, qty: req.talents.talentWeekly, emoji: "🐉", enName: selectedChar.materials.weekly_boss.en, rarity: 5, type: 'weekly' },
              { id: "crown", label: "Корона прозрения (Макс. уровень таланта)", qty: req.talents.talentCrown, emoji: "👑", enName: "Crown of Insight", rarity: 5, type: 'crown' }
            ]
          },
          {
            title: "⚔️ Таланты: Враги на карте",
            items: [
              { id: "common_1_tal", label: `${selectedChar.materials.enemy_drop.tier1.ru} (Таланты)`, qty: req.talents.commonDrop.tier1, emoji: "🗡️", enName: selectedChar.materials.enemy_drop.tier1.en, rarity: 1, type: 'enemy' },
              { id: "common_2_tal", label: `${selectedChar.materials.enemy_drop.tier2.ru} (Таланты)`, qty: req.talents.commonDrop.tier2, emoji: "⚔️", enName: selectedChar.materials.enemy_drop.tier2.en, rarity: 2, type: 'enemy' },
              { id: "common_3_tal", label: `${selectedChar.materials.enemy_drop.tier3.ru} (Таланты)`, qty: req.talents.commonDrop.tier3, emoji: "🛡️", enName: selectedChar.materials.enemy_drop.tier3.en, rarity: 3, type: 'enemy' }
            ]
          }
        );
      }

      let totalCheckboxCount = 0;
      let checkedCount = 0;

      groups.forEach(g => {
        const validItems = g.items.filter(i => i.qty > 0);
        if (validItems.length === 0) return;

        const groupDiv = document.createElement("div");
        groupDiv.className = "space-y-2 pt-4 border-t border-slate-800/60 first:border-t-0";
        groupDiv.innerHTML = `<h5 class="text-xs font-bold text-slate-500 uppercase tracking-wider mb-2">${g.title}</h5>`;

        validItems.forEach(item => {
          const itemKey = `collected_${selectedChar.id}_${item.id}`;
          const isCollected = localStorage.getItem(itemKey) === "true";
          
          totalCheckboxCount++;
          if (isCollected) checkedCount++;

          const row = document.createElement("div");
          row.className = `flex items-center justify-between p-3 rounded-xl border border-slate-800 bg-[#161925]/60 transition-all duration-200 hover:bg-[#161925] ${isCollected ? 'opacity-40 line-through border-slate-800 bg-slate-900/30' : ''}`;
          
          const glowClasses = getRarityGlowClasses(item.rarity);
          const iconUrl = getMaterialIconUrl(item.enName);
          const fallbackVector = generateFallbackSVG(item.type, selectedChar.element, item.rarity);

          row.innerHTML = `
            <div class="flex items-center gap-3">
              <!-- Иконка в Genshin-стиле -->
              <div class="relative w-12 h-12 rounded-xl border flex-shrink-0 flex items-center justify-center overflow-hidden bg-gradient-to-b ${glowClasses} shadow-md">
                <img src="${iconUrl}" alt="${item.label}" class="w-10 h-10 object-contain drop-shadow z-10" onerror="this.style.display='none'; this.nextElementSibling.style.display='flex';">
                <div class="absolute inset-0 hidden items-center justify-center bg-[#161925]/90">${fallbackVector}</div>
              </div>
              <div>
                <span class="text-sm font-semibold text-slate-200 leading-snug">${item.label}</span>
                <span class="block text-[10px] text-slate-400 font-bold mt-0.5 uppercase tracking-wider">Требуется: ${item.qty.toLocaleString()}</span>
              </div>
            </div>
            <input type="checkbox" data-key="${itemKey}" ${isCollected ? 'checked' : ''} class="w-5 h-5 rounded-lg border-slate-800 text-amber-500 focus:ring-amber-500 bg-[#0c0e17] cursor-pointer" onchange="toggleItemCollect(this)">
          `;

          groupDiv.appendChild(row);
        });

        container.appendChild(groupDiv);
      });

      // Обновление прогресс-бара под выбранную вкладку
      const progressPercent = totalCheckboxCount > 0 ? Math.round((checkedCount / totalCheckboxCount) * 100) : 0;
      document.getElementById("checklist-progress").innerText = `${progressPercent}%`;
      document.getElementById("checklist-progress-bar").style.width = `${progressPercent}%`;
    }

    // Клик по чекбоксу
    function toggleItemCollect(checkbox) {
      const key = checkbox.getAttribute("data-key");
      const isChecked = checkbox.checked;

      if (isChecked) {
        localStorage.setItem(key, "true");
      } else {
        localStorage.removeItem(key);
      }

      recalculate();
    }

    // Сбросить прогресс сбора для выбранного персонажа
    function resetCharacterProgress() {
      if (!selectedChar) return;
      const keysToRemove = [];
      for (let i = 0; i < localStorage.length; i++) {
        const key = localStorage.key(i);
        if (key && key.startsWith(`collected_${selectedChar.id}_`)) {
          keysToRemove.push(key);
        }
      }
      keysToRemove.forEach(key => localStorage.removeItem(key));
      recalculate();
    }

    // Рендеринг сборки на 3-й вкладке
    function renderBuildCard(char) {
      const container = document.getElementById("builds-container");
      container.innerHTML = "";

      const build = char.builds || {
        "role": "Универсальный дамагер / Поддержка",
        "weapons": [
          { "name": "Любое 5★ Оружие", "rank": "S", "desc": "Базовое оружие с высокими статами." },
          { "name": "Крафтовое оружие 4★", "rank": "A", "desc": "Доступное решение для любого игрока." }
        ],
        "artifacts": {
          "sets": ["2x Набор на Силу Атаки", "2x Набор на Элементальный урон"],
          "main_stats": { "sands": "Сила атаки %", "goblet": "Бонус стихийного урона %", "circlet": "Крит. шанс / Крит. урон" },
          "sub_stats": ["Крит. шанс", "Крит. урон", "Сила атаки %"]
        }
      };

      // Колонка 1: Роль и Оружие
      const col1 = document.createElement("div");
      col1.className = "md:col-span-1 space-y-6 bg-[#11131e] p-6 rounded-2xl border border-slate-800 shadow-xl";
      
      const weaponsListHTML = build.weapons.map(w => `
        <div class="p-3 bg-[#161925] border border-slate-800 rounded-xl space-y-1">
          <div class="flex items-center justify-between">
            <span class="font-bold text-sm text-slate-100">${w.name}</span>
            <span class="text-xs bg-amber-500/10 text-amber-400 font-bold px-2 py-0.5 rounded-full">${w.rank}</span>
          </div>
          <p class="text-xs text-slate-400 leading-relaxed">${w.desc}</p>
        </div>
      `).join('');

      col1.innerHTML = `
        <div class="pb-4 border-b border-slate-800">
          <span class="text-xs uppercase font-extrabold text-amber-400 tracking-wider">Роль в отряде</span>
          <h3 class="text-lg font-bold mt-1 text-slate-100">${build.role}</h3>
        </div>
        
        <div>
          <h4 class="text-sm font-bold text-slate-400 tracking-wider uppercase mb-3">Рекомендуемое оружие</h4>
          <div class="space-y-3">
            ${weaponsListHTML}
          </div>
        </div>
      `;

      // Колонка 2: Наборы артефактов и статы
      const col2 = document.createElement("div");
      col2.className = "md:col-span-2 space-y-6 bg-[#11131e] p-6 rounded-2xl border border-slate-800 shadow-xl";

      const subStatsHTML = build.artifacts.sub_stats.map(s => `
        <span class="inline-block bg-slate-800 border border-slate-700/60 text-slate-300 px-3 py-1.5 rounded-lg text-xs font-semibold mr-1.5 mb-1.5">${s}</span>
      `).join('');

      col2.innerHTML = `
        <div class="pb-4 border-b border-slate-800">
          <span class="text-xs uppercase font-extrabold text-amber-400 tracking-wider">Лучшие Артефакты</span>
          <p class="text-sm font-medium mt-1 text-slate-300">${build.artifacts.sets.join('<br>')}</p>
        </div>

        <div>
          <h4 class="text-sm font-bold text-slate-400 tracking-wider uppercase mb-4">Главные характеристики (Main Stats)</h4>
          <div class="grid grid-cols-1 sm:grid-cols-3 gap-3">
            <div class="p-3 bg-[#161925] border border-slate-800 rounded-xl">
              <span class="text-[10px] uppercase font-bold text-slate-500 tracking-wider">Часы</span>
              <span class="block text-xs text-slate-200 font-bold mt-1">${build.artifacts.main_stats.sands}</span>
            </div>
            <div class="p-3 bg-[#161925] border border-slate-800 rounded-xl">
              <span class="text-[10px] uppercase font-bold text-slate-500 tracking-wider">Кубок</span>
              <span class="block text-xs text-slate-200 font-bold mt-1">${build.artifacts.main_stats.goblet}</span>
            </div>
            <div class="p-3 bg-[#161925] border border-slate-800 rounded-xl">
              <span class="text-[10px] uppercase font-bold text-slate-500 tracking-wider">Корона</span>
              <span class="block text-xs text-slate-200 font-bold mt-1">${build.artifacts.main_stats.circlet}</span>
            </div>
          </div>
        </div>

        <div>
          <h4 class="text-sm font-bold text-slate-400 tracking-wider uppercase mb-3">Приоритет суб-статов (Sub Stats)</h4>
          <div class="flex flex-wrap pt-1">
            ${subStatsHTML}
          </div>
        </div>
      `;

      container.appendChild(col1);
      container.appendChild(col2);
    }

    // Рендеринг списка персонажей в редакторе базы
    function renderEditorCharList() {
      const listContainer = document.getElementById("editor-char-list");
      listContainer.innerHTML = "";

      CHARACTERS_DATABASE.forEach(char => {
        const btn = document.createElement("button");
        btn.type = "button";
        btn.className = "w-full text-left p-3 rounded-xl bg-[#161925] border border-slate-800 hover:border-amber-500/50 flex items-center justify-between transition-all group";
        
        btn.innerHTML = `
          <div class="flex items-center gap-3">
            <div class="w-8 h-8 rounded-full overflow-hidden bg-slate-900 flex items-center justify-center border border-slate-700">
              <img src="${char.image || ''}" class="w-full h-full object-cover" onerror="this.style.display='none'; this.nextElementSibling.style.display='flex';">
              <span class="hidden text-xs">${char.emoji || '✨'}</span>
            </div>
            <span class="text-sm font-bold text-slate-200 group-hover:text-amber-400 transition-all">${char.name} <span class="text-xs font-normal opacity-80">${char.emoji || ''}</span></span>
          </div>
          <span class="text-[10px] bg-slate-800 text-slate-400 px-2 py-0.5 rounded-full font-bold">${char.element}</span>
        `;

        btn.onclick = () => loadCharacterToForm(char);
        listContainer.appendChild(btn);
      });
    }

    // Загрузка характеристик героя в форму для редактирования
    function loadCharacterToForm(char) {
      document.getElementById("edit-char-id").value = char.id;
      document.getElementById("edit-name").value = char.name;
      document.getElementById("edit-element").value = char.element;
      document.getElementById("edit-rarity").value = char.rarity;
      document.getElementById("edit-image").value = char.image || "";
      document.getElementById("edit-emoji").value = char.emoji || "";

      const defaultGem = ELEMENTAL_GEMSTONES[char.element] || ELEMENTAL_GEMSTONES.Hydro;
      const getGemVal = (tierKey, lang) => {
        if (char.materials && char.materials.gemstones && char.materials.gemstones[tierKey]) {
          return char.materials.gemstones[tierKey][lang] || '';
        }
        return '';
      };

      document.getElementById("edit-gem1-ru").value = getGemVal('tier1', 'ru');
      document.getElementById("edit-gem1-en").value = getGemVal('tier1', 'en');
      document.getElementById("edit-gem2-ru").value = getGemVal('tier2', 'ru');
      document.getElementById("edit-gem2-en").value = getGemVal('tier2', 'en');
      document.getElementById("edit-gem3-ru").value = getGemVal('tier3', 'ru');
      document.getElementById("edit-gem3-en").value = getGemVal('tier3', 'en');
      document.getElementById("edit-gem4-ru").value = getGemVal('tier4', 'ru');
      document.getElementById("edit-gem4-en").value = getGemVal('tier4', 'en');

      document.getElementById("edit-spec-ru").value = char.materials.local_specialty.ru;
      document.getElementById("edit-spec-en").value = char.materials.local_specialty.en;
      
      document.getElementById("edit-boss-ru").value = char.materials.boss_drop.ru;
      document.getElementById("edit-boss-en").value = char.materials.boss_drop.en;

      document.getElementById("edit-books-ru").value = char.materials.book_series.ru;
      document.getElementById("edit-books-en").value = char.materials.book_series.en;

      document.getElementById("edit-weekly-ru").value = char.materials.weekly_boss.ru;
      document.getElementById("edit-weekly-en").value = char.materials.weekly_boss.en;

      document.getElementById("edit-drop1-ru").value = char.materials.enemy_drop.tier1.ru;
      document.getElementById("edit-drop1-en").value = char.materials.enemy_drop.tier1.en;
      document.getElementById("edit-drop2-ru").value = char.materials.enemy_drop.tier2.ru;
      document.getElementById("edit-drop2-en").value = char.materials.enemy_drop.tier2.en;
      document.getElementById("edit-drop3-ru").value = char.materials.enemy_drop.tier3.ru;
      document.getElementById("edit-drop3-en").value = char.materials.enemy_drop.tier3.en;

      // Билд
      const builds = char.builds || {};
      document.getElementById("edit-build-role").value = builds.role || "";
      document.getElementById("edit-build-artifacts").value = (builds.artifacts && builds.artifacts.sets) ? builds.artifacts.sets[0] : "";
      
      if (builds.artifacts && builds.artifacts.main_stats) {
        document.getElementById("edit-stat-sands").value = builds.artifacts.main_stats.sands || "";
        document.getElementById("edit-stat-goblet").value = builds.artifacts.main_stats.goblet || "";
        document.getElementById("edit-stat-circlet").value = builds.artifacts.main_stats.circlet || "";
      } else {
        document.getElementById("edit-stat-sands").value = "";
        document.getElementById("edit-stat-goblet").value = "";
        document.getElementById("edit-stat-circlet").value = "";
      }
    }

    // Настройка формы для создания полностью нового персонажа
    function initNewCharacterForm() {
      document.getElementById("edit-char-id").value = "new_" + Date.now();
      document.getElementById("edit-name").value = "Новый персонаж";
      document.getElementById("edit-element").value = "Hydro";
      document.getElementById("edit-rarity").value = "5";
      document.getElementById("edit-image").value = "";
      document.getElementById("edit-emoji").value = "✨";

      document.getElementById("edit-gem1-ru").value = "";
      document.getElementById("edit-gem1-en").value = "";
      document.getElementById("edit-gem2-ru").value = "";
      document.getElementById("edit-gem2-en").value = "";
      document.getElementById("edit-gem3-ru").value = "";
      document.getElementById("edit-gem3-en").value = "";
      document.getElementById("edit-gem4-ru").value = "";
      document.getElementById("edit-gem4-en").value = "";

      document.getElementById("edit-spec-ru").value = "";
      document.getElementById("edit-spec-en").value = "";
      document.getElementById("edit-boss-ru").value = "";
      document.getElementById("edit-boss-en").value = "";
      document.getElementById("edit-books-ru").value = "";
      document.getElementById("edit-books-en").value = "";
      document.getElementById("edit-weekly-ru").value = "";
      document.getElementById("edit-weekly-en").value = "";

      document.getElementById("edit-drop1-ru").value = "";
      document.getElementById("edit-drop1-en").value = "";
      document.getElementById("edit-drop2-ru").value = "";
      document.getElementById("edit-drop2-en").value = "";
      document.getElementById("edit-drop3-ru").value = "";
      document.getElementById("edit-drop3-en").value = "";

      document.getElementById("edit-build-role").value = "";
      document.getElementById("edit-build-artifacts").value = "";
      document.getElementById("edit-stat-sands").value = "";
      document.getElementById("edit-stat-goblet").value = "";
      document.getElementById("edit-stat-circlet").value = "";
    }

    // Сохранение изменений формы в локальную базу данных
    function saveCharacterEdits(event) {
      event.preventDefault();

      const id = document.getElementById("edit-char-id").value;
      if (!id) {
        alert("Выберите персонажа или нажмите '+ Новый персонаж'!");
        return;
      }

      const name = document.getElementById("edit-name").value.trim();
      const element = document.getElementById("edit-element").value;
      const rarity = parseInt(document.getElementById("edit-rarity").value);
      const image = document.getElementById("edit-image").value.trim();
      const emoji = document.getElementById("edit-emoji").value.trim();

      const gem1_ru = document.getElementById("edit-gem1-ru").value.trim();
      const gem1_en = document.getElementById("edit-gem1-en").value.trim();
      const gem2_ru = document.getElementById("edit-gem2-ru").value.trim();
      const gem2_en = document.getElementById("edit-gem2-en").value.trim();
      const gem3_ru = document.getElementById("edit-gem3-ru").value.trim();
      const gem3_en = document.getElementById("edit-gem3-en").value.trim();
      const gem4_ru = document.getElementById("edit-gem4-ru").value.trim();
      const gem4_en = document.getElementById("edit-gem4-en").value.trim();

      const spec_ru = document.getElementById("edit-spec-ru").value.trim();
      const spec_en = document.getElementById("edit-spec-en").value.trim();
      
      const boss_ru = document.getElementById("edit-boss-ru").value.trim();
      const boss_en = document.getElementById("edit-boss-en").value.trim();

      const books_ru = document.getElementById("edit-books-ru").value.trim();
      const books_en = document.getElementById("edit-books-en").value.trim();

      const weekly_ru = document.getElementById("edit-weekly-ru").value.trim();
      const weekly_en = document.getElementById("edit-weekly-en").value.trim();

      const drop1_ru = document.getElementById("edit-drop1-ru").value.trim();
      const drop1_en = document.getElementById("edit-drop1-en").value.trim();
      const drop2_ru = document.getElementById("edit-drop2-ru").value.trim();
      const drop2_en = document.getElementById("edit-drop2-en").value.trim();
      const drop3_ru = document.getElementById("edit-drop3-ru").value.trim();
      const drop3_en = document.getElementById("edit-drop3-en").value.trim();

      const role = document.getElementById("edit-build-role").value.trim() || "Главный ДД";
      const artifactSet = document.getElementById("edit-build-artifacts").value.trim() || "2x Сила атаки";
      const sands = document.getElementById("edit-stat-sands").value.trim() || "Сила атаки %";
      const goblet = document.getElementById("edit-stat-goblet").value.trim() || "Элементальный урон %";
      const circlet = document.getElementById("edit-stat-circlet").value.trim() || "Крит. урон";

      // Цветовые хелперы для Tailwind на основании элементов
      const elementColors = {
        Hydro: "sky-400",
        Pyro: "red-400",
        Dendro: "emerald-400",
        Electro: "purple-400",
        Anemo: "teal-400",
        Geo: "amber-500",
        Cryo: "cyan-400"
      };

      const characterData = {
        id: id,
        name: name,
        element: element,
        rarity: rarity,
        emoji: emoji || "✨",
        image: image || "",
        color: elementColors[element] || "slate-400",
        materials: {
          boss_drop: { ru: boss_ru, en: boss_en },
          local_specialty: { ru: spec_ru, en: spec_en },
          weekly_boss: { ru: weekly_ru, en: weekly_en },
          book_series: { ru: books_ru, en: books_en },
          gemstones: {
            tier1: { ru: gem1_ru, en: gem1_en },
            tier2: { ru: gem2_ru, en: gem2_en },
            tier3: { ru: gem3_ru, en: gem3_en },
            tier4: { ru: gem4_ru, en: gem4_en }
          },
          enemy_drop: {
            tier1: { ru: drop1_ru, en: drop1_en },
            tier2: { ru: drop2_ru, en: drop2_en },
            tier3: { ru: drop3_ru, en: drop3_en }
          }
        },
        builds: {
          role: role,
          weapons: [
            { name: "Сигнатурное оружие 5★", rank: "S+", desc: "Идеально раскрывает потенциал героя." },
            { name: "Альтернативное оружие 4★", rank: "A (F2P)", desc: "Доступный бесплатный вариант." }
          ],
          artifacts: {
            sets: [artifactSet],
            main_stats: { sands: sands, goblet: goblet, circlet: circlet },
            sub_stats: ["Крит. урон", "Крит. шанс", "Сила атаки %"]
          }
        }
      };

      const existingIndex = CHARACTERS_DATABASE.findIndex(c => c.id === id);
      if (existingIndex !== -1) {
        CHARACTERS_DATABASE[existingIndex] = characterData;
      } else {
        CHARACTERS_DATABASE.push(characterData);
      }

      saveDatabase();
      renderCharactersGrid();
      renderEditorCharList();
      
      // Возврат на вкладку персонажей
      switchTab('characters');
      selectCharacter(characterData);
    }

    // Первичный запуск на событие загрузки страницы
    window.onload = function() {
      initDatabase();
      renderCharactersGrid();
      renderEditorCharList();
    };
  </script>
</body>
</html>
