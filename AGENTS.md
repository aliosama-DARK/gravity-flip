# AGENTS — Context للمشروع

## اللعبة الحالية: «انقلاب · FLIP»
- **ما هي:** 2D Platformer/Shooter بقَلْب الجاذبية في ملف HTML واحد
- **التقنية:** HTML5 Canvas + Web Audio | ملف واحد | 1722 سطر | ~95KB
- **الحالة:** كاملة قابلة للعب (v1.0)
- **المسار:** `C:\Users\madao\OneDrive\Documents\GitHub\gravity-flip\index.html`

### ما تم إنجازه (بالترتيب):
1. تحليل أولي + إضافة idle bob + رجلين (ثم حذف)
2. Gun recoil + عيون enemies تتابع اللاعب + بؤبؤ الزعيم
3. Shooter enemy 'S' + Power-ups (Shield/Rapid)
4. Air Dash (Shift) + Parallax background
5. تحسين شكل اللاعب + الأعداء + الزعماء
6. Responsive canvas + DPR + Touch events
7. Hitstop system + expanding rings
8. 3 أنماط موسيقية DOOM-style (Calm/Tense/Boss)
9. Speedrun timer + Best Times (localStorage)
10. تسريع اللعبة (RUN_MAX 5.5, GRAV 0.9, etc.)
11. Fix: updateEbullets خارج if(G.boss)
12. S enemies للمراحل 3,7,8
13. **الدفعة الكبيرة:** Visual Glow (lighter), Trail + Rings system, Particles upgrade, Level redesign, SFX pitch variation, UI glow/transitions
14. **الدفعة الثانية:** Heat System (بدل الذخيرة), Player color gradient, Tutorial bubbles (ثم حذف), Level Complete screen, Death screen, Ranking (ذهب/فضة/برونز), Secrets (!), 3 شاشات قصة, Performance (particle limit), Red vignette, Enemy HP bars, Boss windup indicators, Charger enemy 'c', Vertical level (Abyss)

### ما في الـ Gameplay حالياً:
- 10 مراحل — Step, Spikes, Wires, Gunplay, Warden (زعيم), Brittle, Abyss (عمودي), Walls, Trial, Tyrant (زعيم)
- 4 أنواع أعداء: h (زاحف أفقي), v (متأرجح عمودي), s (مطلق نار), c (مندفع/شاحن)
- زعيمان: Warden (يرتد + رشقات + اندفاع), Tyrant (يحوم + مطر رصاص + نبضة جاذبية)
- Power-ups: Shield (درع 480 فريم), Rapid (سرعة إطلاق 300 فريم)
- Heat system: 100 حد, 12 حرارة/طلقة, يبرد 0.5/فريم
- Air dash: 22px/frame, مرة لكل طلقة جوية, كولداون 90 فريم
- Secrets: 3 (في مستوى 0/1/3)
- شاشات قصة: 3 (بعد مستوى 2, 5, وقبل الأخير)

### الإعدادات:
- `LANG` يحدد اللغة — نصوص في `I18N`
- `Snd.musicVol`, `Snd.sfxVol` يتحكمون بالصوت
- حفظ في localStorage تحت `flip_cfg`: `{ lang, mus, sfx, bestTimes[] }`

### الـ API اللي ينفع نستخدمه في الاختبار:
- `window.GAME` expose: `{ G, CFG, LEVELS, KEYS, mouse, I18N, loadLevel, startGame, update, render, handleKey, parseLevel, doFlip, isSolid, tryShoot, liveEnemies, setLang, getLang, Snd }`

### طريقة الاختبار (Headless):
- استخدم `C:\Users\madao\AppData\Local\Temp\opencode\screenshot.js`
- شغّل بـ: `node screenshot.js`
- Puppeteer يفتح Edge headless على اللعبة

### الدرجات المستفادة:
1. **Single file ألم** — للمشروع الجاي نستخدم files منفصلة
2. **Canvas 2D ينفع للبروتوتايب بس** — الـ composite operations بطيئة
3. **Random boss patterns سيئة** — الـ pattern لازم يكون واضح وثابت
4. **الأفقية مملة** — نحتاج verticality
5. **الأعداء يتوقعون** — كل عدو يحتاج سلوكين عالأقل
6. **Tutorial تفاعلي** أفضل من نصوص
7. **Sound feedback** ضروري لكل UI element
8. **Meta-progression** يمدد عمر اللعبة
9. **SFX بـ OscillatorNode يسمع له** — نحتاج noise layers

## المشروع الجاي: Dungeon Crawler Roguelite
- **الهدف:** تعلم مهارات جديدة (procedural generation, pathfinding A*, inventory systems, FOV, complex save/load)
- **منظور:** Top-down (مش Platformer)
- **الجهد:** 5-7 أيام
- **التقنية:** HTML5 Canvas + Web Audio (نفس الستاك لكن files منفصلة)
- **مبدأ أساسي:** قرارات ذكية > ردود فعل سريعة
