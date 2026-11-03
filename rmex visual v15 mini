-- ============================================================================
-- FIX: three huge do-blocks wrapped into functions (Luau limit: 200 local variables per function)
--  RMEX | MATERIAL ESP · v14  (Liquid Glass, FPS booster, ULTRA mirror, power-on ritual, intro splash, Evade-style effects, EPIC VFX pack)
--  LocalScript → StarterPlayer > StarterPlayerScripts
--  Только для своего тестового места. Все личные эффекты выключены при старте.
-- ============================================================================

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TweenService = game:GetService("TweenService")
local Lighting = game:GetService("Lighting")

local localPlayer = Players.LocalPlayer
local playerGui = localPlayer:WaitForChild("PlayerGui")

local function getCam()
    return workspace.CurrentCamera
end

-- ============================================================================
-- DATA
-- ============================================================================

local STRINGS = {
    en = {
        subtitle = "ESP TEST PANEL",
        tab_esp = "ESP", tab_settings = "SETTINGS", tab_visuals = "VISUALS", tab_screen = "SCREEN",
        boxes = "Boxes", outline = "Player outline", names = "Names", distance = "Distance",
        health = "Health", through = "Through walls", tracers = "Tracers", zoom = "Zoom",
        language = "Language", theme = "Theme", accent = "Accent color",
        fov = "Field of view", stretch_x = "Horizontal stretch", stretch_y = "Vertical stretch",
        reset = "Reset appearance",
        en_btn = "EN", ru_btn = "RU",
        theme_material = "MATERIAL", theme_glass = "GLASS", theme_neon = "NEON",
        master = "All effects", master_d = "Turns all personal effects on or off",
        aura = "Aura", aura_d = "Soft outline glow around you",
        particles = "Particles", particles_d = "Floating sparks around your avatar",
        rings = "Energy rings", rings_d = "Rotating light rings around your body",
        swords = "Orbiting swords", swords_d = "Glowing swords rotating around your character",
        orbs = "Orbiting energy orbs", orbs_d = "Three glowing spheres with flowing trails orbit around you",
        trails = "Energy trail", trails_d = "Glowing trail while you move",
        halo = "Halo", halo_d = "Floating ring above your head",
        wings = "Wings", wings_d = "Glowing wings behind your back",
        lightning = "Lightning", lightning_d = "Electric arcs between body parts",
        far = "Distant lightning", far_d = "Rare strikes 100-500 studs away",
        glitch = "Glitch", glitch_d = "Random flicker of body parts",
        footsteps = "Footstep rings", footsteps_d = "Expanding rings under your feet",
        jumps = "Jump sparks", jumps_d = "Sparks on jump and landing",
        effect_color = "Effect color", red = "Red", green = "Green", blue = "Blue",
        rainbow = "Rainbow cycle", rainbow_speed = "Rainbow speed", rainbow_label = "RAINBOW",
        bloom = "Bloom", bloom_d = "Soft glow around bright objects",
        vignette = "Vignette", vignette_d = "Darkened screen edges",
        shake = "Camera shake", shake_d = "Shakes the camera while running",
        wind = "Wind streaks", wind_d = "Thin streaks swirl around you like wind",
        hat = "Top hat", hat_d = "Translucent top hat on your head",
        ghost = "Lagging bot", ghost_d = "Delayed copy behind you that repeats your moves",
        ghost_alpha = "Bot visibility", ghost_delay = "Bot delay",
        streaks = "Space streaks", streaks_d = "Tiny thin streaks fly through the whole space",
        sway = "Camera sway", sway_d = "Soft, slow camera drift",
        sway_strength = "Sway strength",
        stable = "Stable camera", stable_d = "Keeps its angle while you walk",
        cam_dist = "Camera distance",
        free = "Free camera", free_d = "Fly: stick / WASD, drag to look",
        free_speed = "Free camera speed",
        zoom_title = "ZOOM", studs = "studs",
    },
    ru = {
        subtitle = "ТЕСТОВАЯ ПАНЕЛЬ ESP",
        tab_esp = "ESP", tab_settings = "НАСТР.", tab_visuals = "ВИЗУАЛ", tab_screen = "ЭКРАН",
        boxes = "Рамки", outline = "Обводка", names = "Имена", distance = "Дистанция",
        health = "Здоровье", through = "Сквозь стены", tracers = "Линии", zoom = "Зум",
        language = "Язык", theme = "Тема", accent = "Акцентный цвет",
        fov = "Поле зрения", stretch_x = "Растяжка по горизонтали", stretch_y = "Растяжка по вертикали",
        reset = "Сбросить оформление",
        en_btn = "EN", ru_btn = "RU",
        theme_material = "МАТЕРИАЛ", theme_glass = "СТЕКЛО", theme_neon = "НЕОН",
        master = "Все эффекты", master_d = "Включает или выключает все личные эффекты",
        aura = "Аура", aura_d = "Мягкое свечение вокруг персонажа",
        particles = "Частицы", particles_d = "Искры, плавающие вокруг аватара",
        rings = "Энергокольца", rings_d = "Вращающиеся кольца вокруг тела",
        swords = "Мечи вокруг игрока", swords_d = "Светящиеся мечи вращаются вокруг персонажа",
        orbs = "Большие энергосферы", orbs_d = "Три светящихся шара плавно вращаются вокруг тебя и оставляют шлейф",
        trails = "Энергошлейф", trails_d = "Светящийся след при движении",
        halo = "Ореол", halo_d = "Кольцо над головой",
        wings = "Крылья", wings_d = "Светящиеся крылья за спиной",
        lightning = "Молнии", lightning_d = "Электрические дуги между частями тела",
        far = "Далёкие молнии", far_d = "Редкие удары в 100-500 стадах от тебя",
        glitch = "Глитч", glitch_d = "Случайное мерцание частей тела",
        footsteps = "Следы шагов", footsteps_d = "Расходящиеся круги под ногами",
        jumps = "Искры прыжка", jumps_d = "Всплеск при прыжке и приземлении",
        effect_color = "Цвет эффектов", red = "Красный", green = "Зелёный", blue = "Синий",
        rainbow = "Радуга", rainbow_speed = "Скорость радуги", rainbow_label = "РАДУГА",
        bloom = "Свечение", bloom_d = "Мягкий ореол вокруг ярких объектов",
        vignette = "Виньетка", vignette_d = "Затемнение по краям экрана",
        shake = "Тряска камеры", shake_d = "Камера трясётся при беге",
        wind = "Ветер", wind_d = "Тонкие полоски кружатся вокруг тебя как ветер",
        hat = "Цилиндр", hat_d = "Полупрозрачная шляпа-цилиндр на голове",
        ghost = "Бот-призрак", ghost_d = "Отстающая копия сзади повторяет твои движения",
        ghost_alpha = "Видимость бота", ghost_delay = "Задержка бота",
        streaks = "Космические полоски", streaks_d = "Маленькие тонкие полоски летают по всему пространству",
        sway = "Покачивание камеры", sway_d = "Плавное небольшое движение",
        sway_strength = "Сила покачивания",
        stable = "Стабильная камера", stable_d = "Угол не меняется при ходьбе",
        cam_dist = "Дистанция камеры",
        free = "Свободная камера", free_d = "Полёт: стик / WASD, тяни для обзора",
        free_speed = "Скорость свободной камеры",
        zoom_title = "ЗУМ", studs = "стад.",
    },
}

local RX = {renders = {}, sound = true}
RX.beep = function(on)
    if not RX.sound then return end
    pcall(function()
        local s = RX.snd
        if not s or not s.Parent then
            s = Instance.new("Sound")
            s.SoundId = "rbxasset://sounds/switch.wav"
            s.Volume = 0.6
            s.Parent = game:GetService("SoundService")
            RX.snd = s
        end
        s.PlaybackSpeed = on and 1.35 or 0.8
        s:Play()
    end)
end
RX.CAPS = {
    Aura = {a = 3, sp = 1, sz = 1, int = 1}, Particles = {a = 3, sp = 1, sz = 1}, Rings = {a = 3, sp = 1, sz = 1},
    Swords = {a = 3, sp = 1, sz = 1}, Orbs = {a = 3, sp = 1, sz = 1}, Trails = {a = 1, sp = 1, sz = 1},
    Halo = {a = 3, sp = 1, sz = 1}, Hat = {a = 3, sp = 1, sz = 1}, ChineseHat = {a = 4, sp = 1, sz = 1},
    Wind = {a = 3, sp = 1, sz = 1}, Streaks = {a = 3, sp = 1, sz = 1}, Wings = {a = 3, sp = 1},
    Lightning = {a = 3, sp = 1, sz = 1}, FarLightning = {a = 1, sp = 1}, Glitch = {a = 2, sp = 1},
    Footsteps = {a = 3, sp = 1, sz = 1}, Jumps = {a = 3, sz = 1}, Fire = {a = 4, sp = 1, sz = 1}, Ghost = {ghost = 1},
    Petals = {a = 3, sp = 1, sz = 1}, Crystals = {a = 3, sp = 1, sz = 1}, Runes = {a = 3, sp = 1, sz = 1}, Smoke = {a = 3, sp = 1, sz = 1},
    Sabers = {a = 4, sp = 1, sz = 1}, Pulse = {a = 3, sp = 1, sz = 1},
}
-- v12: new effects (caps). a = number of animations, sp/sz = speed/size sliders, m = motion + color-flow styles
RX.CAPS.Scanner = {a = 4, sp = 1, sz = 1}
RX.CAPS.Matrix = {a = 3, sp = 1, sz = 1}
RX.CAPS.Vortex = {a = 3, sp = 1, sz = 1}
RX.CAPS.Helix = {a = 3, sp = 1, sz = 1}
RX.CAPS.Comets = {a = 3, sp = 1, sz = 1}
RX.CAPS.Ribbons = {a = 3, sp = 1, sz = 1}
RX.CAPS.Bubble = {a = 3, sp = 1, sz = 1}
RX.CAPS.Cage = {a = 3, sp = 1, sz = 1}
RX.CAPS.Laser = {a = 3, sp = 1, sz = 1}
RX.CAPS.Tag = {a = 3, sp = 1, sz = 1}
RX.CAPS.Rush = {a = 3, sp = 1, sz = 1}
RX.CAPS.Arcs = {a = 3, sp = 1, sz = 1}
RX.CAPS.Grid = {a = 3, sp = 1, sz = 1}
RX.CAPS.SpeedLines = {a = 3, sp = 1, sz = 1}
RX.CAPS.Chroma = {a = 3, sp = 1, sz = 1}
RX.CAPS.GlitchBars = {a = 3, sp = 1}
RX.CAPS.Grade = {a = 3, sp = 1, int = 1}
-- v13: Evade-style effects
RX.CAPS.EvadeTrail = {a = 3, sp = 1, sz = 1}
RX.CAPS.AfterImage = {a = 3, sp = 1}
RX.CAPS.AirRibbons = {a = 3, sp = 1, sz = 1}
RX.CAPS.DustKick = {a = 3, sp = 1, sz = 1}
-- v14: EPIC VFX pack
RX.CAPS.Shockwave = {a = 3, sp = 1, sz = 1}
RX.CAPS.Meteors = {a = 3, sp = 1, sz = 1}
RX.CAPS.Pillar = {a = 3, sp = 1, sz = 1}
RX.CAPS.BlackHole = {a = 3, sp = 1, sz = 1}
RX.CAPS.Dragon = {a = 3, sp = 1, sz = 1}
RX.CAPS.Sigil = {a = 3, sp = 1, sz = 1}
RX.CAPS.Impact = {a = 3, sp = 1}
-- every effect except the bot gets the new Motion / Color-flow styles
for _, cap in pairs(RX.CAPS) do
    if not cap.ghost then cap.m = 1 end
end
RX.ANIMS = {
    Aura = {"Pulse|Пульс", "Breathe|Дыхание", "Flicker|Мерцание"},
    Particles = {"Sparks|Искры", "Rising|Вверх", "Burst|Взрыв"},
    Rings = {"Gyro|Гиро", "Flat|Плоско", "Tumble|Кувырок"},
    Swords = {"Orbit|Орбита", "Reverse|Назад", "Breathe|Дыхание"},
    Orbs = {"Atom|Атом", "Flat|Плоско", "Pulse|Пульс"},
    Halo = {"Spin|Вращение", "Wobble|Качка", "Pulse|Пульс"},
    Hat = {"Static|Статика", "Bob|Прыжки", "Sway|Качание"},
    ChineseHat = {"Static|Статика", "Sway|Качание", "Float|Парение", "Shimmer|Блеск"},
    Wind = {"Spiral|Спираль", "Rising|Вверх", "Reverse|Назад"},
    Streaks = {"Drift|Дрейф", "Rain|Дождь", "Rise|Подъём"},
    Wings = {"Flap|Взмах", "Calm|Спокойно", "Flutter|Трепет"},
    Lightning = {"Body|Тело", "Burst|Вспышка", "Crown|Корона"},
    Glitch = {"Flicker|Мерцание", "Chroma|Хрома"},
    Footsteps = {"Ring|Круг", "Double|Двойной", "Sparks|Искры"},
    Jumps = {"Both|Всё", "Ring|Круг", "Sparks|Искры"},
    Fire = {"Flame|Пламя", "Inferno|Ад", "Embers|Угли", "Soul|Дух"},
    Petals = {"Sakura|Сакура", "Snow|Снег", "Fireflies|Светлячки"},
    Crystals = {"Orbit|Орбита", "Shield|Щит", "Spiral|Спираль"},
    Runes = {"Spin|Вращение", "Counter|Встречно", "Pulse|Пульс"},
    Smoke = {"Wisps|Клубы", "Cloud|Туман", "Rising|Вверх"},
    Sabers = {"Orbit|Орбита", "Spin|Пропеллер", "Wheel|Колесо", "Guard|Защита"},
    Pulse = {"Single|Один", "Double|Двойной", "Big|Большой"},
}
RX.ANIMS.Scanner = {"Rise|Подъём", "Bounce|Отскок", "Double|Двойной", "Descend|Спуск"}
RX.ANIMS.Matrix = {"Rain|Дождь", "Swirl|Вихрь", "Rise|Подъём"}
RX.ANIMS.Vortex = {"Tornado|Торнадо", "Inward|Внутрь", "Fountain|Фонтан"}
RX.ANIMS.Helix = {"Spin|Вращение", "Counter|Встречно", "Wave|Волна"}
RX.ANIMS.Comets = {"Equator|Экватор", "Gyro|Гиро", "Chaos|Хаос"}
RX.ANIMS.Ribbons = {"Wave|Волна", "Spiral|Спираль", "Whip|Хлыст"}
RX.ANIMS.Bubble = {"Breathe|Дыхание", "Ripple|Рябь", "Glitch|Глитч"}
RX.ANIMS.Cage = {"Spin|Вращение", "Tumble|Кувырок", "Breathe|Дыхание"}
RX.ANIMS.Laser = {"Steady|Ровно", "Pulse|Пульс", "Sweep|Развёртка"}
RX.ANIMS.Tag = {"Glitch|Глитч", "Typing|Печать", "Rainbow|Радуга"}
RX.ANIMS.Rush = {"Stream|Поток", "Burst|Взрыв", "Orbit|Орбита"}
RX.ANIMS.Arcs = {"Wrap|Обвив", "Crown|Корона", "Cross|Крест"}
RX.ANIMS.Grid = {"Static|Статика", "Wave|Волна", "Scroll|Бег"}
RX.ANIMS.SpeedLines = {"Dash|Рывок", "Constant|Постоянно", "Pulse|Пульс"}
RX.ANIMS.Chroma = {"Static|Статика", "Pulse|Пульс", "Reactive|Реакция"}
RX.ANIMS.GlitchBars = {"Rare|Редко", "Frequent|Часто", "On move|В ходьбе"}
RX.ANIMS.Grade = {"Lime-Pink|Лайм-розовый", "Cyber|Кибер", "Blood|Кровь"}
RX.ANIMS.EvadeTrail = {"Twin|Парный", "Comet|Комета", "Fan|Веер"}
RX.ANIMS.AfterImage = {"Line|Линия", "Spiral|Спираль", "Sprint|Спринт"}
RX.ANIMS.AirRibbons = {"Flow|Поток", "Corkscrew|Штопор", "Wide|Широко"}
RX.ANIMS.DustKick = {"Run|Бег", "Landing|Приземление", "Both|Всё"}
RX.ANIMS.Shockwave = {"Landing|Приземление", "Rhythm|Ритм", "Sprint|Спринт"}
RX.ANIMS.Meteors = {"Rain|Дождь", "Storm|Шторм", "Giant|Гиганты"}
RX.ANIMS.Pillar = {"Pillar|Столп", "Twin|Двойной", "Searchlight|Прожекторы"}
RX.ANIMS.BlackHole = {"Above|Над головой", "Behind|За спиной", "Orbit|Орбита"}
RX.ANIMS.Dragon = {"Coil|Кольцо", "Follow|Следует", "Eight|Восьмёрка"}
RX.ANIMS.Sigil = {"Hexagram|Гексаграмма", "Pentagram|Пентаграмма", "Ascend|Вознесение"}
RX.ANIMS.Impact = {"Jump|Прыжок", "Landing|Приземление", "Heartbeat|Сердцебиение"}
do
    local EX = {
        en = {
            chat = "Chinese hat", chat_d = "Elegant conical hat with woven rings",
            fire = "Fire", fire_d = "Your character burns with flames",
            speed = "Speed", size = "Size", anim = "Animation", intensity = "Brightness",
            ecolor = "Color (A = shared)", tab_universal = "UNIV",
            tracer_origin = "Tracer start", o_bottom = "BOTTOM", o_center = "CENTER", o_top = "TOP",
            crosshair = "Crosshair", crosshair_d = "Aim marker in the screen center",
            cross_style = "Crosshair style", cs_cross = "CROSS", cs_dot = "DOT", cs_circle = "CIRCLE",
            cross_size = "Crosshair size", cross_thick = "Thickness", cross_color = "Crosshair color",
            fullbright = "Always visible", fullbright_d = "Everything stays bright, even in the dark",
            bright_level = "Brightness level",
            uni_speed = "Walk speed", uni_speed_d = "Lower or raise your speed", walkspeed = "Speed value",
            uni_jump = "Jump power", uni_jump_d = "Change jump height", jumppower = "Jump value",
            uni_grav = "Gravity", uni_grav_d = "Lower = floaty, higher = heavy", gravity_v = "Gravity value",
        },
        ru = {
            chat = "Китайская шляпа", chat_d = "Изящная коническая шляпа с плетёными кольцами",
            fire = "Огонь", fire_d = "Персонаж горит огнём",
            speed = "Скорость", size = "Размер", anim = "Анимация", intensity = "Яркость",
            ecolor = "Цвет (A = общий)", tab_universal = "УНИВ",
            tracer_origin = "Начало линий", o_bottom = "НИЗ", o_center = "СЕРЕДИНА", o_top = "ВЕРХ",
            crosshair = "Прицел", crosshair_d = "Прицел в центре экрана",
            cross_style = "Вид прицела", cs_cross = "КРЕСТ", cs_dot = "ТОЧКА", cs_circle = "КРУГ",
            cross_size = "Размер прицела", cross_thick = "Толщина", cross_color = "Цвет прицела",
            fullbright = "Всегда видно", fullbright_d = "Всё хорошо видно, даже в темноте",
            bright_level = "Уровень яркости",
            uni_speed = "Скорость ходьбы", uni_speed_d = "Уменьшить или увеличить скорость", walkspeed = "Значение скорости",
            uni_jump = "Сила прыжка", uni_jump_d = "Изменить высоту прыжка", jumppower = "Значение прыжка",
            uni_grav = "Гравитация", uni_grav_d = "Меньше = парение, больше = тяжесть", gravity_v = "Значение гравитации",
        },
    }
    local EX2 = {
        en = {
            petals = "Petals / snow", petals_d = "Falling sakura, snow or fireflies",
            crystals = "Crystals", crystals_d = "Glowing crystals around you",
            runes = "Rune circle", runes_d = "Magic circle under your feet",
            smoke = "Smoke", smoke_d = "Smoke cloud, can be black",
            preset_title = "Presets", pr_anime = "ANIME", pr_dark = "DARK", pr_fire = "FIRE", pr_ice = "ICE", pr_off = "OFF",
            motionblur = "Motion blur", motionblur_d = "Blur when turning the camera", blur_strength = "Blur strength",
            sounds = "Sounds", sounds_d = "Sound when toggling functions",
        },
        ru = {
            petals = "Лепестки / снег", petals_d = "Падающая сакура, снег или светлячки",
            crystals = "Кристаллы", crystals_d = "Светящиеся кристаллы вокруг",
            runes = "Круг рун", runes_d = "Магический круг под ногами",
            smoke = "Дым", smoke_d = "Облако дыма, можно чёрное",
            preset_title = "Пресеты", pr_anime = "АНИМЕ", pr_dark = "ТЬМА", pr_fire = "ОГОНЬ", pr_ice = "ЛЁД", pr_off = "ВЫКЛ",
            motionblur = "Размытие движения", motionblur_d = "Размытие при повороте камеры", blur_strength = "Сила размытия",
            sounds = "Звуки", sounds_d = "Звук при включении функций",
        },
    }
    for l, tbl in pairs(EX2) do
        for k, v in pairs(tbl) do EX[l][k] = v end
    end
    local EX3 = {
        en = {
            tab_esp = "ESP", tab_settings = "SET", tab_visuals = "VIS", tab_screen = "SCR", tab_universal = "UNI",
            tab_aimbot = "AIM", tab_music = "MUS",
            sabers = "Lightsabers", sabers_d = "Swords of light fly around you",
            pulse = "Pulse rings", pulse_d = "Waves spreading from your feet",
            tint = "World tint", tint_d = "Colors the whole screen", tint_color = "Tint color", tint_strength = "Tint strength", mono = "Black & white",
            stretch = "Stretch screen", stretch_d = "Stretched resolution", stretch_k = "Stretch amount",
            radar = "Radar", radar_d = "Mini radar with players", arrows = "Off-screen arrows", arrows_d = "Arrows to players you can't see",
            headdot = "Head dot", headdot_d = "Dot on every head", lookline = "Look direction", lookline_d = "Line showing where they look",
            aim_on = "Aimbot", aim_on_d = "Aims the camera at the nearest player", aim_hold = "Hold RMB", aim_hold_d = "Aim only while right mouse is held",
            aim_fov = "Aim FOV", aim_smooth = "Smoothness", aim_pred = "Prediction", aim_dist = "Max distance",
            aim_part = "Target part", ap_head = "HEAD", ap_body = "BODY",
            aim_team = "Team check", aim_team_d = "Ignore teammates", aim_wall = "Wall check", aim_wall_d = "Ignore players behind walls",
            aim_sticky = "Sticky target", aim_sticky_d = "Keep the target while it is in FOV", aim_circle = "Show FOV circle", aim_circle_d = "Circle on screen",
            mus_id = "Sound ID", mus_play = "PLAY", mus_pause = "PAUSE", mus_stop = "STOP", mus_vol = "Volume", mus_speed = "Speed",
            mus_loop = "Loop", mus_loop_d = "Repeat the track",
            pr_neon = "NEON", pr_mono = "MONO",
        },
        ru = {
            tab_esp = "ESP", tab_settings = "НАС", tab_visuals = "ВИЗ", tab_screen = "ЭКР", tab_universal = "УНИ",
            tab_aimbot = "АИМ", tab_music = "МУЗ",
            sabers = "Световые мечи", sabers_d = "Световые мечи летают вокруг",
            pulse = "Волны", pulse_d = "Круги расходятся от ног",
            tint = "Цвет мира", tint_d = "Окрашивает весь экран", tint_color = "Цвет заливки", tint_strength = "Сила заливки", mono = "Чёрно-белый",
            stretch = "Растяг экрана", stretch_d = "Растянутое разрешение", stretch_k = "Степень растяга",
            radar = "Радар", radar_d = "Мини-радар с игроками", arrows = "Стрелки за экраном", arrows_d = "Стрелки к игрокам вне экрана",
            headdot = "Точка головы", headdot_d = "Точка на каждой голове", lookline = "Куда смотрит", lookline_d = "Линия направления взгляда",
            aim_on = "Аимбот", aim_on_d = "Наводит камеру на ближайшего игрока", aim_hold = "Удержание ПКМ", aim_hold_d = "Целится только при зажатой ПКМ",
            aim_fov = "Радиус FOV", aim_smooth = "Плавность", aim_pred = "Упреждение", aim_dist = "Макс. дистанция",
            aim_part = "Часть тела", ap_head = "ГОЛОВА", ap_body = "ТЕЛО",
            aim_team = "Свои не цель", aim_team_d = "Игнорировать союзников", aim_wall = "Проверка стен", aim_wall_d = "Игнорировать игроков за стеной",
            aim_sticky = "Липкая цель", aim_sticky_d = "Держать цель пока она в FOV", aim_circle = "Круг FOV", aim_circle_d = "Круг на экране",
            mus_id = "ID музыки", mus_play = "ИГРАТЬ", mus_pause = "ПАУЗА", mus_stop = "СТОП", mus_vol = "Громкость", mus_speed = "Скорость",
            mus_loop = "Повтор", mus_loop_d = "Повторять трек",
            pr_neon = "НЕОН", pr_mono = "ЧБ",
        },
    }
    local EX4 = {
        en = {fps_win = "FPS window", fps_win_d = "Mini window with your FPS", ping_win = "Ping window", ping_win_d = "Mini window with your ping"},
        ru = {fps_win = "Окно FPS", fps_win_d = "Мини-окно с твоим FPS", ping_win = "Окно пинга", ping_win_d = "Мини-окно с твоим пингом"},
    }
    for l, tbl in pairs(EX4) do
        for k, v in pairs(tbl) do EX3[l][k] = v end
    end
    for l, tbl in pairs(EX3) do
        for k, v in pairs(tbl) do EX[l][k] = v end
    end
    for l, tbl in pairs(EX) do
        for k, v in pairs(tbl) do STRINGS[l][k] = v end
    end
    for name, list in pairs(RX.ANIMS) do
        for i, s in ipairs(list) do
            local en, ru = s:match("^(.-)|(.+)$")
            STRINGS.en["an_" .. name .. "_" .. i] = en
            STRINGS.ru["an_" .. name .. "_" .. i] = ru
        end
    end
end

do
    local SHS = {
        en = {
            shaders = "Shaders", shaders_d = "Repaints the whole world: day, sunset, night or mirror",
            shader_mode = "Shader mode",
            sh_day = "DAY", sh_sunset = "SUNSET", sh_night = "NIGHT", sh_mirror = "MIRROR",
            shader_strength = "Shader strength", mirror_level = "Mirror shine",
        },
        ru = {
            shaders = "Шейдеры", shaders_d = "Перекрашивает весь мир: день, закат, ночь или зеркало",
            shader_mode = "Режим шейдеров",
            sh_day = "ДЕНЬ", sh_sunset = "ЗАКАТ", sh_night = "НОЧЬ", sh_mirror = "ЗЕРКАЛО",
            shader_strength = "Сила шейдеров", mirror_level = "Блеск зеркала",
        },
    }
    for l, tbl in pairs(SHS) do
        for k, v in pairs(tbl) do STRINGS[l][k] = v end
    end
end

do
    local NEW = {
        en = {
            scanner = "Scan ring", scanner_d = "Hologram ring sweeps up and down your body",
            matrix = "Code rain", matrix_d = "Falling hacker code around you",
            vortex = "Vortex", vortex_d = "Neon bits spin around you like a tornado",
            helix = "DNA helix", helix_d = "Two glowing strands twist around your body",
            comets = "Comets", comets_d = "Comets with long tails orbit you",
            ribbons = "Ribbons", ribbons_d = "Soft light ribbons flow behind you",
            bubble = "Force bubble", bubble_d = "Hex energy dome around your character",
            cage = "Wire cage", cage_d = "Rotating neon cube frame",
            laser = "Laser eyes", laser_d = "Beams shoot from your eyes and hit walls",
            tag = "Cheater tag", tag_d = "Glitchy tag floating above your head",
            rush = "Rush flames", rush_d = "Red-white flame shards streak past (video look)",
            arcs = "Plasma arcs", arcs_d = "Violet electric arcs wrap your body (video look)",
            grid = "Neon grid", grid_d = "Glowing grid on the floor (video look)",
            speedlines = "Speed lines", speedlines_d = "Anime rush lines fly from the screen center",
            chroma = "Chromatic edges", chroma_d = "RGB-split fringes on the screen edges",
            glitchbars = "Glitch bars", glitchbars_d = "Screen tears with colored bands",
            grade = "Neon grade", grade_d = "Saturated neon colors and glow like the video",
            ritual = "Power-on ritual", ritual_d = "Screen tears, then your character dissolves in",
            ritual_btn = "PLAY RITUAL", detect = "Detection pulse", detect_d = "Red / green edge alarm when ESP or aimbot turns on",
            detect_btn = "TEST ALERT",
            motion = "Motion style", mo_1 = "NONE", mo_2 = "BREATH", mo_3 = "SURGE", mo_4 = "BEAT", mo_5 = "CHAOS",
            flow = "Color flow", fl_1 = "STATIC", fl_2 = "DRIFT", fl_3 = "FLASH", fl_4 = "DUAL",
            det_esp = "ESP SCAN ACTIVE", det_aim = "AIMBOT LOCKED ON", tag_text = "CHEATER",
            sh_neon = "NEON", mirror_tier = "Mirror quality", mt_std = "STANDARD", mt_ultra = "ULTRA (strong phones)",
            ultra_range = "Reflection range", ultra_detail = "Reflection detail", ultra_clear = "Floor clarity",
            boost = "FPS booster", boost_d = "Removes particles, shadows and heavy effects",
            boost_level = "Boost level", bl_1 = "LIGHT", bl_2 = "BALANCED", bl_3 = "MAX",
            boost_fps = "FPS", glass_clarity = "Glass clarity", meta_head = "POWER-ON + ALERTS", new_head = "NEW IN v12",
            evade_head = "EVADE STYLE",
            evadetrail = "Evade trail", evadetrail_d = "Long neon trails stream from your feet like in Evade",
            afterimage = "Afterimages", afterimage_d = "Fading copies of your body stay behind while you move",
            airribbons = "Air ribbons", airribbons_d = "Thin glowing ribbons twist behind you in the air",
            dustkick = "Dust kick", dustkick_d = "Dust puffs under your feet when you run and land",
        },
        ru = {
            scanner = "Кольцо-сканер", scanner_d = "Голографическое кольцо ходит по телу вверх-вниз",
            matrix = "Дождь из кода", matrix_d = "Хакерский код падает вокруг тебя",
            vortex = "Вихрь", vortex_d = "Неоновые частицы кружат торнадо вокруг тебя",
            helix = "Спираль ДНК", helix_d = "Две светящиеся нити вьются вокруг тела",
            comets = "Кометы", comets_d = "Кометы с длинными хвостами летают вокруг",
            ribbons = "Ленты", ribbons_d = "Мягкие световые ленты за спиной",
            bubble = "Силовой пузырь", bubble_d = "Энергетический купол с сотами",
            cage = "Каркас-куб", cage_d = "Вращающийся неоновый куб",
            laser = "Лазерные глаза", laser_d = "Лучи из глаз бьют в стены",
            tag = "Тег читера", tag_d = "Глитч-табличка над головой",
            rush = "Огненные осколки", rush_d = "Красно-белые огненные осколки (как в видео)",
            arcs = "Плазменные дуги", arcs_d = "Фиолетовые дуги обвивают тело (как в видео)",
            grid = "Неоновая сетка", grid_d = "Светящаяся сетка на полу (как в видео)",
            speedlines = "Линии скорости", speedlines_d = "Аниме-линии разлетаются от центра экрана",
            chroma = "Хроматика по краям", chroma_d = "RGB-расслоение по краям экрана",
            glitchbars = "Глитч-полосы", glitchbars_d = "Экран рвётся цветными полосами",
            grade = "Неоновый грейд", grade_d = "Насыщенные неоновые цвета и свечение как в видео",
            ritual = "Ритуал включения", ritual_d = "Экран рвётся, потом персонаж проявляется",
            ritual_btn = "ЗАПУСТИТЬ РИТУАЛ", detect = "Подсветка обнаружения", detect_d = "Красный / зелёный контур при включении ESP и аимбота",
            detect_btn = "ТЕСТ ТРЕВОГИ",
            motion = "Стиль движения", mo_1 = "НЕТ", mo_2 = "ДЫХАНИЕ", mo_3 = "РЫВОК", mo_4 = "ПУЛЬС", mo_5 = "ХАОС",
            flow = "Переливы цвета", fl_1 = "СТАТИКА", fl_2 = "ДРЕЙФ", fl_3 = "ВСПЫШКА", fl_4 = "ДУЭТ",
            det_esp = "ESP: СКАНИРОВАНИЕ", det_aim = "АИМБОТ: ЗАХВАТ ЦЕЛИ", tag_text = "ЧИТЕР",
            sh_neon = "НЕОН", mirror_tier = "Качество зеркала", mt_std = "ОБЫЧНОЕ", mt_ultra = "УЛЬТРА (мощные)",
            ultra_range = "Дальность отражений", ultra_detail = "Детализация отражений", ultra_clear = "Прозрачность пола",
            boost = "Бустер FPS", boost_d = "Убирает частицы, тени и тяжёлые эффекты",
            boost_level = "Уровень буста", bl_1 = "ЛЁГКИЙ", bl_2 = "СРЕДНИЙ", bl_3 = "МАКС",
            boost_fps = "FPS", glass_clarity = "Прозрачность стекла", meta_head = "ВКЛЮЧЕНИЕ + ТРЕВОГИ", new_head = "НОВОЕ В v12",
            evade_head = "СТИЛЬ EVADE",
            evadetrail = "Шлейф Evade", evadetrail_d = "Длинные неоновые полосы тянутся от ног, как в Evade",
            afterimage = "Остаточные образы", afterimage_d = "Затухающие копии тела остаются позади при движении",
            airribbons = "Воздушные ленты", airribbons_d = "Тонкие светящиеся ленты вьются за спиной",
            dustkick = "Пыль из-под ног", dustkick_d = "Облачка пыли при беге и приземлении",
        },
    }
    for l, tbl in pairs(NEW) do
        for k, v in pairs(tbl) do STRINGS[l][k] = v end
    end
    local NEW14 = {
        en = {
            epic_head = "EPIC VFX (v14)", pr_epic = "EPIC",
            shockwave = "Shockwave", shockwave_d = "Huge ring, glowing ground cracks and flying rubble",
            meteors = "Meteor shower", meteors_d = "Burning meteors fall from the sky and explode around you",
            pillar = "Light pillar", pillar_d = "A column of light from the sky with energy rings",
            blackhole = "Black hole", blackhole_d = "Dark core with a glowing disk, matter spirals inside",
            dragon = "Energy dragon", dragon_d = "A glowing serpent coils around you and follows you",
            sigil = "Magic sigil", sigil_d = "Big rotating summoning circle on the ground",
            impact = "Impact flash", impact_d = "Screen shock rings, flash and camera punch on jump / landing",
        },
        ru = {
            epic_head = "ЭПИЧНЫЕ VFX (v14)", pr_epic = "ЭПИК",
            shockwave = "Ударная волна", shockwave_d = "Огромное кольцо, светящиеся трещины и летящие камни",
            meteors = "Метеоритный дождь", meteors_d = "Горящие метеориты падают с неба и взрываются вокруг",
            pillar = "Столп света", pillar_d = "Колонна света с неба и энергетические кольца",
            blackhole = "Чёрная дыра", blackhole_d = "Тёмное ядро со светящимся диском, материя летит внутрь",
            dragon = "Энергетический дракон", dragon_d = "Светящийся змей обвивает тебя и летает следом",
            sigil = "Магическая печать", sigil_d = "Большой вращающийся круг призыва на земле",
            impact = "Вспышка удара", impact_d = "Кольца удара, вспышка и толчок камеры при прыжке / приземлении",
        },
    }
    for l, tbl in pairs(NEW14) do
        for k, v in pairs(tbl) do STRINGS[l][k] = v end
    end
    -- animation labels of the new effects (the older ones were registered earlier)
    for _, name in ipairs({"Scanner", "Matrix", "Vortex", "Helix", "Comets", "Ribbons", "Bubble", "Cage", "Laser", "Tag",
        "Rush", "Arcs", "Grid", "SpeedLines", "Chroma", "GlitchBars", "Grade",
        "EvadeTrail", "AfterImage", "AirRibbons", "DustKick",
        "Shockwave", "Meteors", "Pillar", "BlackHole", "Dragon", "Sigil", "Impact"}) do
        for i, s in ipairs(RX.ANIMS[name]) do
            local en, ru = s:match("^(.-)|(.+)$")
            STRINGS.en["an_" .. name .. "_" .. i] = en
            STRINGS.ru["an_" .. name .. "_" .. i] = ru
        end
    end
end

local THEMES = {
    material = {
        panelAlpha = 0, strokeAlpha = 0.45, strokeThickness = 1, glow = 1,
        bg = Color3.fromRGB(24, 24, 32), surface = Color3.fromRGB(38, 38, 48),
        text = Color3.fromRGB(230, 225, 236), muted = Color3.fromRGB(160, 155, 170),
        off = Color3.fromRGB(90, 87, 100),
        gradient = false, shine = false, blur = false, glassStroke = false,
    },
    glass = {
        panelAlpha = 0.34, strokeAlpha = 0.05, strokeThickness = 1.5, glow = 1,
        cardAlpha = 0.8, indAlpha = 0.12,
        bg = Color3.fromRGB(26, 38, 62), surface = Color3.fromRGB(150, 176, 218),
        text = Color3.fromRGB(250, 252, 255), muted = Color3.fromRGB(208, 224, 246),
        off = Color3.fromRGB(150, 168, 196),
        gradient = true, shine = true, blur = true, glassStroke = true,
    },
    neon = {
        panelAlpha = 0, strokeAlpha = 0, strokeThickness = 2, glow = 0.5,
        bg = Color3.fromRGB(7, 10, 24), surface = Color3.fromRGB(14, 22, 43),
        text = Color3.fromRGB(229, 250, 255), muted = Color3.fromRGB(124, 208, 235),
        off = Color3.fromRGB(45, 55, 80),
        gradient = true, shine = false, blur = false, glassStroke = false,
    },
}

local ACCENTS = {
    Color3.fromRGB(187, 134, 252), -- violet
    Color3.fromRGB(80, 220, 255),  -- cyan
    Color3.fromRGB(255, 95, 145),  -- pink
    Color3.fromRGB(255, 190, 75),  -- amber
    Color3.fromRGB(110, 235, 160), -- mint
    Color3.fromRGB(245, 245, 255), -- white
    Color3.fromRGB(255, 75, 85),   -- red
    Color3.fromRGB(85, 130, 255),  -- blue
}

local EFFECT_COLORS = {
    Color3.fromRGB(0, 220, 255),
    Color3.fromRGB(255, 90, 35),
    Color3.fromRGB(130, 255, 45),
    Color3.fromRGB(220, 250, 255),
    Color3.fromRGB(160, 80, 255),
    Color3.fromRGB(255, 70, 170),
    Color3.fromRGB(255, 190, 75),
    Color3.fromRGB(110, 235, 160),
    Color3.fromRGB(14, 14, 18),
}

local RING_SEGMENTS = 36
local RINGS = {
    {radius = 1.65, y = -1.00, tx = 0.00,  tz = 0.00,  speed = 1.5},
    {radius = 2.15, y = 0.10,  tx = 0.55,  tz = 0.25,  speed = -1.1},
    {radius = 1.85, y = 1.00,  tx = -0.50, tz = -0.30, speed = 0.9},
}
local SWORD_COUNT = 5
local ORB_COUNT = 3
local HALO_BEADS = 40
local BOLT_COUNT = 3
local BOLT_SEGMENTS = 9
-- {angle, length} of each wing feather, from the lowest to the highest
local WING_FEATHERS = {
    {-0.30, 1.15}, {0.00, 1.65}, {0.30, 2.15}, {0.58, 2.55},
    {0.86, 2.75}, {1.12, 2.45}, {1.36, 1.95}, {1.56, 1.35},
}
local BEAM_PARTS = {
    "Head", "UpperTorso", "LowerTorso", "Torso",
    "LeftUpperArm", "RightUpperArm", "LeftLowerArm", "RightLowerArm",
    "LeftHand", "RightHand", "LeftUpperLeg", "RightUpperLeg",
    "LeftLowerLeg", "RightLowerLeg", "LeftFoot", "RightFoot",
    "Left Arm", "Right Arm", "Left Leg", "Right Leg",
}
local STEP_LIMIT = 14
local HEALTH_GOOD = Color3.fromRGB(91, 207, 125)
local HEALTH_LOW = Color3.fromRGB(235, 95, 115)

-- ============================================================================
-- STATE
-- ============================================================================

local lang = "en"
local currentTheme = "material"
local accent = ACCENTS[1]

local settings = {
    Boxes = false, Outline = false, Names = false, Distance = false,
    Health = false, ThroughWalls = false, Tracers = false, Zoom = false,
}
local ESP_ORDER = {"Boxes", "Outline", "Names", "Distance", "Health", "ThroughWalls", "Tracers", "Zoom"}
local ESP_KEYS = {
    Boxes = "boxes", Outline = "outline", Names = "names", Distance = "distance",
    Health = "health", ThroughWalls = "through", Tracers = "tracers", Zoom = "zoom",
}

settings.Radar, settings.Arrows, settings.HeadDot, settings.LookLine = false, false, false, false
local esp = {FOV = 70, StretchX = 100, StretchY = 100, Origin = "bottom"}

local visual = {
    Master = true, Aura = false, Particles = false, Rings = false, Swords = false, Orbs = false, Trails = false,
    Halo = false, Wings = false, Lightning = false, Glitch = false,
    Footsteps = false, Jumps = false,
    Wind = false, Hat = false, Ghost = false, Streaks = false, FarLightning = false,
    GhostAlpha = 30,   -- % видимости бота (30 = 30% видно, 70% прозрачный)
    GhostDelay = 0.5,  -- секунды отставания бота
    Rainbow = false, RainbowSpeed = 35, Color = EFFECT_COLORS[1],
}

local screenFX = {
    Bloom = false, Vignette = false, Shake = false, Cross = false, Bright = false, Blur = false, Tint = false, Stretch = false,
}
RX.cross = {Style = 1, Size = 14, Thick = 2, Color = ACCENTS[6]}
RX.bright = {Level = 70}
RX.uni = {Speed = false, SpeedV = 16, Jump = false, JumpV = 50, Grav = false, GravV = 196}
visual.ChineseHat = false
visual.Fire = false
visual.cfg = {}
for name in pairs(RX.CAPS) do visual.cfg[name] = {Speed = 1, Size = 1, Anim = 1, Intensity = 45, Motion = 1, Flow = 1} end
visual.cfg.Fire.Color = EFFECT_COLORS[2]
visual.cfg.Petals.Color = EFFECT_COLORS[6]
visual.cfg.Crystals.Color = EFFECT_COLORS[4]
visual.cfg.Runes.Color = EFFECT_COLORS[5]
visual.cfg.Smoke.Color = EFFECT_COLORS[9]
visual.Petals, visual.Crystals, visual.Runes, visual.Smoke = false, false, false, false
for _, n in ipairs({"Scanner", "Matrix", "Vortex", "Helix", "Comets", "Ribbons", "Bubble", "Cage", "Laser", "Tag", "Rush", "Arcs",
    "Grid", "SpeedLines", "Chroma", "GlitchBars", "Grade",
    "Shockwave", "Meteors", "Pillar", "BlackHole", "Dragon", "Sigil", "Impact"}) do
    visual[n] = false
end
visual.Ritual, visual.Detect = true, true
visual.cfg.Laser.Color = Color3.fromRGB(255, 50, 70)
visual.cfg.Arcs.Color = Color3.fromRGB(165, 85, 255)
visual.cfg.Grid.Color = Color3.fromRGB(150, 255, 40)
visual.cfg.Rush.Color = Color3.fromRGB(255, 70, 40)
visual.cfg.Matrix.Color = Color3.fromRGB(60, 255, 120)
visual.cfg.Tag.Color = Color3.fromRGB(255, 60, 90)
visual.cfg.Scanner.Color = Color3.fromRGB(60, 240, 255)
visual.cfg.Chroma.Color = Color3.fromRGB(255, 255, 255)
visual.cfg.Shockwave.Color = Color3.fromRGB(255, 130, 50)
visual.cfg.Meteors.Color = Color3.fromRGB(255, 110, 40)
visual.cfg.Pillar.Color = Color3.fromRGB(110, 210, 255)
visual.cfg.BlackHole.Color = Color3.fromRGB(170, 70, 255)
visual.cfg.Dragon.Color = Color3.fromRGB(60, 255, 170)
visual.cfg.Sigil.Color = Color3.fromRGB(255, 205, 70)
visual.cfg.Impact.Color = Color3.fromRGB(255, 255, 255)
RX.blurK = 50
RX.menuScale = 1
RX.perfFps, RX.perfPing = false, false
visual.Sabers, visual.Pulse = false, false
RX.tint = {Color = Color3.fromRGB(190, 70, 255), Strength = 60, Mono = false}
RX.stretchK = 70
RX.aim = {On = false, Hold = true, FOV = 140, Smooth = 40, Part = 1, Team = true, Wall = true, Pred = 0, Dist = 500, Sticky = true, Circle = true}
RX.music = {Vol = 50, Speed = 100, Loop = true}

-- Camera modes (SCREEN tab). Distance / speed sliders live here too.
local camFX = {
    Sway = false, SwayStrength = 40,
    Stable = false, Distance = 14,
    Free = false, FreeSpeed = 40,
}

local tracked = {}
local tracers = {}
local playerConns = {}
local rainbowHue = 0
local shakeAmp = 0
local zoomLevel = 1
local zoomShown = false
local menuOpen = false
local menuToken = 0
local langHooks = {}

local function newFX()
    return {
        instances = {}, conns = {}, emitters = {}, rings = {}, wings = {}, swords = {}, orbs = {},
        halo = {}, bolts = {}, wingSparks = {},
        wind = {}, streaks = {}, hatParts = {}, streaksOn = false,
        chatParts = {}, crysParts = {}, runeParts = {}, saberParts = {}, clk = {}, cur = {}, gcol = {}, gs = {}, ss = {},
        sig = nil, sigAcc = 1, hatK = nil, far = nil,
        groups = {rings = {}, orbs = {}, swords = {}, halo = {}, wings = {}, hat = {}, chat = {}, crys = {}, rune = {}, saber = {}},
        shown = {}, applied = {},
        attachments = {}, bodyParts = {},
        stepAcc = 0, glitchAcc = 0, lightAcc = 0,
        stepCount = 0, glitching = false, boltsShown = false,
        cs = 0, wingPhase = 0, wingAmp = 0.1, wingSpeed = 2,
    }
end
local fx = newFX()

local function buildPalette()
    local t = THEMES[currentTheme]
    return {
        theme = t,
        bg = t.bg, surface = t.surface, text = t.text, muted = t.muted, off = t.off,
        accent = accent,
        onAccent = currentTheme == "neon" and Color3.new(1, 1, 1) or Color3.fromRGB(25, 22, 32),
        stroke = t.glassStroke and Color3.fromRGB(225, 241, 255) or accent,
    }
end
local P = buildPalette()

-- ============================================================================
-- HELPERS
-- ============================================================================

local themeBinds, textBinds = {}, {}
local orderSeq = 0

local function tween(obj, props, time, style, dir)
    local t = TweenService:Create(
        obj,
        TweenInfo.new(time or 0.3, style or Enum.EasingStyle.Quint, dir or Enum.EasingDirection.Out),
        props
    )
    t:Play()
    return t
end

local function setOrTween(obj, props, instant, time)
    if instant then
        for k, v in pairs(props) do obj[k] = v end
    else
        tween(obj, props, time or 0.35)
    end
end

local function corner(parent, radius)
    local c = Instance.new("UICorner")
    c.CornerRadius = UDim.new(0, radius)
    c.Parent = parent
    return c
end

local function isPointer(input)
    local t = input.UserInputType
    return t == Enum.UserInputType.MouseButton1 or t == Enum.UserInputType.Touch
end

local function isMove(input)
    local t = input.UserInputType
    return t == Enum.UserInputType.MouseMovement or t == Enum.UserInputType.Touch
end

local function rgbInts(c)
    return math.floor(c.R * 255 + 0.5), math.floor(c.G * 255 + 0.5), math.floor(c.B * 255 + 0.5)
end

local function bindTheme(fn)
    table.insert(themeBinds, fn)
    fn(P, true)
end

local function applyTheme(instant)
    P = buildPalette()
    for _, fn in ipairs(themeBinds) do fn(P, instant) end
end

local function bindText(obj, key)
    table.insert(textBinds, {obj = obj, key = key})
    obj.Text = STRINGS[lang][key] or key
end

local function refreshTexts()
    local s = STRINGS[lang]
    for _, b in ipairs(textBinds) do
        b.obj.Text = s[b.key] or b.key
    end
    for _, hook in ipairs(langHooks) do hook() end
end

local function addPopScale(obj)
    local s = Instance.new("UIScale")
    s.Name = "PopScale"
    s.Parent = obj
    return s
end

-- Press feedback: shrinks while held, springs back on release.
local function addPress(button, strength)
    local scale = Instance.new("UIScale")
    scale.Parent = button
    button.InputBegan:Connect(function(input)
        if isPointer(input) then tween(scale, {Scale = currentTheme == "glass" and (2 - (strength or 0.94)) or (strength or 0.94)}, 0.12) end
    end)
    UserInputService.InputEnded:Connect(function(input)
        if isPointer(input) then tween(scale, {Scale = 1}, 0.35, Enum.EasingStyle.Back) end
    end)
    return scale
end

-- Drags a GUI object by its Position offsets (not AbsolutePosition, which broke the drag).
local function makeDraggable(handle, target)
    local state = {dragging = false, moved = false}
    local startMouse, startPos
    handle.InputBegan:Connect(function(input)
        if not isPointer(input) then return end
        state.dragging = true
        state.moved = false
        startMouse = input.Position
        startPos = target.Position
    end)
    UserInputService.InputChanged:Connect(function(input)
        if not state.dragging or not isMove(input) then return end
        local delta = input.Position - startMouse
        if not state.moved and delta.Magnitude < 4 then return end
        state.moved = true
        target.Position = UDim2.new(
            startPos.X.Scale, startPos.X.Offset + delta.X,
            startPos.Y.Scale, startPos.Y.Offset + delta.Y
        )
    end)
    UserInputService.InputEnded:Connect(function(input)
        if isPointer(input) then state.dragging = false end
    end)
    return state
end

local function makeLabel(parent, o)
    local l = Instance.new("TextLabel")
    l.BackgroundTransparency = 1
    l.Position = o.pos or UDim2.new()
    l.Size = o.size or UDim2.new(1, 0, 0, 16)
    l.Font = o.font or Enum.Font.GothamMedium
    l.TextSize = o.textSize or 11
    l.TextXAlignment = o.align or Enum.TextXAlignment.Left
    l.TextYAlignment = Enum.TextYAlignment.Center
    l.TextTruncate = Enum.TextTruncate.AtEnd
    l.ZIndex = o.zindex or 2
    l.Text = o.text or ""
    l.Parent = parent
    if o.key then bindText(l, o.key) end
    if o.role ~= false then
        local role = o.role or "text"
        bindTheme(function(p, instant)
            setOrTween(l, {TextColor3 = p[role]}, instant, 0.4)
        end)
    end
    return l
end

local function nextOrder()
    orderSeq += 1
    return orderSeq
end

local function makeCard(parent, height)
    local card = Instance.new("Frame")
    card.Size = UDim2.new(1, -6, 0, height)
    card.BorderSizePixel = 0
    card.LayoutOrder = nextOrder()
    card.Parent = parent
    corner(card, 9)
    addPopScale(card)
    bindTheme(function(p, instant)
        setOrTween(card, {BackgroundColor3 = p.surface, BackgroundTransparency = p.theme.cardAlpha and (0.9 - (RX.glassK or 70) / 100 * 0.25) or 0}, instant, 0.4)
    end)
    return card
end

local function makePage(parent, name)
    local page = Instance.new("ScrollingFrame")
    page.Name = name
    page.Size = UDim2.fromScale(1, 1)
    page.BackgroundTransparency = 1
    page.BorderSizePixel = 0
    page.ScrollBarThickness = 3
    page.ScrollingDirection = Enum.ScrollingDirection.Y
    page.CanvasSize = UDim2.new()
    page.AutomaticCanvasSize = Enum.AutomaticSize.Y
    page.Visible = false
    page.Parent = parent
    local list = Instance.new("UIListLayout")
    list.SortOrder = Enum.SortOrder.LayoutOrder
    list.Padding = UDim.new(0, 6)
    list.Parent = page
    local pad = Instance.new("UIPadding")
    pad.PaddingTop = UDim.new(0, 2)
    pad.PaddingBottom = UDim.new(0, 8)
    pad.Parent = page
    bindTheme(function(p, instant)
        setOrTween(page, {ScrollBarImageColor3 = p.accent}, instant)
    end)
    return page
end

-- Cards pop in one after another when a page or the menu appears.
local function stagger(page)
    if not page then return end
    local i = 0
    for _, child in ipairs(page:GetChildren()) do
        local s = child:FindFirstChild("PopScale")
        if s then
            i += 1
            s.Scale = 0.86
            task.delay(math.min(i * 0.03, 0.4), function()
                tween(s, {Scale = 1}, 0.5, Enum.EasingStyle.Back)
            end)
        end
    end
end

local function makeSwitch(parent, get, set)
    local sw = Instance.new("TextButton")
    sw.Name = "Switch"
    sw.AnchorPoint = Vector2.new(1, 0.5)
    sw.Position = UDim2.new(1, -10, 0.5, 0)
    sw.Size = UDim2.fromOffset(40, 22)
    sw.Text = ""
    sw.AutoButtonColor = false
    sw.BorderSizePixel = 0
    sw.Parent = parent
    corner(sw, 999)

    local knob = Instance.new("Frame")
    knob.Size = UDim2.fromOffset(16, 16)
    knob.BorderSizePixel = 0
    knob.Parent = sw
    corner(knob, 999)
    addPress(sw, 0.9)

    local function render(instant)
        local on = get()
        local glass = currentTheme == "glass"
        local kw = glass and 24 or 16
        setOrTween(sw, {BackgroundColor3 = on and P.accent or P.off, BackgroundTransparency = glass and (on and 0.1 or 0.45) or 0}, instant, 0.35)
        setOrTween(knob, {
            Size = UDim2.fromOffset(kw, 16),
            Position = on and UDim2.fromOffset(37 - kw, 3) or UDim2.fromOffset(3, 3),
            BackgroundColor3 = glass and Color3.new(1, 1, 1) or (on and P.onAccent or P.text),
        }, instant, 0.35)
    end

    sw.Activated:Connect(function()
        local ok, err = pcall(function() set(not get()) end)
        if not ok then warn("[RMEX] toggle error: " .. tostring(err)) end
        render(false)
        pcall(RX.beep, get())
    end)
    bindTheme(function(_, instant) render(instant) end)
    table.insert(RX.renders, render)
    -- keep the switch in sync with the real state (booster, fly window etc. can change it elsewhere)
    task.spawn(function()
        local last = get()
        while sw.Parent do
            local now = get()
            if now ~= last then last = now render(false) end
            task.wait(0.25)
        end
    end)
    return render
end

local function makeToggleRow(parent, o)
    local card = makeCard(parent, o.desc and 46 or 36)
    makeLabel(card, {
        key = o.key,
        pos = o.desc and UDim2.fromOffset(10, 6) or UDim2.fromOffset(10, 0),
        size = o.desc and UDim2.new(1, -(o.pad or 62), 0, 16) or UDim2.new(1, -(o.pad or 62), 1, 0),
        textSize = 11,
    })
    if o.desc then
        makeLabel(card, {
            key = o.desc, pos = UDim2.fromOffset(10, 23), size = UDim2.new(1, -(o.pad or 62), 0, 14),
            font = Enum.Font.Gotham, textSize = 9, role = "muted",
        })
    end
    local render = makeSwitch(card, o.get, function(v)
        o.set(v)
        if o.onChange then o.onChange() end
    end)
    return render, card
end

local function makeSlider(parent, o)
    local card = makeCard(parent, 46)
    makeLabel(card, {key = o.key, pos = UDim2.fromOffset(10, 6), size = UDim2.new(1, -70, 0, 16), textSize = 11})
    local valueLabel = makeLabel(card, {
        pos = UDim2.new(1, -70, 0, 6), size = UDim2.fromOffset(60, 16),
        align = Enum.TextXAlignment.Right, font = Enum.Font.GothamBold, textSize = 10, role = "accent",
    })

    local hit = Instance.new("TextButton")
    hit.Position = UDim2.fromOffset(10, 26)
    hit.Size = UDim2.new(1, -20, 0, 14)
    hit.BackgroundTransparency = 1
    hit.Text = ""
    hit.AutoButtonColor = false
    hit.Parent = card

    local track = Instance.new("Frame")
    track.Position = UDim2.new(0, 0, 0.5, -3)
    track.Size = UDim2.new(1, 0, 0, 6)
    track.BorderSizePixel = 0
    track.Parent = hit
    corner(track, 999)

    local fill = Instance.new("Frame")
    fill.Size = UDim2.fromScale(0, 1)
    fill.BorderSizePixel = 0
    fill.Parent = track
    corner(fill, 999)

    local knob = Instance.new("Frame")
    knob.AnchorPoint = Vector2.new(0.5, 0.5)
    knob.Size = UDim2.fromOffset(12, 12)
    knob.Position = UDim2.fromScale(0, 0.5)
    knob.BorderSizePixel = 0
    knob.ZIndex = 3
    knob.Parent = track
    corner(knob, 999)

    bindTheme(function(p, instant)
        setOrTween(track, {BackgroundColor3 = p.off}, instant, 0.35)
        setOrTween(fill, {BackgroundColor3 = p.accent}, instant, 0.35)
        setOrTween(knob, {BackgroundColor3 = p.text}, instant, 0.35)
    end)

    local function render(instant)
        local v = o.get()
        local f = math.clamp((v - o.min) / (o.max - o.min), 0, 1)
        setOrTween(fill, {Size = UDim2.fromScale(f, 1)}, instant, 0.25)
        setOrTween(knob, {Position = UDim2.fromScale(f, 0.5)}, instant, 0.25)
        valueLabel.Text = o.format(v)
    end

    local dragging = false
    local function setFromX(x)
        local rel = math.clamp((x - track.AbsolutePosition.X) / track.AbsoluteSize.X, 0, 1)
        o.set(o.min + rel * (o.max - o.min))
        render(true)
        if o.onChange then o.onChange() end
    end
    hit.InputBegan:Connect(function(input)
        if isPointer(input) then
            dragging = true
            setFromX(input.Position.X)
        end
    end)
    UserInputService.InputChanged:Connect(function(input)
        if dragging and isMove(input) then setFromX(input.Position.X) end
    end)
    UserInputService.InputEnded:Connect(function(input)
        if isPointer(input) then dragging = false end
    end)

    render(true)
    return render
end

local function makeSwatchRow(parent, titleKey, colors, getCurrent, onPick, marks)
    local card = makeCard(parent, 58)
    makeLabel(card, {key = titleKey, pos = UDim2.fromOffset(10, 6), size = UDim2.new(1, -20, 0, 14), textSize = 10, role = "muted"})

    local row = Instance.new("Frame")
    row.BackgroundTransparency = 1
    row.Position = UDim2.fromOffset(8, 26)
    row.Size = UDim2.new(1, -16, 0, 24)
    row.Parent = card
    local list = Instance.new("UIListLayout")
    list.FillDirection = Enum.FillDirection.Horizontal
    list.HorizontalAlignment = Enum.HorizontalAlignment.Center
    list.VerticalAlignment = Enum.VerticalAlignment.Center
    list.Padding = UDim.new(0, 4)
    list.SortOrder = Enum.SortOrder.LayoutOrder
    list.Parent = row

    local items = {}
    local function refresh(instant)
        local cur = getCurrent()
        for _, item in ipairs(items) do
            setOrTween(item.ring, {Transparency = item.color == cur and 0 or 1}, instant, 0.3)
        end
    end

    for i, color in ipairs(colors) do
        local s = Instance.new("TextButton")
        s.Size = UDim2.fromOffset(18, 18)
        s.BackgroundColor3 = color
        s.Text = ""
        s.AutoButtonColor = false
        s.BorderSizePixel = 0
        s.LayoutOrder = i
        s.Parent = row
        corner(s, 999)
        if marks and marks[i] then
            s.Text = marks[i]
            s.Font = Enum.Font.GothamBold
            s.TextSize = 10
            s.TextColor3 = Color3.new(1, 1, 1)
        end
        local ring = Instance.new("UIStroke")
        ring.Color = Color3.new(1, 1, 1)
        ring.Thickness = 2
        ring.Transparency = 1
        ring.Parent = s
        addPress(s, 0.85)
        s.Activated:Connect(function()
            onPick(color)
            refresh(false)
        end)
        table.insert(items, {ring = ring, color = color})
    end

    bindTheme(function(_, instant) refresh(instant) end)
    refresh(true)
    table.insert(RX.renders, refresh)
    return refresh
end

local function makeSegmented(parent, titleKey, options, getCurrent, onPick)
    local card = makeCard(parent, 58)
    makeLabel(card, {key = titleKey, pos = UDim2.fromOffset(10, 6), size = UDim2.new(1, -20, 0, 14), textSize = 10, role = "muted"})

    local row = Instance.new("Frame")
    row.BackgroundTransparency = 1
    row.Position = UDim2.fromOffset(6, 26)
    row.Size = UDim2.new(1, -12, 0, 26)
    row.Parent = card

    local buttons = {}
    local function refresh(instant)
        local cur = getCurrent()
        for _, item in ipairs(buttons) do
            local on = item.value == cur
            setOrTween(item.button, {BackgroundColor3 = on and P.accent or P.bg}, instant, 0.35)
            setOrTween(item.label, {TextColor3 = on and P.onAccent or P.text}, instant, 0.35)
        end
    end

    local n = #options
    for i, opt in ipairs(options) do
        local b = Instance.new("TextButton")
        b.Position = UDim2.new((i - 1) / n, 2, 0, 0)
        b.Size = UDim2.new(1 / n, -4, 1, 0)
        b.Text = ""
        b.AutoButtonColor = false
        b.BorderSizePixel = 0
        b.Parent = row
        corner(b, 7)
        local lbl = makeLabel(b, {
            key = opt.key, size = UDim2.fromScale(1, 1), font = Enum.Font.GothamBold,
            textSize = 9, align = Enum.TextXAlignment.Center, role = false, zindex = 3,
        })
        addPress(b, 0.95)
        b.Activated:Connect(function()
            onPick(opt.value)
            refresh(false)
        end)
        table.insert(buttons, {button = b, label = lbl, value = opt.value})
    end

    bindTheme(function(_, instant) refresh(instant) end)
    refresh(true)
    table.insert(RX.renders, refresh)
    return refresh
end

-- ============================================================================
-- ROOT GUI
-- ============================================================================

local applySettings      -- defined in ESP section
local refreshVisualUI    -- defined in visuals section
local rainbowRender      -- set when the rainbow toggle is built
local fovRender, stretchXRender, stretchYRender

local gui = Instance.new("ScreenGui")
gui.Name = "RMEXVisuals"
gui.ResetOnSpawn = false
gui.IgnoreGuiInset = true
gui.Parent = playerGui

-- Vignette edges (created first so they sit behind the menu).
local vignetteEdges = {}
local function makeEdge(anchor, pos, size, rot, darkAtStart)
    local f = Instance.new("Frame")
    f.AnchorPoint = anchor
    f.Position = pos
    f.Size = size
    f.BackgroundColor3 = Color3.new(0, 0, 0)
    f.BorderSizePixel = 0
    f.Visible = false
    f.ZIndex = 0
    f.Parent = gui
    local g = Instance.new("UIGradient")
    g.Rotation = rot
    local a, b = 0.42, 1
    if not darkAtStart then a, b = 1, 0.42 end
    g.Transparency = NumberSequence.new({
        NumberSequenceKeypoint.new(0, a),
        NumberSequenceKeypoint.new(1, b),
    })
    g.Parent = f
    table.insert(vignetteEdges, f)
end
makeEdge(Vector2.new(0, 0), UDim2.new(0, 0, 0, 0), UDim2.new(1, 0, 0.28, 0), 90, true)
makeEdge(Vector2.new(0, 1), UDim2.new(0, 0, 1, 0), UDim2.new(1, 0, 0.28, 0), 90, false)
makeEdge(Vector2.new(0, 0), UDim2.new(0, 0, 0, 0), UDim2.new(0.18, 0, 1, 0), 0, true)
makeEdge(Vector2.new(1, 0), UDim2.new(1, 0, 0, 0), UDim2.new(0.18, 0, 1, 0), 0, false)

-- Screen flash for distant lightning.
local farFlash = Instance.new("Frame")
farFlash.Name = "RMEXFarFlash"
farFlash.Size = UDim2.fromScale(1, 1)
farFlash.BackgroundColor3 = Color3.fromRGB(232, 238, 255)
farFlash.BackgroundTransparency = 1
farFlash.BorderSizePixel = 0
farFlash.Active = false
farFlash.Visible = false
farFlash.ZIndex = 0
farFlash.Parent = gui

-- Lighting effects (only used locally, all off by default).
local glassBlur = Lighting:FindFirstChild("RMEXVisualsGlassBlur") or Instance.new("BlurEffect")
glassBlur.Name = "RMEXVisualsGlassBlur"
glassBlur.Size = 0
glassBlur.Enabled = false
glassBlur.Parent = Lighting

local bloomFX = Lighting:FindFirstChild("RMEXBloom") or Instance.new("BloomEffect")
bloomFX.Name = "RMEXBloom"
bloomFX.Intensity = 0.8
bloomFX.Size = 20
bloomFX.Threshold = 0.9
bloomFX.Enabled = false
bloomFX.Parent = Lighting

-- Остатки старых версий (размытие / дымка) — убираем, если они остались в Lighting.
for _, name in ipairs({"RMEXMotionBlur", "RMEXLensHaze", "RMEXLensFog"}) do
    local old = Lighting:FindFirstChild(name)
    if old then old:Destroy() end
end

local function applyScreenFX()
    bloomFX.Enabled = screenFX.Bloom
    for _, e in ipairs(vignetteEdges) do e.Visible = screenFX.Vignette end
end

-- Launcher -------------------------------------------------------------------
local PANEL_W, PANEL_H
do
    local vp = getCam() and getCam().ViewportSize or Vector2.new(800, 420)
    PANEL_W = math.max(240, math.min(276, vp.X - 96))
    PANEL_H = math.max(220, math.min(372, vp.Y - 20))
end

local launcher = Instance.new("TextButton")
launcher.Name = "Launcher"
launcher.AnchorPoint = Vector2.new(0.5, 0.5)
launcher.Size = UDim2.fromOffset(46, 46)
launcher.Position = UDim2.new(0, 37, 0.5, 0)
launcher.Text = "R"
launcher.Font = Enum.Font.GothamBold
launcher.TextSize = 20
launcher.AutoButtonColor = false
launcher.BorderSizePixel = 0
launcher.ZIndex = 5
launcher.Parent = gui
corner(launcher, 999)
local launcherScale = addPress(launcher, 0.9)
local launcherDrag = makeDraggable(launcher, launcher)

local launcherRing = Instance.new("UIStroke")
launcherRing.Thickness = 2
launcherRing.Transparency = 0.2
launcherRing.Parent = launcher
tween(launcherRing, {Transparency = 0.85}, 1.6, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut)
task.spawn(function()
    -- Gentle breathing pulse on the launcher ring.
    while launcherRing.Parent do
        tween(launcherRing, {Transparency = 0.85}, 1.6, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut).Completed:Wait()
        if not launcherRing.Parent then break end
        tween(launcherRing, {Transparency = 0.15}, 1.6, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut).Completed:Wait()
    end
end)

bindTheme(function(p, instant)
    setOrTween(launcher, {BackgroundColor3 = p.accent, TextColor3 = p.onAccent}, instant, 0.4)
    setOrTween(launcherRing, {Color = p.accent}, instant, 0.4)
end)

-- Main panel -----------------------------------------------------------------
local panel = Instance.new("CanvasGroup")
panel.Name = "Panel"
panel.AnchorPoint = Vector2.new(0.5, 0.5)
panel.Size = UDim2.fromOffset(PANEL_W, PANEL_H)
panel.Position = UDim2.new(0, 74 + PANEL_W / 2, 0.5, 0)
panel.GroupTransparency = 1
panel.Visible = false
panel.ClipsDescendants = true
panel.BorderSizePixel = 0
panel.Parent = gui
corner(panel, 14)

local panelScale = Instance.new("UIScale")
panelScale.Scale = 0.62
panelScale.Parent = panel

local panelStroke = Instance.new("UIStroke")
panelStroke.Thickness = 1
panelStroke.Parent = panel
local panelGlow = Instance.new("UIStroke")
panelGlow.Thickness = 6
panelGlow.Transparency = 1
panelGlow.Parent = panel
local panelGradient = Instance.new("UIGradient")
panelGradient.Rotation = 35
panelGradient.Enabled = false
panelGradient.Parent = panel

local shine = Instance.new("Frame")
shine.Name = "GlassReflection"
shine.Position = UDim2.fromOffset(1, 1)
shine.Size = UDim2.new(1, -2, 0, 70)
shine.BackgroundColor3 = Color3.new(1, 1, 1)
shine.BackgroundTransparency = 0.88
shine.BorderSizePixel = 0
shine.Visible = false
shine.Parent = panel
corner(shine, 14)
local shineGradient = Instance.new("UIGradient")
shineGradient.Rotation = 90
shineGradient.Transparency = NumberSequence.new({
    NumberSequenceKeypoint.new(0, 0.15),
    NumberSequenceKeypoint.new(1, 1),
})
shineGradient.Parent = shine

local function gradientFor(p)
    if currentTheme == "glass" then
        return ColorSequence.new({
            ColorSequenceKeypoint.new(0, Color3.fromRGB(190, 220, 255)),
            ColorSequenceKeypoint.new(0.28, p.accent:Lerp(Color3.fromRGB(75, 94, 130), 0.45)),
            ColorSequenceKeypoint.new(1, Color3.fromRGB(24, 34, 55)),
        })
    end
    return ColorSequence.new({
        ColorSequenceKeypoint.new(0, p.accent:Lerp(Color3.fromRGB(8, 12, 30), 0.68)),
        ColorSequenceKeypoint.new(0.35, Color3.fromRGB(13, 20, 43)),
        ColorSequenceKeypoint.new(1, Color3.fromRGB(5, 8, 19)),
    })
end

bindTheme(function(p, instant)
    setOrTween(panel, {BackgroundColor3 = p.bg, BackgroundTransparency = currentTheme == "glass" and (0.62 - (RX.glassK or 70) / 100 * 0.4) or p.theme.panelAlpha}, instant)
    setOrTween(panelStroke, {
        Color = p.stroke, Transparency = p.theme.strokeAlpha, Thickness = p.theme.strokeThickness,
    }, instant)
    setOrTween(panelGlow, {Color = p.accent, Transparency = p.theme.glow}, instant)
    panelGradient.Enabled = p.theme.gradient
    panelGradient.Color = gradientFor(p)
    shine.Visible = p.theme.shine
    applyScreenFX()
end)

-- Header (drag handle) -------------------------------------------------------
local header = Instance.new("TextButton")
header.Name = "Header"
header.Size = UDim2.new(1, 0, 0, 44)
header.BackgroundTransparency = 1
header.Text = ""
header.AutoButtonColor = false
header.ZIndex = 2
header.Parent = panel
local panelDrag = makeDraggable(header, panel)

do
    local grip = Instance.new("TextButton")
    grip.Name = "ResizeGrip"
    grip.AnchorPoint = Vector2.new(1, 1)
    grip.Position = UDim2.new(1, -2, 1, -2)
    grip.Size = UDim2.fromOffset(26, 26)
    grip.BackgroundTransparency = 1
    grip.Text = ""
    grip.AutoButtonColor = false
    grip.ZIndex = 30
    grip.Parent = panel
    local dots = {}
    for _, d in ipairs({{15, 15}, {9, 15}, {15, 9}, {3, 15}, {9, 9}, {15, 3}}) do
        local f = Instance.new("Frame")
        f.Size = UDim2.fromOffset(3, 3)
        f.Position = UDim2.fromOffset(d[1] + 4, d[2] + 4)
        f.BorderSizePixel = 0
        f.ZIndex = 31
        f.Parent = grip
        corner(f, 999)
        table.insert(dots, f)
    end
    bindTheme(function(p, instant)
        for _, f in ipairs(dots) do setOrTween(f, {BackgroundColor3 = p.accent}, instant) end
    end)
    local resizing, startM, startS = false, nil, 1
    grip.InputBegan:Connect(function(input)
        if not isPointer(input) then return end
        resizing = true
        startM = input.Position
        startS = RX.menuScale
    end)
    UserInputService.InputChanged:Connect(function(input)
        if not resizing or not isMove(input) then return end
        local d = input.Position - startM
        local s = math.clamp(startS + d.X / PANEL_W + d.Y / PANEL_H, 0.6, 1.6)
        RX.menuScale = s
        panelScale.Scale = s
    end)
    UserInputService.InputEnded:Connect(function(input)
        if isPointer(input) then resizing = false end
    end)
end

RX.title = makeLabel(header, {
    text = "RMEX VISUALS", pos = UDim2.fromOffset(14, 8), size = UDim2.new(1, -60, 0, 16),
    font = Enum.Font.GothamBold, textSize = 14, role = "accent",
})
makeLabel(header, {
    key = "subtitle", pos = UDim2.fromOffset(14, 25), size = UDim2.new(1, -60, 0, 12),
    textSize = 9, role = "muted",
})

local closeBtn = Instance.new("TextButton")
closeBtn.Size = UDim2.fromOffset(26, 26)
closeBtn.Position = UDim2.new(1, -36, 0, 9)
closeBtn.Text = "×"
closeBtn.Font = Enum.Font.GothamBold
closeBtn.TextSize = 16
closeBtn.AutoButtonColor = false
closeBtn.BorderSizePixel = 0
closeBtn.ZIndex = 3
closeBtn.Parent = header
corner(closeBtn, 999)
addPress(closeBtn)
bindTheme(function(p, instant)
    setOrTween(closeBtn, {BackgroundColor3 = p.surface, TextColor3 = p.text}, instant)
end)

-- Tabs (sliding indicator) ---------------------------------------------------
local TAB_COUNT = 7
local tabBar = Instance.new("Frame")
tabBar.Name = "TabBar"
tabBar.Position = UDim2.fromOffset(10, 48)
tabBar.Size = UDim2.new(1, -20, 0, 30)
tabBar.BorderSizePixel = 0
tabBar.Parent = panel
corner(tabBar, 9)
bindTheme(function(p, instant)
    setOrTween(tabBar, {BackgroundColor3 = p.surface}, instant)
end)

local tabIndicator = Instance.new("Frame")
tabIndicator.Name = "Indicator"
tabIndicator.Size = UDim2.new(1 / TAB_COUNT, -4, 1, -4)
tabIndicator.Position = UDim2.new(0, 2, 0, 2)
tabIndicator.BorderSizePixel = 0
tabIndicator.Parent = tabBar
corner(tabIndicator, 7)
bindTheme(function(p, instant)
    setOrTween(tabIndicator, {BackgroundColor3 = p.accent}, instant)
end)

local content = Instance.new("Frame")
content.Name = "Content"
content.Position = UDim2.fromOffset(10, 86)
content.Size = UDim2.new(1, -20, 1, -94)
content.BackgroundTransparency = 1
content.ClipsDescendants = true
content.Parent = panel

local espPage = makePage(content, "ESPPage")
local settingsPage = makePage(content, "SettingsPage")
local visualsPage = makePage(content, "VisualsPage")
local screenPage = makePage(content, "ScreenPage")
local universalPage = makePage(content, "UniversalPage")
local aimbotPage = makePage(content, "AimbotPage")
local musicPage = makePage(content, "MusicPage")
local pages = {espPage, settingsPage, visualsPage, screenPage, universalPage, aimbotPage, musicPage}

local tabButtons = {}
local currentTab = 0
for i, key in ipairs({"tab_esp", "tab_settings", "tab_visuals", "tab_screen", "tab_universal", "tab_aimbot", "tab_music"}) do
    local b = Instance.new("TextButton")
    b.Size = UDim2.new(1 / TAB_COUNT, 0, 1, 0)
    b.Position = UDim2.new((i - 1) / TAB_COUNT, 0, 0, 0)
    b.BackgroundTransparency = 1
    b.Text = ""
    b.AutoButtonColor = false
    b.ZIndex = 2
    b.Parent = tabBar
    local lbl = makeLabel(b, {
        key = key, size = UDim2.fromScale(1, 1), font = Enum.Font.GothamBold,
        textSize = 9, align = Enum.TextXAlignment.Center, role = false, zindex = 3,
    })
    tabButtons[i] = {button = b, label = lbl}
end

bindTheme(function(p, instant)
    for i, item in ipairs(tabButtons) do
        setOrTween(item.label, {TextColor3 = i == currentTab and p.onAccent or p.muted}, instant, 0.35)
    end
end)


-- ============================================================================
-- LIQUID GLASS (iOS-style): bright specular rim that follows the light / phone tilt,
-- inner lens band, frosted translucent cards, glass capsule tab, vibrancy + backdrop blur.
-- ============================================================================
RX.glassK = 70 -- clarity %, 0 = frosted, 100 = very clear
do
    local WHITE = Color3.new(1, 1, 1)

    -- Rim: gradient on the panel stroke (bright top-left and bottom-right, like a lit glass edge).
    local rimGrad = Instance.new("UIGradient")
    rimGrad.Color = ColorSequence.new(WHITE)
    rimGrad.Transparency = NumberSequence.new({
        NumberSequenceKeypoint.new(0, 0.0),
        NumberSequenceKeypoint.new(0.22, 0.55),
        NumberSequenceKeypoint.new(0.5, 0.92),
        NumberSequenceKeypoint.new(0.78, 0.55),
        NumberSequenceKeypoint.new(1, 0.0),
    })
    rimGrad.Enabled = false
    rimGrad.Parent = panelStroke

    -- Inner lens band: soft wide edge inside the panel (looks like glass thickness).
    local lens = Instance.new("Frame")
    lens.Name = "GlassLens"
    lens.Size = UDim2.fromScale(1, 1)
    lens.BackgroundTransparency = 1
    lens.BorderSizePixel = 0
    lens.Active = false
    lens.Visible = false
    lens.ZIndex = 1
    lens.Parent = panel
    corner(lens, 14)
    local lensStroke = Instance.new("UIStroke")
    lensStroke.Thickness = 5
    lensStroke.Color = WHITE
    lensStroke.Transparency = 0.8
    lensStroke.Parent = lens
    local lensGrad = Instance.new("UIGradient")
    lensGrad.Transparency = NumberSequence.new({
        NumberSequenceKeypoint.new(0, 0.0),
        NumberSequenceKeypoint.new(0.3, 0.75),
        NumberSequenceKeypoint.new(0.7, 0.75),
        NumberSequenceKeypoint.new(1, 0.1),
    })
    lensGrad.Parent = lensStroke

    -- Specular sheen: big diagonal highlight in the upper-left.
    local sheen = Instance.new("Frame")
    sheen.Name = "GlassSheen"
    sheen.Size = UDim2.fromScale(1, 0.55)
    sheen.BackgroundColor3 = WHITE
    sheen.BackgroundTransparency = 0.9
    sheen.BorderSizePixel = 0
    sheen.Active = false
    sheen.Visible = false
    sheen.ZIndex = 1
    sheen.Parent = panel
    corner(sheen, 14)
    local sheenGrad = Instance.new("UIGradient")
    sheenGrad.Rotation = 62
    sheenGrad.Transparency = NumberSequence.new({
        NumberSequenceKeypoint.new(0, 0.1),
        NumberSequenceKeypoint.new(0.45, 0.85),
        NumberSequenceKeypoint.new(1, 1),
    })
    sheenGrad.Parent = sheen

    -- Vibrancy: a bit more saturation behind the glass while the menu is open.
    local old = Lighting:FindFirstChild("RMEXGlassCC")
    if old then old:Destroy() end
    local glassCC = Instance.new("ColorCorrectionEffect")
    glassCC.Name = "RMEXGlassCC"
    glassCC.Enabled = false
    glassCC.Parent = Lighting
    RX.glassCC = glassCC

    local drag = 0
    local lastX = nil
    local tiltX, tiltY = 0, 0
    RunService.RenderStepped:Connect(function(dt)
        local glass = currentTheme == "glass"
        rimGrad.Enabled = glass
        lens.Visible = glass
        sheen.Visible = glass
        if not glass or not menuOpen then return end
        local t = os.clock()
        -- phone tilt (gyro / accelerometer) moves the light; falls back to a slow drift
        local ok, cf = pcall(function()
            local _, c = UserInputService:GetDeviceRotation()
            return c
        end)
        if ok and cf and UserInputService.GyroscopeEnabled then
            local rx, ry = cf:ToOrientation()
            tiltX += (math.clamp(ry, -1, 1) - tiltX) * math.min(1, dt * 6)
            tiltY += (math.clamp(rx, -1, 1) - tiltY) * math.min(1, dt * 6)
        else
            tiltX = math.sin(t * 0.55) * 0.7
            tiltY = math.cos(t * 0.41) * 0.5
        end
        local px = panel.AbsolutePosition.X
        if lastX then drag += ((px - lastX) * 0.6 - drag) * math.min(1, dt * 8) end
        lastX = px
        local rot = 45 + tiltX * 55 + tiltY * 25 + drag
        rimGrad.Rotation = rot
        lensGrad.Rotation = rot
        sheenGrad.Rotation = 62 + tiltX * 30
        sheen.Position = UDim2.fromScale(math.clamp(tiltX * 0.06, -0.06, 0.06), 0)
    end)

    bindTheme(function(p, instant)
        local glass = currentTheme == "glass"
        local clear = RX.glassK / 100
        if glass then
            -- clearer glass = more see-through panel and cards
            panel.BackgroundTransparency = 0.62 - clear * 0.4
            panelGradient.Transparency = NumberSequence.new({
                NumberSequenceKeypoint.new(0, 0.0),
                NumberSequenceKeypoint.new(1, 0.2 + clear * 0.2),
            })
            shine.BackgroundTransparency = 0.93
        else
            panelGradient.Transparency = NumberSequence.new(0)
        end
        panelStroke.Color = glass and WHITE or p.stroke
        panelStroke.Transparency = glass and 0.05 or p.theme.strokeAlpha
        panelGlow.Transparency = glass and 1 or p.theme.glow
        setOrTween(tabBar, {BackgroundTransparency = glass and 0.7 or 0}, instant)
        setOrTween(closeBtn, {BackgroundTransparency = glass and 0.7 or 0}, instant)
        setOrTween(tabIndicator, {
            BackgroundTransparency = glass and 0.12 or 0,
            BackgroundColor3 = glass and p.accent:Lerp(WHITE, 0.45) or p.accent,
        }, instant)
        glassCC.Saturation = 0
    end)
    RX.glassRefresh = function() applyTheme(false) end
end

local function selectTab(index, instant)
    if index == currentTab then return end
    local dir = (currentTab == 0) and 0 or (index > currentTab and 1 or -1)
    local old = pages[currentTab]
    if old then old.Visible = false end
    currentTab = index

    local page = pages[index]
    page.Visible = true
    if instant or dir == 0 then
        page.Position = UDim2.new()
    else
        page.Position = UDim2.fromOffset(dir * 36, 0)
        tween(page, {Position = UDim2.new()}, 0.45)
        stagger(page)
    end

    setOrTween(tabIndicator, {Position = UDim2.new((index - 1) / TAB_COUNT, 2, 0, 2)}, instant, 0.45)
    for i, item in ipairs(tabButtons) do
        setOrTween(item.label, {TextColor3 = i == index and P.onAccent or P.muted}, instant, 0.35)
    end
end

for i, item in ipairs(tabButtons) do
    item.button.Activated:Connect(function() selectTab(i, false) end)
end

-- Menu animation ------------------------------------------------------------
-- A thin line opens sideways, then unfolds into the panel; the title is typed out
-- and a scan line sweeps down while the cards pop in. Closing plays it backwards.
do
    local TITLE = "RMEX VISUALS"
    local FULL_W, FULL_H = PANEL_W, PANEL_H

    local scan = Instance.new("Frame")
    scan.Name = "ScanLine"
    scan.AnchorPoint = Vector2.new(0, 0.5)
    scan.Size = UDim2.new(1, 0, 0, 2)
    scan.Position = UDim2.fromScale(0, 0)
    scan.BorderSizePixel = 0
    scan.Visible = false
    scan.ZIndex = 40
    scan.Parent = panel
    local scanFade = Instance.new("UIGradient")
    scanFade.Transparency = NumberSequence.new({
        NumberSequenceKeypoint.new(0, 1),
        NumberSequenceKeypoint.new(0.5, 0),
        NumberSequenceKeypoint.new(1, 1),
    })
    scanFade.Parent = scan

    -- Soft trail above the line (the area the line has already revealed).
    local trail = Instance.new("Frame")
    trail.Name = "ScanTrail"
    trail.AnchorPoint = Vector2.new(0, 1)
    trail.Position = UDim2.fromScale(0, 0)
    trail.Size = UDim2.new(1, 0, 0, 56)
    trail.BorderSizePixel = 0
    trail.ZIndex = 39
    trail.Parent = scan
    local trailFade = Instance.new("UIGradient")
    trailFade.Rotation = 90
    trailFade.Transparency = NumberSequence.new({
        NumberSequenceKeypoint.new(0, 1),
        NumberSequenceKeypoint.new(1, 0.72),
    })
    trailFade.Parent = trail

    bindTheme(function(p, instant)
        scan.BackgroundColor3 = p.accent
        trail.BackgroundColor3 = p.accent
    end)

    local function alive(token)
        return token == menuToken and menuOpen
    end

    local function typeTitle(token)
        local lbl = RX.title
        if not lbl then return end
        task.spawn(function()
            for i = 1, #TITLE do
                if not alive(token) then break end
                lbl.Text = string.sub(TITLE, 1, i) .. "_"
                task.wait(0.035)
            end
            lbl.Text = TITLE
        end)
    end

    function RX.menuOpenAnim(token)
        content.Visible = false
        panel.Size = UDim2.fromOffset(8, 2)
        panel.GroupTransparency = 1
        panelScale.Scale = RX.menuScale
        panel.Visible = true
        scan.Visible = false
        if RX.title then RX.title.Text = "" end

        tween(panel, {GroupTransparency = 0}, 0.1, Enum.EasingStyle.Quad)
        -- 1) the line grows sideways
        tween(panel, {Size = UDim2.fromOffset(FULL_W, 2)}, 0.2, Enum.EasingStyle.Quint)

        task.delay(0.17, function()
            if not alive(token) then return end
            -- 2) the line unfolds into the panel
            tween(panel, {Size = UDim2.fromOffset(FULL_W, FULL_H)}, 0.5, Enum.EasingStyle.Quint)
            typeTitle(token)
        end)
        task.delay(0.26, function()
            if alive(token) then content.Visible = true end
        end)
        task.delay(0.4, function()
            if not alive(token) then return end
            stagger(pages[currentTab])
            -- 3) scan line sweeps from top to bottom
            scan.Position = UDim2.fromScale(0, 0)
            scan.Visible = true
            tween(scan, {Position = UDim2.fromScale(0, 1)}, 0.6, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut)
        end)
        task.delay(1.05, function()
            if token == menuToken then scan.Visible = false end
        end)
    end

    function RX.menuCloseAnim(token)
        scan.Visible = false
        content.Visible = false
        tween(panel, {Size = UDim2.fromOffset(FULL_W, 2)}, 0.22, Enum.EasingStyle.Quint, Enum.EasingDirection.In)
        task.delay(0.19, function()
            if token ~= menuToken or menuOpen then return end
            tween(panel, {Size = UDim2.fromOffset(8, 2)}, 0.12, Enum.EasingStyle.Quint, Enum.EasingDirection.In)
            tween(panel, {GroupTransparency = 1}, 0.12, Enum.EasingStyle.Quad, Enum.EasingDirection.In)
        end)
        task.delay(0.33, function()
            if token == menuToken and not menuOpen then
                panel.Visible = false
                panel.Size = UDim2.fromOffset(FULL_W, FULL_H)
                content.Visible = true
                if RX.title then RX.title.Text = TITLE end
            end
        end)
    end
end


-- Open / close --------------------------------------------------------------
local function setMenu(open)
    if open == menuOpen then return end
    menuOpen = open
    menuToken += 1
    local token = menuToken

    launcher.Text = open and "×" or "R"
    local spin = tween(launcher, {Rotation = launcher.Rotation + 360}, 0.5, Enum.EasingStyle.Quint)
    spin.Completed:Connect(function()
        launcher.Rotation = launcher.Rotation % 360
    end)
    launcherScale.Scale = 0.8
    tween(launcherScale, {Scale = 1}, 0.45, Enum.EasingStyle.Back)

    if open then
        RX.menuOpenAnim(token)
    else
        RX.menuCloseAnim(token)
    end

    if open and P.theme.blur then
        glassBlur.Enabled = true
        tween(glassBlur, {Size = 18}, 0.4)
        if RX.glassCC then
            RX.glassCC.Enabled = true
            tween(RX.glassCC, {Saturation = 0.2, Brightness = 0.02}, 0.4)
        end
    else
        tween(glassBlur, {Size = 0}, 0.25)
        if RX.glassCC then
            tween(RX.glassCC, {Saturation = 0, Brightness = 0}, 0.25)
            task.delay(0.3, function() if not menuOpen then RX.glassCC.Enabled = false end end)
        end
        task.delay(0.27, function()
            if not (menuOpen and P.theme.blur) then glassBlur.Enabled = false end
        end)
    end
end

launcher.Activated:Connect(function()
    if not launcherDrag.moved then setMenu(not menuOpen) end
end)
closeBtn.Activated:Connect(function() setMenu(false) end)

-- ============================================================================
-- ZOOM WIDGET
-- ============================================================================

local zoomPanel = Instance.new("CanvasGroup")
zoomPanel.Name = "ZoomControls"
zoomPanel.AnchorPoint = Vector2.new(0.5, 0.5)
zoomPanel.Size = UDim2.fromOffset(100, 112)
zoomPanel.Position = UDim2.new(1, -70, 0.5, 0)
zoomPanel.GroupTransparency = 1
zoomPanel.Visible = false
zoomPanel.BorderSizePixel = 0
zoomPanel.Parent = gui
corner(zoomPanel, 12)
local zoomScale = Instance.new("UIScale")
zoomScale.Scale = 0.7
zoomScale.Parent = zoomPanel
local zoomStroke = Instance.new("UIStroke")
zoomStroke.Thickness = 1
zoomStroke.Parent = zoomPanel

bindTheme(function(p, instant)
    setOrTween(zoomPanel, {BackgroundColor3 = p.bg, BackgroundTransparency = p.theme.panelAlpha}, instant)
    setOrTween(zoomStroke, {Color = p.stroke, Transparency = p.theme.strokeAlpha}, instant)
end)

local zoomHeader = Instance.new("TextButton")
zoomHeader.Size = UDim2.new(1, 0, 0, 28)
zoomHeader.BackgroundTransparency = 1
zoomHeader.Text = ""
zoomHeader.AutoButtonColor = false
zoomHeader.ZIndex = 2
zoomHeader.Parent = zoomPanel
makeDraggable(zoomHeader, zoomPanel)
makeLabel(zoomHeader, {
    key = "zoom_title", pos = UDim2.fromOffset(0, 6), size = UDim2.new(1, 0, 0, 16),
    font = Enum.Font.GothamBold, textSize = 11, align = Enum.TextXAlignment.Center, role = "accent",
})

local zoomValue = makeLabel(zoomPanel, {
    text = "1x", pos = UDim2.new(0.5, 0, 0, 42), size = UDim2.new(1, 0, 0, 24),
    font = Enum.Font.GothamBold, textSize = 16, align = Enum.TextXAlignment.Center,
})
zoomValue.AnchorPoint = Vector2.new(0.5, 0.5)
local zoomPop = Instance.new("UIScale")
zoomPop.Parent = zoomValue

local minusBtn = Instance.new("TextButton")
minusBtn.Position = UDim2.fromOffset(8, 62)
minusBtn.Size = UDim2.fromOffset(40, 38)
minusBtn.Text = "−"
minusBtn.Font = Enum.Font.GothamBold
minusBtn.TextSize = 20
minusBtn.AutoButtonColor = false
minusBtn.BorderSizePixel = 0
minusBtn.Parent = zoomPanel
corner(minusBtn, 9)
addPress(minusBtn)

local plusBtn = Instance.new("TextButton")
plusBtn.Position = UDim2.fromOffset(52, 62)
plusBtn.Size = UDim2.fromOffset(40, 38)
plusBtn.Text = "+"
plusBtn.Font = Enum.Font.GothamBold
plusBtn.TextSize = 20
plusBtn.AutoButtonColor = false
plusBtn.BorderSizePixel = 0
plusBtn.Parent = zoomPanel
corner(plusBtn, 9)
addPress(plusBtn)

bindTheme(function(p, instant)
    setOrTween(minusBtn, {BackgroundColor3 = p.surface, TextColor3 = p.text}, instant)
    setOrTween(plusBtn, {BackgroundColor3 = p.accent, TextColor3 = p.onAccent}, instant)
end)

local function setZoom(level)
    local nz = math.clamp(level, 1, 120)
    if nz == zoomLevel then return end
    zoomLevel = nz
    zoomValue.Text = zoomLevel .. "x"
    zoomPop.Scale = 1.18
    tween(zoomPop, {Scale = 1}, 0.3, Enum.EasingStyle.Back)
end

local function holdZoom(button, amount)
    local holding = false
    local token = 0
    button.InputBegan:Connect(function(input)
        if not isPointer(input) then return end
        holding = true
        token += 1
        local my = token
        setZoom(zoomLevel + amount)
        task.spawn(function()
            task.wait(0.3)
            while holding and token == my do
                setZoom(zoomLevel + amount)
                task.wait(0.05)
            end
        end)
    end)
    UserInputService.InputEnded:Connect(function(input)
        if isPointer(input) then
            holding = false
            token += 1
        end
    end)
end
holdZoom(plusBtn, 1)
holdZoom(minusBtn, -1)

local function setZoomVisible(on)
    if on == zoomShown then return end
    zoomShown = on
    if on then
        zoomPanel.Visible = true
        zoomPanel.GroupTransparency = 1
        zoomScale.Scale = 0.7
        tween(zoomPanel, {GroupTransparency = 0}, 0.25, Enum.EasingStyle.Quad)
        tween(zoomScale, {Scale = 1}, 0.5, Enum.EasingStyle.Back)
    else
        tween(zoomPanel, {GroupTransparency = 1}, 0.18, Enum.EasingStyle.Quad, Enum.EasingDirection.In)
        tween(zoomScale, {Scale = 0.7}, 0.22, Enum.EasingStyle.Quint, Enum.EasingDirection.In)
        task.delay(0.24, function()
            if not zoomShown then zoomPanel.Visible = false end
        end)
    end
end

-- ============================================================================
-- SETTINGS PAGE
-- ============================================================================

makeSegmented(settingsPage, "language",
    {{key = "en_btn", value = "en"}, {key = "ru_btn", value = "ru"}},
    function() return lang end,
    function(v)
        lang = v
        refreshTexts()
    end)

local themeRefresh = makeSegmented(settingsPage, "theme",
    {
        {key = "theme_material", value = "material"},
        {key = "theme_glass", value = "glass"},
        {key = "theme_neon", value = "neon"},
    },
    function() return currentTheme end,
    function(v)
        currentTheme = v
        applyTheme(false)
    end)

local accentRefresh = makeSwatchRow(settingsPage, "accent", ACCENTS,
    function() return accent end,
    function(c)
        accent = c
        applyTheme(false)
    end)

makeSlider(settingsPage, {
    key = "glass_clarity", min = 0, max = 100,
    get = function() return RX.glassK end,
    set = function(v) RX.glassK = math.floor(v + 0.5) end,
    format = function(v) return math.floor(v + 0.5) .. "%" end,
    onChange = function() applyTheme(true) end,
})

stretchXRender = makeSlider(settingsPage, {
    key = "stretch_x", min = 50, max = 150,
    get = function() return esp.StretchX end,
    set = function(v) esp.StretchX = math.floor(v + 0.5) end,
    format = function(v) return math.floor(v + 0.5) .. "%" end,
})

stretchYRender = makeSlider(settingsPage, {
    key = "stretch_y", min = 50, max = 150,
    get = function() return esp.StretchY end,
    set = function(v) esp.StretchY = math.floor(v + 0.5) end,
    format = function(v) return math.floor(v + 0.5) .. "%" end,
})

local resetBtn = Instance.new("TextButton")
resetBtn.Size = UDim2.new(1, -6, 0, 34)
resetBtn.Text = ""
resetBtn.AutoButtonColor = false
resetBtn.BorderSizePixel = 0
resetBtn.LayoutOrder = nextOrder()
resetBtn.Parent = settingsPage
corner(resetBtn, 9)
addPop = addPopScale(resetBtn)
addPress(resetBtn)
makeLabel(resetBtn, {
    key = "reset", size = UDim2.fromScale(1, 1), font = Enum.Font.GothamBold,
    textSize = 10, align = Enum.TextXAlignment.Center, role = "accent",
})
bindTheme(function(p, instant)
    setOrTween(resetBtn, {BackgroundColor3 = p.surface}, instant)
end)
resetBtn.Activated:Connect(function()
    accent = ACCENTS[1]
    currentTheme = "material"
    esp.FOV = 70
    esp.StretchX = 100
    esp.StretchY = 100
    applyTheme(false)
    themeRefresh(false)
    accentRefresh(false)
    fovRender(false)
    stretchXRender(false)
    stretchYRender(false)
end)

-- ============================================================================
-- ESP PAGE
-- ============================================================================

for _, name in ipairs(ESP_ORDER) do
    makeToggleRow(espPage, {
        key = ESP_KEYS[name],
        get = function() return settings[name] end,
        set = function(v) settings[name] = v end,
        onChange = function() applySettings() end,
    })
end

for _, d in ipairs({{"radar", "Radar"}, {"arrows", "Arrows"}, {"headdot", "HeadDot"}, {"lookline", "LookLine"}}) do
    makeToggleRow(espPage, {
        key = d[1], desc = d[1] .. "_d",
        get = function() return settings[d[2]] end,
        set = function(v) settings[d[2]] = v end,
    })
end

makeSegmented(espPage, "tracer_origin",
    {{key = "o_bottom", value = "bottom"}, {key = "o_center", value = "center"}, {key = "o_top", value = "top"}},
    function() return esp.Origin end,
    function(v) esp.Origin = v end)

-- ============================================================================
-- VISUALS PAGE
-- ============================================================================

local personalToggles = {
    {key = "master", desc = "master_d", field = "Master"},
    {key = "aura", desc = "aura_d", field = "Aura"},
    {key = "particles", desc = "particles_d", field = "Particles"},
    {key = "rings", desc = "rings_d", field = "Rings"},
    {key = "swords", desc = "swords_d", field = "Swords"},
    {key = "orbs", desc = "orbs_d", field = "Orbs"},
    {key = "trails", desc = "trails_d", field = "Trails"},
    {key = "halo", desc = "halo_d", field = "Halo"},
    {key = "hat", desc = "hat_d", field = "Hat"},
    {key = "chat", desc = "chat_d", field = "ChineseHat"},
    {key = "fire", desc = "fire_d", field = "Fire"},
    {key = "petals", desc = "petals_d", field = "Petals"},
    {key = "crystals", desc = "crystals_d", field = "Crystals"},
    {key = "runes", desc = "runes_d", field = "Runes"},
    {key = "smoke", desc = "smoke_d", field = "Smoke"},
    {key = "sabers", desc = "sabers_d", field = "Sabers"},
    {key = "pulse", desc = "pulse_d", field = "Pulse"},
    {key = "wind", desc = "wind_d", field = "Wind"},
    {key = "streaks", desc = "streaks_d", field = "Streaks"},
    {key = "ghost", desc = "ghost_d", field = "Ghost"},
    {key = "wings", desc = "wings_d", field = "Wings"},
    {key = "lightning", desc = "lightning_d", field = "Lightning"},
    {key = "far", desc = "far_d", field = "FarLightning"},
    {key = "glitch", desc = "glitch_d", field = "Glitch"},
    {key = "footsteps", desc = "footsteps_d", field = "Footsteps"},
    {key = "jumps", desc = "jumps_d", field = "Jumps"},
    {key = "rush", desc = "rush_d", field = "Rush"},
    {key = "arcs", desc = "arcs_d", field = "Arcs"},
    {key = "grid", desc = "grid_d", field = "Grid"},
    {key = "speedlines", desc = "speedlines_d", field = "SpeedLines"},
    {key = "chroma", desc = "chroma_d", field = "Chroma"},
    {key = "glitchbars", desc = "glitchbars_d", field = "GlitchBars"},
    {key = "grade", desc = "grade_d", field = "Grade"},
    {key = "scanner", desc = "scanner_d", field = "Scanner"},
    {key = "matrix", desc = "matrix_d", field = "Matrix"},
    {key = "vortex", desc = "vortex_d", field = "Vortex"},
    {key = "helix", desc = "helix_d", field = "Helix"},
    {key = "comets", desc = "comets_d", field = "Comets"},
    {key = "ribbons", desc = "ribbons_d", field = "Ribbons"},
    {key = "bubble", desc = "bubble_d", field = "Bubble"},
    {key = "cage", desc = "cage_d", field = "Cage"},
    {key = "laser", desc = "laser_d", field = "Laser"},
    {key = "tag", desc = "tag_d", field = "Tag"},
    {key = "evadetrail", desc = "evadetrail_d", field = "EvadeTrail"},
    {key = "afterimage", desc = "afterimage_d", field = "AfterImage"},
    {key = "airribbons", desc = "airribbons_d", field = "AirRibbons"},
    {key = "dustkick", desc = "dustkick_d", field = "DustKick"},
    {key = "shockwave", desc = "shockwave_d", field = "Shockwave"},
    {key = "meteors", desc = "meteors_d", field = "Meteors"},
    {key = "pillar", desc = "pillar_d", field = "Pillar"},
    {key = "blackhole", desc = "blackhole_d", field = "BlackHole"},
    {key = "dragon", desc = "dragon_d", field = "Dragon"},
    {key = "sigil", desc = "sigil_d", field = "Sigil"},
    {key = "impact", desc = "impact_d", field = "Impact"},
}
do
    local PRE = {
        anime = {on = {"ChineseHat", "Halo", "Particles", "Petals", "Wings"}, color = EFFECT_COLORS[6]},
        dark = {on = {"Aura", "Smoke", "Wings", "Lightning", "Runes"}, color = EFFECT_COLORS[9],
            per = {Runes = {Color = EFFECT_COLORS[5]}, Lightning = {Color = EFFECT_COLORS[5]}}},
        fire = {on = {"Fire", "Aura", "Particles", "Trails"}, color = EFFECT_COLORS[2]},
        ice = {on = {"Crystals", "Petals", "Halo", "Trails", "Rings"}, color = EFFECT_COLORS[4],
            per = {Petals = {Anim = 2}}},
        neon = {on = {"Aura", "Wings", "Rings", "Pulse", "ChineseHat", "Orbs", "Particles"}, color = Color3.fromRGB(215, 70, 255),
            tint = {on = true, color = Color3.fromRGB(190, 70, 255)}},
        mono = {on = {"Aura", "Wings", "Rings", "Pulse", "Halo"}, color = Color3.fromRGB(255, 255, 255),
            tint = {on = true, mono = true}},
        epic = {on = {"Sigil", "Pillar", "Dragon", "Shockwave", "Meteors", "Impact", "Aura", "Wings", "Grade"},
            color = Color3.fromRGB(150, 110, 255),
            per = {Meteors = {Color = Color3.fromRGB(255, 120, 45)}, Sigil = {Color = Color3.fromRGB(255, 205, 70)},
                Pillar = {Color = Color3.fromRGB(110, 210, 255)}, Dragon = {Color = Color3.fromRGB(60, 255, 170)}}},
        off = {on = {}},
    }
    local function applyPreset(p)
        local set = {}
        for _, f in ipairs(p.on) do set[f] = true end
        for _, item in ipairs(personalToggles) do
            if item.field ~= "Master" then visual[item.field] = set[item.field] or false end
        end
        if #p.on > 0 then visual.Master = true end
        screenFX.Tint = p.tint ~= nil and p.tint.on or false
        if p.tint then
            if p.tint.color then RX.tint.Color = p.tint.color end
            RX.tint.Mono = p.tint.mono or false
        end
        if p.color then visual.Color = p.color; visual.Rainbow = false end
        for f, c in pairs(visual.cfg) do
            if set[f] then c.Color = nil; c.Anim = 1 end
        end
        for f, o in pairs(p.per or {}) do
            for k, v in pairs(o) do visual.cfg[f][k] = v end
        end
        refreshVisualUI(false)
        for _, r in ipairs(RX.renders) do r(false) end
        RX.beep(true)
    end

    local card = makeCard(visualsPage, 88)
    makeLabel(card, {key = "preset_title", pos = UDim2.fromOffset(10, 6), size = UDim2.new(1, -20, 0, 14), textSize = 10, role = "muted"})
    local row = Instance.new("Frame")
    row.BackgroundTransparency = 1
    row.Position = UDim2.fromOffset(6, 26)
    row.Size = UDim2.new(1, -12, 0, 56)
    row.Parent = card
    local n = 4
    for i, key in ipairs({"anime", "dark", "fire", "ice", "neon", "mono", "epic", "off"}) do
        local b = Instance.new("TextButton")
        b.Position = UDim2.new(((i - 1) % n) / n, 2, 0, math.floor((i - 1) / n) * 30)
        b.Size = UDim2.new(1 / n, -4, 0, 26)
        b.Text = ""
        b.AutoButtonColor = false
        b.BorderSizePixel = 0
        b.Parent = row
        corner(b, 7)
        local lbl = makeLabel(b, {
            key = "pr_" .. key, size = UDim2.fromScale(1, 1), font = Enum.Font.GothamBold,
            textSize = 9, align = Enum.TextXAlignment.Center, role = false, zindex = 3,
        })
        addPress(b, 0.95)
        b.Activated:Connect(function() applyPreset(PRE[key]) end)
        bindTheme(function(p, instant)
            setOrTween(b, {BackgroundColor3 = p.bg}, instant)
            setOrTween(lbl, {TextColor3 = p.accent}, instant)
        end)
    end
end

do
    local GLOBAL_MARK = Color3.fromRGB(120, 120, 128)
    local palette = {GLOBAL_MARK}
    for _, col in ipairs(EFFECT_COLORS) do table.insert(palette, col) end

    local function addSettings(rowCard, field)
        local cap = RX.CAPS[field]
        local c = visual.cfg[field]
        local startOrder = orderSeq
        if cap.ghost then
            makeSlider(visualsPage, {
                key = "ghost_alpha", min = 5, max = 100,
                get = function() return visual.GhostAlpha end,
                set = function(v) visual.GhostAlpha = math.floor(v + 0.5) end,
                format = function(v) return math.floor(v + 0.5) .. "%" end,
            })
            makeSlider(visualsPage, {
                key = "ghost_delay", min = 0.1, max = 1.5,
                get = function() return visual.GhostDelay end,
                set = function(v) visual.GhostDelay = math.floor(v * 20 + 0.5) / 20 end,
                format = function(v) return string.format("%.2fs", v) end,
            })
        else
            if cap.sp then
                makeSlider(visualsPage, {
                    key = "speed", min = 0.2, max = 3,
                    get = function() return c.Speed end,
                    set = function(v) c.Speed = math.floor(v * 20 + 0.5) / 20 end,
                    format = function(v) return string.format("x%.2f", v) end,
                })
            end
            if cap.sz then
                makeSlider(visualsPage, {
                    key = "size", min = 0.4, max = 2.5,
                    get = function() return c.Size end,
                    set = function(v) c.Size = math.floor(v * 20 + 0.5) / 20 end,
                    format = function(v) return string.format("x%.2f", v) end,
                })
            end
            if cap.int then
                makeSlider(visualsPage, {
                    key = "intensity", min = 5, max = 100,
                    get = function() return c.Intensity end,
                    set = function(v) c.Intensity = math.floor(v + 0.5) end,
                    format = function(v) return math.floor(v + 0.5) .. "%" end,
                })
            end
            if cap.a and cap.a > 1 then
                local opts = {}
                for i = 1, cap.a do opts[i] = {key = "an_" .. field .. "_" .. i, value = i} end
                makeSegmented(visualsPage, "anim", opts,
                    function() return c.Anim end,
                    function(v) c.Anim = v end)
            end
            if cap.m then
                local mo = {}
                for i = 1, 5 do mo[i] = {key = "mo_" .. i, value = i} end
                makeSegmented(visualsPage, "motion", mo,
                    function() return c.Motion or 1 end,
                    function(v) c.Motion = v end)
                local fl = {}
                for i = 1, 4 do fl[i] = {key = "fl_" .. i, value = i} end
                makeSegmented(visualsPage, "flow", fl,
                    function() return c.Flow or 1 end,
                    function(v) c.Flow = v end)
            end
            makeSwatchRow(visualsPage, "ecolor", palette,
                function() return c.Color or GLOBAL_MARK end,
                function(col) c.Color = (col ~= GLOBAL_MARK) and col or nil end,
                {[1] = "A"})
        end
        local subs = {}
        for _, ch in ipairs(visualsPage:GetChildren()) do
            if ch:IsA("Frame") and ch.LayoutOrder > startOrder then
                ch.Visible = false
                table.insert(subs, ch)
            end
        end
        local btn = Instance.new("TextButton")
        btn.AnchorPoint = Vector2.new(1, 0.5)
        btn.Position = UDim2.new(1, -58, 0.5, 0)
        btn.Size = UDim2.fromOffset(22, 22)
        btn.Text = "+"
        btn.Font = Enum.Font.GothamBold
        btn.TextSize = 14
        btn.AutoButtonColor = false
        btn.BorderSizePixel = 0
        btn.ZIndex = 3
        btn.Parent = rowCard
        corner(btn, 999)
        addPress(btn, 0.88)
        bindTheme(function(p, instant)
            setOrTween(btn, {BackgroundColor3 = p.bg, TextColor3 = p.accent}, instant)
        end)
        local open = false
        btn.Activated:Connect(function()
            open = not open
            btn.Text = open and "-" or "+"
            for _, s in ipairs(subs) do s.Visible = open end
        end)
    end

    local function headerCard(key)
        local c = makeCard(visualsPage, 22)
        makeLabel(c, {key = key, pos = UDim2.fromOffset(10, 0), size = UDim2.new(1, -20, 1, 0), textSize = 10, font = Enum.Font.GothamBold, role = "accent"})
    end
    local function actionButton(key, fn)
        local c = makeCard(visualsPage, 32)
        local b = Instance.new("TextButton")
        b.Position = UDim2.fromOffset(6, 4)
        b.Size = UDim2.new(1, -12, 1, -8)
        b.Text = ""
        b.AutoButtonColor = false
        b.BorderSizePixel = 0
        b.Parent = c
        corner(b, 7)
        addPress(b, 0.96)
        makeLabel(b, {key = key, size = UDim2.fromScale(1, 1), font = Enum.Font.GothamBold, textSize = 10,
            align = Enum.TextXAlignment.Center, role = "accent", zindex = 3})
        bindTheme(function(p, instant) setOrTween(b, {BackgroundColor3 = p.bg}, instant) end)
        b.Activated:Connect(fn)
    end
    headerCard("meta_head")
    makeToggleRow(visualsPage, {key = "ritual", desc = "ritual_d",
        get = function() return visual.Ritual end, set = function(v) visual.Ritual = v end})
    actionButton("ritual_btn", function() if RX.ritualPlay then RX.ritualPlay() end end)
    makeToggleRow(visualsPage, {key = "detect", desc = "detect_d",
        get = function() return visual.Detect end, set = function(v) visual.Detect = v end})
    actionButton("detect_btn", function() if RX.detectTest then RX.detectTest() end end)

    for _, item in ipairs(personalToggles) do
        if item.field == "Rush" then headerCard("new_head") end
        if item.field == "EvadeTrail" then headerCard("evade_head") end
        if item.field == "Shockwave" then headerCard("epic_head") end
        local hasCfg = RX.CAPS[item.field] ~= nil
        local _, rowCard = makeToggleRow(visualsPage, {
            key = item.key,
            desc = item.desc,
            pad = hasCfg and 92 or 62,
            get = function() return visual[item.field] end,
            set = function(v) visual[item.field] = v end,
        })
        if hasCfg then addSettings(rowCard, item.field) end
    end
end

local visualSwatchRefresh = makeSwatchRow(visualsPage, "effect_color", EFFECT_COLORS,
    function() return visual.Color end,
    function(c)
        visual.Color = c
        visual.Rainbow = false
        if rainbowRender then rainbowRender(false) end
        refreshVisualUI(false)
    end)

local previewCard = makeCard(visualsPage, 40)
local previewFrame = Instance.new("Frame")
previewFrame.Position = UDim2.fromOffset(10, 8)
previewFrame.Size = UDim2.fromOffset(24, 24)
previewFrame.BorderSizePixel = 0
previewFrame.Parent = previewCard
corner(previewFrame, 6)
local hexLabel = makeLabel(previewCard, {
    pos = UDim2.fromOffset(44, 0), size = UDim2.new(1, -54, 1, 0),
    font = Enum.Font.GothamBold, textSize = 10, role = "muted",
})

local visualRenders = {}
for _, ch in ipairs({"R", "G", "B"}) do
    local key = ch == "R" and "red" or (ch == "G" and "green" or "blue")
    table.insert(visualRenders, makeSlider(visualsPage, {
        key = key, min = 0, max = 255,
        get = function()
            local r, g, b = rgbInts(visual.Color)
            if ch == "R" then return r elseif ch == "G" then return g end
            return b
        end,
        set = function(v)
            local r, g, b = rgbInts(visual.Color)
            v = math.floor(v + 0.5)
            if ch == "R" then r = v elseif ch == "G" then g = v else b = v end
            visual.Color = Color3.fromRGB(r, g, b)
            visual.Rainbow = false
        end,
        format = function(v) return tostring(math.floor(v + 0.5)) end,
        onChange = function()
            if rainbowRender then rainbowRender(true) end
            refreshVisualUI(true)
        end,
    }))
end

rainbowRender = makeToggleRow(visualsPage, {
    key = "rainbow",
    get = function() return visual.Rainbow end,
    set = function(v) visual.Rainbow = v end,
    onChange = function() refreshVisualUI(false) end,
})

makeSlider(visualsPage, {
    key = "rainbow_speed", min = 5, max = 100,
    get = function() return visual.RainbowSpeed end,
    set = function(v) visual.RainbowSpeed = math.floor(v + 0.5) end,
    format = function(v) return tostring(math.floor(v + 0.5)) end,
})


local function getEffectColor()
    if visual.Rainbow then
        return Color3.fromHSV(rainbowHue, 0.86, 1)
    end
    return visual.Color
end


-- v12: Motion + Color-flow styles, shared by the old effects (via FXC) and the new ones
RX.fxMod = {prox = {}}
do
    local prox = RX.fxMod.prox
    function RX.fxMod.apply(name, C, t, base)
        local p = prox[name]
        if not p then
            p = {}
            prox[name] = p
        end
        p.Speed, p.Size, p.Anim, p.Intensity, p.Color = C.Speed, C.Size, C.Anim, C.Intensity, C.Color
        local m = C.Motion or 1
        if m == 2 then
            p.Size = C.Size * (1 + 0.22 * math.sin(t * 2.1))
        elseif m == 3 then
            local s = math.max(0, math.sin(t * 1.4))
            p.Speed = C.Speed * (1 + 1.6 * s * s)
        elseif m == 4 then
            local ph = (t * 1.3) % 1
            local beat = math.exp(-ph * 9) + 0.6 * math.exp(-math.abs(ph - 0.28) * 14)
            p.Size = C.Size * (1 + 0.32 * beat)
        elseif m == 5 then
            p.Size = C.Size * (1 + 0.5 * math.noise(t * 2.3, 1.7))
            p.Speed = C.Speed * (1 + 0.5 * math.noise(t * 1.9, 8.1))
        end
        local c = base
        local f = C.Flow or 1
        if f == 2 then
            local h, s, v = c:ToHSV()
            c = Color3.fromHSV((h + 0.09 * math.sin(t * 0.9)) % 1, s, v)
        elseif f == 3 then
            local ph = (t * 1.7) % 1
            c = c:Lerp(Color3.new(1, 1, 1), math.exp(-ph * 7) * 0.85)
        elseif f == 4 then
            local h, s, v = c:ToHSV()
            c = c:Lerp(Color3.fromHSV((h + 0.5) % 1, s, v), 0.5 + 0.5 * math.sin(t * 0.8))
        end
        return p, c
    end
end

refreshVisualUI = function(instant)
    visualSwatchRefresh(instant)
    for _, render in ipairs(visualRenders) do render(instant) end
    if rainbowRender then rainbowRender(instant) end
    local r, g, b = rgbInts(visual.Color)
    setOrTween(previewFrame, {BackgroundColor3 = visual.Color}, instant, 0.3)
    hexLabel.Text = visual.Rainbow and STRINGS[lang].rainbow_label
        or string.format("#%02X%02X%02X", r, g, b)
end
refreshVisualUI(true)
table.insert(langHooks, function() refreshVisualUI(true) end)

-- ============================================================================
-- SHADERS: day / sunset / night / mirror world (client-side only)
-- ============================================================================
-- Lighting, Atmosphere, Bloom, ColorCorrection, SunRays and the stars are blended from
-- the world's own values toward the chosen look, so switching modes (or turning the
-- feature off) is a smooth fade. "Mirror" also makes every map part glossy
-- (Reflectance + Metal) and the water reflective. Characters keep their own look.
-- Only this player sees any of it: client changes to Lighting / parts are not replicated.
RX.sh = {On = false, Mode = "day", Strength = 100, Mirror = 85, dirty = false}
do
    local SH = RX.sh
    local C = Color3.fromRGB

    local FIELDS = {
        "Clock", "Bright", "Amb", "Out", "Top", "Bot", "Exp", "Dif", "Spe",
        "aDen", "aOff", "aCol", "aDec", "aGla", "aHaz",
        "bInt", "bSiz", "bThr", "cBri", "cCon", "cSat", "cTint", "rInt", "rSpr", "stars",
    }

    local LOOKS = {
        day = {
            Clock = 13.2, Bright = 3, Amb = C(105, 112, 125), Out = C(150, 160, 178),
            Top = C(255, 246, 228), Bot = C(0, 0, 0), Exp = 0.1, Dif = 1, Spe = 1,
            aDen = 0.28, aOff = 0.25, aCol = C(190, 214, 245), aDec = C(160, 190, 225), aGla = 0.3, aHaz = 0.8,
            bInt = 0.35, bSiz = 24, bThr = 1.1, cBri = 0, cCon = 0.06, cSat = 0.12, cTint = C(255, 250, 242),
            rInt = 0.08, rSpr = 0.7, stars = 0,
        },
        sunset = {
            Clock = 17.9, Bright = 2.4, Amb = C(70, 50, 70), Out = C(130, 90, 100),
            Top = C(255, 150, 80), Bot = C(90, 50, 90), Exp = 0.25, Dif = 1, Spe = 1,
            aDen = 0.38, aOff = 0.3, aCol = C(255, 185, 140), aDec = C(255, 120, 80), aGla = 0.8, aHaz = 2,
            bInt = 0.7, bSiz = 30, bThr = 0.95, cBri = 0, cCon = 0.1, cSat = 0.2, cTint = C(255, 236, 222),
            rInt = 0.18, rSpr = 0.9, stars = 0,
        },
        night = {
            Clock = 23.6, Bright = 0.9, Amb = C(35, 40, 75), Out = C(55, 65, 120),
            Top = C(140, 160, 255), Bot = C(0, 0, 0), Exp = 0.35, Dif = 1, Spe = 1,
            aDen = 0.4, aOff = 0, aCol = C(40, 50, 110), aDec = C(15, 20, 55), aGla = 0, aHaz = 1.5,
            bInt = 0.9, bSiz = 30, bThr = 0.9, cBri = 0, cCon = 0.15, cSat = 0.1, cTint = C(225, 235, 255),
            rInt = 0, rSpr = 0.5, stars = 3000,
        },
        neon = {
            Clock = 0, Bright = 1.1, Amb = C(70, 20, 90), Out = C(90, 35, 120),
            Top = C(255, 60, 200), Bot = C(120, 255, 40), Exp = 0.1, Dif = 1, Spe = 1,
            aDen = 0.35, aOff = 0, aCol = C(70, 20, 100), aDec = C(30, 10, 60), aGla = 0, aHaz = 1.2,
            bInt = 1.3, bSiz = 38, bThr = 0.75, cBri = -0.03, cCon = 0.3, cSat = 0.55, cTint = C(245, 230, 255),
            rInt = 0, rSpr = 0.5, stars = 2500,
        },
        mirror = {
            Clock = 14.5, Bright = 3.2, Amb = C(130, 140, 160), Out = C(170, 185, 210),
            Top = C(255, 255, 255), Bot = C(0, 0, 0), Exp = 0.25, Dif = 1, Spe = 1,
            aDen = 0.18, aOff = 0, aCol = C(205, 225, 250), aDec = C(150, 180, 215), aGla = 0.4, aHaz = 0.3,
            bInt = 0.8, bSiz = 28, bThr = 0.85, cBri = 0.02, cCon = 0.2, cSat = -0.05, cTint = C(245, 250, 255),
            rInt = 0.1, rSpr = 0.8, stars = 0,
        },
    }

    local function lerp(a, b, t)
        if typeof(a) == "Color3" then return a:Lerp(b, t) end
        return a + (b - a) * t
    end

    local base, cur = nil, nil
    local I = {}            -- instances: atm, bloom, cc, rays, sky
    local ownAtm = false    -- true when we created the Atmosphere ourselves
    local active = false
    local offTimer = 0

    local function getFX(className, name)
        local e = Lighting:FindFirstChild(name)
        if e and e.ClassName ~= className then
            e:Destroy()
            e = nil
        end
        if not e then
            e = Instance.new(className)
            e.Name = name
            e.Parent = Lighting
        end
        return e
    end

    -- Values the world has right now. While "Always visible" is on it owns a few of the
    -- lighting values, so we read the world's real ones from its saved copy.
    local function snapshot()
        local fb = RX.fb
        local old = Lighting:FindFirstChild("RMEXShaderAtmosphere")
        if old then old:Destroy() end
        local atm = Lighting:FindFirstChildOfClass("Atmosphere")
        local sky = Lighting:FindFirstChildOfClass("Sky")
        local b = {
            Clock = Lighting.ClockTime,
            Bright = fb and fb.B or Lighting.Brightness,
            Amb = fb and fb.A or Lighting.Ambient,
            Out = fb and fb.O or Lighting.OutdoorAmbient,
            Top = Lighting.ColorShift_Top, Bot = Lighting.ColorShift_Bottom,
            Exp = fb and fb.E or Lighting.ExposureCompensation,
            Dif = Lighting.EnvironmentDiffuseScale, Spe = Lighting.EnvironmentSpecularScale,
            bInt = 0, bSiz = 24, bThr = 1, cBri = 0, cCon = 0, cSat = 0, cTint = C(255, 255, 255),
            rInt = 0, rSpr = 0.5,
            stars = sky and sky.StarCount or 0,
        }
        if atm then
            b.aDen = (fb and fb.atm == atm and fb.D) or atm.Density
            b.aOff, b.aCol, b.aDec = atm.Offset, atm.Color, atm.Decay
            b.aGla, b.aHaz = atm.Glare, atm.Haze
            I.atm, ownAtm = atm, false
        else
            b.aDen, b.aOff, b.aCol, b.aDec = 0, 0, C(199, 199, 199), C(106, 112, 125)
            b.aGla, b.aHaz = 0, 0
            I.atm = Instance.new("Atmosphere")
            I.atm.Name = "RMEXShaderAtmosphere"
            I.atm.Density = 0
            I.atm.Parent = Lighting
            ownAtm = true
        end
        I.sky = sky
        return b
    end

    local function begin()
        base = snapshot()
        cur = {}
        for _, f in ipairs(FIELDS) do cur[f] = base[f] end
        I.bloom = getFX("BloomEffect", "RMEXShaderBloom")
        I.cc = getFX("ColorCorrectionEffect", "RMEXShaderCC")
        I.rays = getFX("SunRaysEffect", "RMEXShaderRays")
        I.bloom.Intensity, I.bloom.Size, I.bloom.Threshold = base.bInt, base.bSiz, base.bThr
        I.rays.Intensity, I.rays.Spread = base.rInt, base.rSpr
        active = true
        offTimer = 0
    end

    local function apply()
        Lighting.ClockTime = math.clamp(cur.Clock, 0, 23.99)
        Lighting.ColorShift_Top = cur.Top
        Lighting.ColorShift_Bottom = cur.Bot
        Lighting.EnvironmentDiffuseScale = math.clamp(cur.Dif, 0, 1)
        Lighting.EnvironmentSpecularScale = math.clamp(cur.Spe, 0, 1)
        local fbOwns = screenFX.Bright  -- "Always visible" controls these while it is on
        if not fbOwns then
            Lighting.Brightness = cur.Bright
            Lighting.Ambient = cur.Amb
            Lighting.OutdoorAmbient = cur.Out
            Lighting.ExposureCompensation = cur.Exp
        end
        local atm = I.atm
        if atm and atm.Parent then
            if not fbOwns then atm.Density = math.clamp(cur.aDen, 0, 1) end
            atm.Offset = math.clamp(cur.aOff, 0, 1)
            atm.Color, atm.Decay = cur.aCol, cur.aDec
            atm.Glare = math.max(cur.aGla, 0)
            atm.Haze = math.max(cur.aHaz, 0)
        end
        local bl, cc, rays = I.bloom, I.cc, I.rays
        if bl and bl.Parent then
            bl.Enabled = true
            bl.Intensity, bl.Size, bl.Threshold = math.max(cur.bInt, 0), math.max(cur.bSiz, 0), math.max(cur.bThr, 0)
        end
        if cc and cc.Parent then
            cc.Enabled = true
            cc.Brightness = math.clamp(cur.cBri, -1, 1)
            cc.Contrast = math.clamp(cur.cCon, -1, 1)
            cc.Saturation = math.clamp(cur.cSat, -1, 1)
            cc.TintColor = cur.cTint
        end
        if rays and rays.Parent then
            rays.Enabled = true
            rays.Intensity = math.clamp(cur.rInt, 0, 1)
            rays.Spread = math.clamp(cur.rSpr, 0, 1)
        end
        local sky = I.sky
        if sky and sky.Parent then
            local stars = math.floor(math.clamp(cur.stars, 0, 5000) + 0.5)
            if sky.StarCount ~= stars then sky.StarCount = stars end
        end
    end

    -- Back to the world's exact original values, then clean up.
    local function finish()
        active = false
        local fb = RX.fb
        Lighting.ClockTime = base.Clock
        Lighting.ColorShift_Top = base.Top
        Lighting.ColorShift_Bottom = base.Bot
        Lighting.EnvironmentDiffuseScale = base.Dif
        Lighting.EnvironmentSpecularScale = base.Spe
        if fb then
            fb.B, fb.A, fb.O, fb.E = base.Bright, base.Amb, base.Out, base.Exp
            if fb.atm == I.atm then fb.D = base.aDen end
        else
            Lighting.Brightness = base.Bright
            Lighting.Ambient = base.Amb
            Lighting.OutdoorAmbient = base.Out
            Lighting.ExposureCompensation = base.Exp
        end
        local atm = I.atm
        if atm and atm.Parent then
            if ownAtm then
                atm:Destroy()
            else
                if not fb or fb.atm ~= atm then atm.Density = base.aDen end
                atm.Offset, atm.Color, atm.Decay = base.aOff, base.aCol, base.aDec
                atm.Glare, atm.Haze = base.aGla, base.aHaz
            end
        end
        if I.sky and I.sky.Parent then I.sky.StarCount = base.stars end
        for _, e in ipairs({I.bloom, I.cc, I.rays}) do
            if e and e.Parent then e:Destroy() end
        end
        I.atm, I.bloom, I.cc, I.rays, I.sky = nil, nil, nil, nil, nil
    end

    ----------------------------------------------------------------------
    -- Mirror world: every map part turns into glossy chrome
    ----------------------------------------------------------------------
    local mirror = {orig = setmetatable({}, {__mode = "k"}), on = false, token = 0, conn = nil, water = nil}
    -- Materials that already look right (or are see-through) are kept as they are.
    local KEEP = {
        [Enum.Material.Glass] = true, [Enum.Material.Neon] = true, [Enum.Material.ForceField] = true,
        [Enum.Material.Foil] = true, [Enum.Material.Metal] = true, [Enum.Material.DiamondPlate] = true,
        [Enum.Material.CorrodedMetal] = true, [Enum.Material.Ice] = true,
    }

    local function mirrorLevel()
        return math.clamp(SH.Mirror / 100, 0, 1)
    end

    local function isTarget(part)
        if part:IsA("Terrain") or part.Transparency >= 0.99 then return false end
        if part:FindFirstAncestor("RMEX_FX") then return false end
        if part:FindFirstChildOfClass("SurfaceAppearance") then return false end -- own PBR maps
        local model = part:FindFirstAncestorOfClass("Model")
        if model and model:FindFirstChildOfClass("Humanoid") then return false end -- characters / NPCs
        return true
    end

    local function mirrorApply(part)
        if not mirror.on then return end
        local o = mirror.orig[part]
        if not o then
            if not isTarget(part) then return end
            o = {R = part.Reflectance, M = part.Material}
            mirror.orig[part] = o
            if not KEEP[part.Material] then part.Material = Enum.Material.Metal end
        end
        part.Reflectance = mirrorLevel()
    end

    local function setMirror(on)
        mirror.token += 1
        local tok = mirror.token
        mirror.on = on
        if mirror.conn then
            mirror.conn:Disconnect()
            mirror.conn = nil
        end
        local terrain = workspace:FindFirstChildOfClass("Terrain")
        if on then
            if terrain then
                pcall(function()
                    if not mirror.water then mirror.water = {R = terrain.WaterReflectance} end
                    terrain.WaterReflectance = 1
                end)
            end
            mirror.conn = workspace.DescendantAdded:Connect(function(inst)
                if inst:IsA("BasePart") then task.defer(mirrorApply, inst) end
            end)
            -- Done in small slices so a big map does not freeze the phone.
            task.spawn(function()
                local n = 0
                for _, inst in ipairs(workspace:GetDescendants()) do
                    if tok ~= mirror.token then return end
                    if inst:IsA("BasePart") then
                        mirrorApply(inst)
                        n += 1
                        if n % 200 == 0 then RunService.Heartbeat:Wait() end
                    end
                end
            end)
        else
            if terrain and mirror.water then
                pcall(function() terrain.WaterReflectance = mirror.water.R end)
            end
            mirror.water = nil
            task.spawn(function()
                local list = {}
                for part in pairs(mirror.orig) do list[#list + 1] = part end
                for i, part in ipairs(list) do
                    if tok ~= mirror.token then return end
                    local o = mirror.orig[part]
                    if o then
                        if part.Parent then
                            part.Reflectance = o.R
                            part.Material = o.M
                        end
                        mirror.orig[part] = nil
                    end
                    if i % 200 == 0 then RunService.Heartbeat:Wait() end
                end
            end)
        end
    end

    -- Shine slider moved: update every part we already changed (one pass at a time).
    local refreshing = false
    local function refreshMirror()
        if not mirror.on or refreshing then return end
        refreshing = true
        local tok = mirror.token
        task.spawn(function()
            local list = {}
            for part in pairs(mirror.orig) do list[#list + 1] = part end
            local lvl = mirrorLevel()
            for i, part in ipairs(list) do
                if tok ~= mirror.token then break end
                if part.Parent then part.Reflectance = lvl end
                if i % 300 == 0 then RunService.Heartbeat:Wait() end
            end
            refreshing = false
        end)
    end

    ----------------------------------------------------------------------
    -- Per-frame blend
    ----------------------------------------------------------------------
    RunService.RenderStepped:Connect(function(dt)
        local on = SH.On
        if on and not active then begin() end
        if not active then return end

        local look = LOOKS[SH.Mode] or LOOKS.day
        local k = on and (SH.Strength / 100) or 0
        local a = 1 - math.exp(-dt * 3.2)
        for _, f in ipairs(FIELDS) do
            cur[f] = lerp(cur[f], lerp(base[f], look[f], k), a)
        end
        apply()

        local wantMirror = on and SH.Mode == "mirror" and SH.Tier ~= 2
        if wantMirror ~= mirror.on then setMirror(wantMirror) end
        if SH.dirty then
            SH.dirty = false
            refreshMirror()
        end

        if on then
            offTimer = 0
        else
            offTimer += dt
            if offTimer > 1.8 then finish() end
        end
    end)
end


-- ============================================================================
-- ULTRA MIRROR: real reflections. The floor under you becomes glossy glass and a mirrored
-- copy of nearby objects + all players is placed under it (client only). Roblox's own
-- Reflectance cannot reflect nearby objects, only the sky - this is the real thing.
-- ============================================================================
RX.sh.Tier, RX.sh.Range, RX.sh.Detail, RX.sh.Clear = 1, 130, 350, 60
do
    local SH = RX.sh
    local Players = game:GetService("Players")
    local plane = nil               -- Y of the mirror plane
    local folder = nil
    local proxies = {}              -- original part -> {clone = part, static = bool, last = CFrame}
    local floors = setmetatable({}, {__mode = "k"})
    local floorList = {}
    local acc, slowAcc, adaptAcc = 0, 0, 0
    local lastDetail = 0
    local KEEPCLS = {
        SpecialMesh = true, BlockMesh = true, CylinderMesh = true, FileMesh = true,
        SurfaceAppearance = true, Decal = true, Texture = true,
    }
    local overlap = OverlapParams.new()
    overlap.FilterType = Enum.RaycastFilterType.Exclude
    local rayP = RaycastParams.new()
    rayP.FilterType = Enum.RaycastFilterType.Exclude

    -- Mirror a CFrame over the plane y = h. Parts are symmetric boxes, so we flip local X to keep a valid rotation.
    local function mirrorCF(cf, h)
        local x, y, z, r00, r01, r02, r10, r11, r12, r20, r21, r22 = cf:GetComponents()
        return CFrame.new(x, 2 * h - y - 0.03, z, -r00, r01, r02, r10, -r11, -r12, -r20, r21, r22)
    end

    local function ensureFolder()
        if folder and folder.Parent then return folder end
        folder = Instance.new("Folder")
        folder.Name = "RMEX_MIRROR"
        folder.Parent = workspace
        return folder
    end

    local function makeProxy(p)
        local c
        pcall(function() c = p:Clone() end)
        if not c or not c:IsA("BasePart") then
            if c then c:Destroy() end
            c = Instance.new("Part")
            c.Size = p.Size
            c.Color = p.Color
            c.Material = p.Material
            c.Transparency = p.Transparency
            if p:IsA("Part") then c.Shape = p.Shape end
        else
            for _, d in ipairs(c:GetDescendants()) do
                if not KEEPCLS[d.ClassName] then d:Destroy() end
            end
        end
        c.Anchored = true
        c.CanCollide = false
        c.CanTouch = false
        c.CanQuery = false
        c.CastShadow = false
        c.Locked = true
        c.Reflectance = 0
        -- the mirrored underside is lit from below, so brighten it a little
        c.Color = c.Color:Lerp(Color3.new(1, 1, 1), 0.18)
        return c
    end

    local function hyOf(cf, size)
        local _, _, _, _, _, _, r10, r11, r12 = cf:GetComponents()
        return (math.abs(r10) * size.X + math.abs(r11) * size.Y + math.abs(r12) * size.Z) / 2
    end

    local function floorize(p)
        if floors[p] then return end
        floors[p] = {T = p.Transparency, R = p.Reflectance, M = p.Material}
        table.insert(floorList, p)
    end

    local function floorLook()
        local T = math.clamp(SH.Clear / 100, 0.25, 0.92)
        local R = math.clamp(SH.Mirror / 100 * 0.45, 0.05, 0.45)
        for _, p in ipairs(floorList) do
            if p.Parent then
                p.Transparency = T
                p.Reflectance = R
                if floors[p] and floors[p].M ~= Enum.Material.Neon then p.Material = Enum.Material.SmoothPlastic end
            end
        end
    end

    local function restoreFloors()
        for _, p in ipairs(floorList) do
            local o = floors[p]
            if o and p.Parent then
                p.Transparency, p.Reflectance, p.Material = o.T, o.R, o.M
            end
            floors[p] = nil
        end
        floorList = {}
    end

    local function clearAll()
        for _, pr in pairs(proxies) do
            if pr.clone then pr.clone:Destroy() end
        end
        proxies = {}
        restoreFloors()
        plane = nil
        if folder then
            folder:Destroy()
            folder = nil
        end
    end
    RX.sh.ultraClear = clearAll

    local function findPlane(root, char)
        rayP.FilterDescendantsInstances = {char, folder}
        local hit = workspace:Raycast(root.Position, Vector3.new(0, -14, 0), rayP)
        if hit and hit.Instance:IsA("BasePart") and not hit.Instance:IsA("Terrain") and hit.Normal.Y > 0.95 then
            return hit.Position.Y, hit.Instance
        end
        return nil, nil
    end

    -- Collect nearby parts: floors turn glossy, everything above the plane gets a mirrored twin.
    local function scan(root, char)
        local h = plane
        overlap.FilterDescendantsInstances = {char, folder}
        local parts = workspace:GetPartBoundsInRadius(root.Position, SH.Range, overlap)
        local cand = {}
        for _, p in ipairs(parts) do
            if p.Transparency < 0.95 and not p:IsA("Terrain") then
                local cf, sz = p.CFrame, p.Size
                local hy = hyOf(cf, sz)
                local y = cf.Position.Y
                local top, bot = y + hy, y - hy
                local model = p:FindFirstAncestorOfClass("Model")
                local isChar = model and model:FindFirstChildOfClass("Humanoid") ~= nil
                if not isChar then
                    local big = math.max(sz.X, sz.Z) >= 6 and math.min(sz.X, sz.Z) >= 4
                    if big and p.Anchored and cf.UpVector.Y > 0.97 and math.abs(top - h) < 0.4 then
                        floorize(p)
                    elseif bot >= h - 0.25 and sz.Magnitude > 1.4 and not p:FindFirstAncestor("RMEX_FX") then
                        table.insert(cand, {p = p, d = (cf.Position - root.Position).Magnitude})
                    end
                end
            end
        end
        table.sort(cand, function(a, b) return a.d < b.d end)
        local keep, count = {}, 0
        for _, c in ipairs(cand) do
            count += 1
            if count > SH.Detail then break end
            keep[c.p] = true
        end
        for p, pr in pairs(proxies) do
            if not keep[p] and not pr.char then
                pr.clone:Destroy()
                proxies[p] = nil
            end
        end
        local made = 0
        for p in pairs(keep) do
            if not proxies[p] and made < 12 then
                made += 1
                local c = makeProxy(p)
                c.CFrame = mirrorCF(p.CFrame, h)
                c.Parent = ensureFolder()
                proxies[p] = {clone = c, static = p.Anchored, last = p.CFrame}
            end
        end
    end

    local function characters(h)
        -- players are moved every frame
        local list, cfs, n = {}, {}, 0
        for _, plr in ipairs(Players:GetPlayers()) do
            local ch = plr.Character
            if ch then
                for _, d in ipairs(ch:GetDescendants()) do
                    if d:IsA("BasePart") and d.Transparency < 0.98 and d.Name ~= "HumanoidRootPart" then
                        local pr = proxies[d]
                        if not pr then
                            local c = makeProxy(d)
                            c.CFrame = mirrorCF(d.CFrame, h)
                            c.Parent = ensureFolder()
                            pr = {clone = c, char = true}
                            proxies[d] = pr
                        end
                        n += 1
                        list[n], cfs[n] = pr.clone, mirrorCF(d.CFrame, h)
                        pr.clone.Transparency = d.Transparency
                    end
                end
            end
        end
        for p, pr in pairs(proxies) do
            if pr.char and not p:IsDescendantOf(workspace) then
                pr.clone:Destroy()
                proxies[p] = nil
            end
        end
        return list, cfs, n
    end

    RunService.RenderStepped:Connect(function(dt)
        local want = SH.On and SH.Mode == "mirror" and SH.Tier == 2
        if not want then
            if plane or folder then clearAll() end
            return
        end
        local char = localPlayer.Character
        local root = char and char:FindFirstChild("HumanoidRootPart")
        if not root then return end
        acc += dt
        if acc > 0.35 or not plane then
            acc = 0
            -- v15: only re-evaluate the floor while standing on it. In the air (jump / fall) we keep the
            -- current reflection, otherwise every jump rebuilt the whole mirrored world and tanked FPS.
            local hum = char:FindFirstChildOfClass("Humanoid")
            local grounded = hum ~= nil and hum.FloorMaterial ~= Enum.Material.Air
            if grounded or not plane then
                local h, hitPart = findPlane(root, char)
                if h and (not plane or math.abs(h - plane) > 0.3) then
                    -- a different floor must be seen twice in a row before we switch (no flicker on stairs)
                    if not plane or SH._pendH and math.abs(SH._pendH - h) < 0.15 then
                        SH._pendN = (SH._pendN or 0) + 1
                    else
                        SH._pendH, SH._pendN = h, 1
                    end
                    if not plane or SH._pendN >= 2 then
                        clearAll()
                        plane = h
                        SH._pendH, SH._pendN, SH._miss = nil, 0, 0
                        if hitPart and hitPart.Anchored then floorize(hitPart) end
                    end
                elseif not h and plane then
                    SH._miss = (SH._miss or 0) + 1
                    if SH._miss >= 6 then
                        clearAll()
                        SH._miss = 0
                    end
                else
                    SH._pendH, SH._pendN, SH._miss = nil, 0, 0
                end
            end
            if not plane then return end
        end
        if not plane then return end
        slowAcc += dt
        if slowAcc > 0.9 then
            slowAcc = 0
            scan(root, char)
            floorLook()
        end
        -- adaptive detail: if the phone struggles, reduce the load
        adaptAcc += dt
        if adaptAcc > 2 then
            adaptAcc = 0
            if RX.boost and RX.boost.fps < 24 and SH.Detail > 140 then
                SH.Detail = math.floor(SH.Detail * 0.8)
            end
        end
        local mp, mc, n = {}, {}, 0
        for p, pr in pairs(proxies) do
            if not pr.char and p.Parent and (not pr.static) then
                n += 1
                mp[n], mc[n] = pr.clone, mirrorCF(p.CFrame, plane)
            end
        end
        local lp, lc, ln = characters(plane)
        for i = 1, ln do
            n += 1
            mp[n], mc[n] = lp[i], lc[i]
        end
        if n > 0 then workspace:BulkMoveTo(mp, mc, Enum.BulkMoveMode.FireCFrameChanged) end
    end)
end

-- ============================================================================
-- FPS BOOSTER (SCREEN tab, first row): particles, shadows, post effects, materials
-- ============================================================================
RX.boost = {On = false, Level = 2, fps = 60, before = nil, after = nil, t0 = 0}
do
    local B = RX.boost
    local Stats = nil
    local saved = setmetatable({}, {__mode = "k"})
    local lightingSaved = nil
    local conn = nil
    local token = 0
    local PARTICLE = {
        ParticleEmitter = true, Trail = true, Beam = true, Smoke = true, Fire = true, Sparkles = true,
    }
    local POST = {
        BloomEffect = true, DepthOfFieldEffect = true, SunRaysEffect = true, BlurEffect = true, ColorCorrectionEffect = true,
    }

    local function ours(inst)
        if inst:FindFirstAncestor("RMEX_FX") or inst:FindFirstAncestor("RMEX_MIRROR") then return true end
        return inst.Name:sub(1, 4) == "RMEX"
    end

    -- Handles one instance. Remembers the original value so turning the booster off restores it.
    local function process(inst, level)
        if ours(inst) then return end
        local cls = inst.ClassName
        local rec = saved[inst]
        if PARTICLE[cls] then
            if not rec then saved[inst] = {En = inst.Enabled} end
            inst.Enabled = false
        elseif cls == "Explosion" then
            if not rec then saved[inst] = {Vis = inst.Visible} end
            inst.Visible = false
        elseif level >= 2 then
            if POST[cls] then
                if not rec then saved[inst] = {En = inst.Enabled} end
                inst.Enabled = false
            elseif cls == "PointLight" or cls == "SpotLight" or cls == "SurfaceLight" then
                if not rec then saved[inst] = {Sh = inst.Shadows} end
                inst.Shadows = false
            elseif inst:IsA("BasePart") then
                if not rec then
                    rec = {Cast = inst.CastShadow}
                    saved[inst] = rec
                end
                inst.CastShadow = false
                local model = inst:FindFirstAncestorOfClass("Model")
                local isChar = model ~= nil and model:FindFirstChildOfClass("Humanoid") ~= nil
                if level >= 3 and not isChar then
                    if rec.Mat == nil and inst.Material ~= Enum.Material.Neon and inst.Material ~= Enum.Material.Glass
                        and inst.Material ~= Enum.Material.ForceField then
                        rec.Mat, rec.Refl = inst.Material, inst.Reflectance
                        inst.Material = Enum.Material.Plastic
                        inst.Reflectance = 0
                    end
                    if inst:IsA("MeshPart") then
                        rec.Fid = rec.Fid or inst.RenderFidelity
                        inst.RenderFidelity = Enum.RenderFidelity.Performance
                    end
                end
            end
        end
    end

    local function applyGlobal(level)
        if not lightingSaved then
            lightingSaved = {
                Shadows = Lighting.GlobalShadows,
                Quality = nil,
            }
            local terrain = workspace:FindFirstChildOfClass("Terrain")
            if terrain then
                lightingSaved.Terrain = terrain
                lightingSaved.Deco = terrain.Decoration
                lightingSaved.WaveSize, lightingSaved.WaveSpeed = terrain.WaterWaveSize, terrain.WaterWaveSpeed
                lightingSaved.WaterRefl = terrain.WaterReflectance
            end
            pcall(function()
                local rs = getfenv(0).settings().Rendering
                lightingSaved.rs = rs
                lightingSaved.Quality = rs.QualityLevel
            end)
        end
        Lighting.GlobalShadows = false
        local terrain = lightingSaved.Terrain
        if terrain and level >= 2 then
            pcall(function()
                terrain.Decoration = false
                terrain.WaterWaveSize = 0
                terrain.WaterWaveSpeed = 0
                terrain.WaterReflectance = 0
            end)
        end
        if level >= 3 and lightingSaved.rs then
            pcall(function() lightingSaved.rs.QualityLevel = Enum.QualityLevel.Level01 end)
        end
    end

    local function restore()
        for inst, rec in pairs(saved) do
            if inst.Parent then
                pcall(function()
                    if rec.En ~= nil then inst.Enabled = rec.En end
                    if rec.Vis ~= nil then inst.Visible = rec.Vis end
                    if rec.Sh ~= nil then inst.Shadows = rec.Sh end
                    if rec.Cast ~= nil then inst.CastShadow = rec.Cast end
                    if rec.Mat ~= nil then
                        inst.Material = rec.Mat
                        inst.Reflectance = rec.Refl
                    end
                    if rec.Fid ~= nil then inst.RenderFidelity = rec.Fid end
                end)
            end
            saved[inst] = nil
        end
        local s = lightingSaved
        if s then
            Lighting.GlobalShadows = s.Shadows
            if s.Terrain then
                pcall(function()
                    s.Terrain.Decoration = s.Deco
                    s.Terrain.WaterWaveSize, s.Terrain.WaterWaveSpeed = s.WaveSize, s.WaveSpeed
                    s.Terrain.WaterReflectance = s.WaterRefl
                end)
            end
            if s.rs and s.Quality then pcall(function() s.rs.QualityLevel = s.Quality end) end
            lightingSaved = nil
        end
    end

    local function run(level)
        token += 1
        local my = token
        if conn then conn:Disconnect() end
        pcall(applyGlobal, level)
        task.defer(function()
            local n = 0
            for _, inst in ipairs(game:GetDescendants()) do
                if my ~= token then return end
                process(inst, level)
                n += 1
                if n % 120 == 0 then RunService.Heartbeat:Wait() end
            end
        end)
        conn = game.DescendantAdded:Connect(function(inst)
            task.defer(process, inst, B.Level)
        end)
    end

    B.set = function(on)
        B.On = on
        token += 1
        if on then
            B.before = B.fps
            B.after = nil
            B.t0 = os.clock()
            local ok, err = pcall(run, B.Level)
            if not ok then warn("[RMEX] booster error: " .. tostring(err)) end
        else
            if conn then conn:Disconnect() conn = nil end
            restore()
            B.after = nil
        end
    end
    B.level = function(l)
        B.Level = l
        if B.On then
            restore()
            run(l)
        end
    end

    local acc = 0
    RunService.Heartbeat:Connect(function(dt)
        acc += (1 / math.max(dt, 1 / 240) - acc) * math.min(1, dt * 2)
        B.fps = acc
        if B.On and not B.after and os.clock() - B.t0 > 3.5 then B.after = B.fps end
    end)
end

-- ============================================================================
-- SCREEN PAGE
-- ============================================================================

-- FPS booster (first thing on the SCREEN tab) --------------------------------
makeToggleRow(screenPage, {
    key = "boost", desc = "boost_d",
    get = function() return RX.boost.On end,
    set = function(v) RX.boost.set(v) end,
})
makeSegmented(screenPage, "boost_level",
    {{key = "bl_1", value = 1}, {key = "bl_2", value = 2}, {key = "bl_3", value = 3}},
    function() return RX.boost.Level end,
    function(v) RX.boost.level(v) end)
do
    local card = makeCard(screenPage, 24)
    local lbl = makeLabel(card, {pos = UDim2.fromOffset(10, 0), size = UDim2.new(1, -20, 1, 0), textSize = 10,
        font = Enum.Font.GothamBold, role = "muted", text = "FPS"})
    task.spawn(function()
        while lbl.Parent do
            local B = RX.boost
            local name = STRINGS[lang].boost_fps
            if B.On and B.after and B.before then
                lbl.Text = string.format("%s: %d -> %d  (%+d)", name, B.before, B.after, B.after - B.before)
            else
                lbl.Text = string.format("%s: %d", name, B.fps)
            end
            task.wait(0.5)
        end
    end)
end

-- Shaders: one switch + mode (day / sunset / night / mirror / neon) ----------
makeToggleRow(screenPage, {
    key = "shaders", desc = "shaders_d",
    get = function() return RX.sh.On end,
    set = function(v) RX.sh.On = v end,
})
makeSegmented(screenPage, "shader_mode",
    {
        {key = "sh_day", value = "day"},
        {key = "sh_sunset", value = "sunset"},
        {key = "sh_night", value = "night"},
        {key = "sh_mirror", value = "mirror"},
        {key = "sh_neon", value = "neon"},
    },
    function() return RX.sh.Mode end,
    function(v) RX.sh.Mode = v end)
makeSlider(screenPage, {
    key = "shader_strength", min = 10, max = 100,
    get = function() return RX.sh.Strength end,
    set = function(v) RX.sh.Strength = math.floor(v + 0.5) end,
    format = function(v) return math.floor(v + 0.5) .. "%" end,
})
makeSlider(screenPage, {
    key = "mirror_level", min = 20, max = 100,
    get = function() return RX.sh.Mirror end,
    set = function(v) RX.sh.Mirror = math.floor(v + 0.5) end,
    format = function(v) return math.floor(v + 0.5) .. "%" end,
    onChange = function() RX.sh.dirty = true end,
})
makeSegmented(screenPage, "mirror_tier",
    {{key = "mt_std", value = 1}, {key = "mt_ultra", value = 2}},
    function() return RX.sh.Tier end,
    function(v) RX.sh.Tier = v end)
makeSlider(screenPage, {
    key = "ultra_range", min = 60, max = 250,
    get = function() return RX.sh.Range end,
    set = function(v) RX.sh.Range = math.floor(v + 0.5) end,
    format = function(v) return math.floor(v + 0.5) .. " " .. STRINGS[lang].studs end,
})
makeSlider(screenPage, {
    key = "ultra_detail", min = 100, max = 800,
    get = function() return RX.sh.Detail end,
    set = function(v) RX.sh.Detail = math.floor(v + 0.5) end,
    format = function(v) return tostring(math.floor(v + 0.5)) end,
})
makeSlider(screenPage, {
    key = "ultra_clear", min = 25, max = 92,
    get = function() return RX.sh.Clear end,
    set = function(v) RX.sh.Clear = math.floor(v + 0.5) end,
    format = function(v) return math.floor(v + 0.5) .. "%" end,
})

-- Roblox clamps Camera.FieldOfView to 1..120, so 120 is the real maximum.
fovRender = makeSlider(screenPage, {
    key = "fov", min = 30, max = 120,
    get = function() return esp.FOV end,
    set = function(v) esp.FOV = math.floor(v + 0.5) end,
    format = function(v) return tostring(math.floor(v + 0.5)) end,
})

local screenToggles = {
    {key = "bloom", desc = "bloom_d", field = "Bloom"},
    {key = "vignette", desc = "vignette_d", field = "Vignette"},
    {key = "shake", desc = "shake_d", field = "Shake"},
}
for _, item in ipairs(screenToggles) do
    makeToggleRow(screenPage, {
        key = item.key,
        desc = item.desc,
        get = function() return screenFX[item.field] end,
        set = function(v) screenFX[item.field] = v end,
        onChange = applyScreenFX,
    })
end

makeToggleRow(screenPage, {
    key = "sway", desc = "sway_d",
    get = function() return camFX.Sway end,
    set = function(v) camFX.Sway = v end,
})
makeSlider(screenPage, {
    key = "sway_strength", min = 5, max = 100,
    get = function() return camFX.SwayStrength end,
    set = function(v) camFX.SwayStrength = math.floor(v + 0.5) end,
    format = function(v) return math.floor(v + 0.5) .. "%" end,
})
makeToggleRow(screenPage, {
    key = "stable", desc = "stable_d",
    get = function() return camFX.Stable end,
    set = function(v) camFX.Stable = v end,
})
camFX.distRender = makeSlider(screenPage, {
    key = "cam_dist", min = 3, max = 60,
    get = function() return camFX.Distance end,
    set = function(v) camFX.Distance = math.floor(v + 0.5) end,
    format = function(v) return math.floor(v + 0.5) .. " " .. STRINGS[lang].studs end,
})
makeToggleRow(screenPage, {
    key = "free", desc = "free_d",
    get = function() return camFX.Free end,
    set = function(v) camFX.Free = v end,
})
camFX.speedRender = makeSlider(screenPage, {
    key = "free_speed", min = 5, max = 200,
    get = function() return camFX.FreeSpeed end,
    set = function(v) camFX.FreeSpeed = math.floor(v + 0.5) end,
    format = function(v) return math.floor(v + 0.5) .. "" end,
})

-- ============================================================================
-- CROSSHAIR / FULLBRIGHT / UNIVERSAL UI
-- ============================================================================
do
    local ch = Instance.new("Frame")
    ch.Name = "RMEXCrosshair"
    ch.AnchorPoint = Vector2.new(0.5, 0.5)
    ch.Position = UDim2.fromScale(0.5, 0.5)
    ch.Size = UDim2.fromOffset(0, 0)
    ch.BackgroundTransparency = 1
    ch.Active = false
    ch.Visible = false
    ch.Parent = gui
    local function mk(name)
        local f = Instance.new("Frame")
        f.Name = name
        f.AnchorPoint = Vector2.new(0.5, 0.5)
        f.BorderSizePixel = 0
        f.Parent = ch
        local s = Instance.new("UIStroke")
        s.Thickness = 1
        s.Color = Color3.new(0, 0, 0)
        s.Transparency = 0.35
        s.Parent = f
        return f
    end
    local bars = {mk("L"), mk("R"), mk("U"), mk("D")}
    local dot = mk("Dot")
    corner(dot, 999)
    local ring = Instance.new("Frame")
    ring.AnchorPoint = Vector2.new(0.5, 0.5)
    ring.BackgroundTransparency = 1
    ring.BorderSizePixel = 0
    ring.Parent = ch
    corner(ring, 999)
    local rs = Instance.new("UIStroke")
    rs.Parent = ring

    RX.applyCross = function()
        local c = RX.cross
        ch.Visible = screenFX.Cross
        local s, th, gap = c.Size, c.Thick, 4
        local isCross = c.Style == 1
        for _, b in ipairs(bars) do
            b.Visible = isCross
            b.BackgroundColor3 = c.Color
        end
        if isCross then
            local off = gap + s / 2
            bars[1].Size = UDim2.fromOffset(s, th); bars[1].Position = UDim2.fromOffset(-off, 0)
            bars[2].Size = UDim2.fromOffset(s, th); bars[2].Position = UDim2.fromOffset(off, 0)
            bars[3].Size = UDim2.fromOffset(th, s); bars[3].Position = UDim2.fromOffset(0, -off)
            bars[4].Size = UDim2.fromOffset(th, s); bars[4].Position = UDim2.fromOffset(0, off)
        end
        dot.Visible = c.Style ~= 1
        local ds = c.Style == 2 and math.max(th * 2, s / 3) or th * 1.6
        dot.Size = UDim2.fromOffset(ds, ds)
        dot.BackgroundColor3 = c.Color
        ring.Visible = c.Style == 3
        ring.Size = UDim2.fromOffset(s * 2, s * 2)
        rs.Thickness = th
        rs.Color = c.Color
    end

    makeToggleRow(screenPage, {
        key = "crosshair", desc = "crosshair_d",
        get = function() return screenFX.Cross end,
        set = function(v) screenFX.Cross = v end,
        onChange = RX.applyCross,
    })
    makeSegmented(screenPage, "cross_style",
        {{key = "cs_cross", value = 1}, {key = "cs_dot", value = 2}, {key = "cs_circle", value = 3}},
        function() return RX.cross.Style end,
        function(v) RX.cross.Style = v; RX.applyCross() end)
    makeSlider(screenPage, {
        key = "cross_size", min = 4, max = 40,
        get = function() return RX.cross.Size end,
        set = function(v) RX.cross.Size = math.floor(v + 0.5) end,
        format = function(v) return tostring(math.floor(v + 0.5)) end,
        onChange = RX.applyCross,
    })
    makeSlider(screenPage, {
        key = "cross_thick", min = 1, max = 6,
        get = function() return RX.cross.Thick end,
        set = function(v) RX.cross.Thick = math.floor(v + 0.5) end,
        format = function(v) return tostring(math.floor(v + 0.5)) end,
        onChange = RX.applyCross,
    })
    makeSwatchRow(screenPage, "cross_color", ACCENTS,
        function() return RX.cross.Color end,
        function(c) RX.cross.Color = c; RX.applyCross() end)
    RX.applyCross()

    makeToggleRow(screenPage, {
        key = "fullbright", desc = "fullbright_d",
        get = function() return screenFX.Bright end,
        set = function(v) screenFX.Bright = v end,
    })
    makeSlider(screenPage, {
        key = "bright_level", min = 10, max = 100,
        get = function() return RX.bright.Level end,
        set = function(v) RX.bright.Level = math.floor(v + 0.5) end,
        format = function(v) return math.floor(v + 0.5) .. "%" end,
    })

    -- Universal page
    for _, d in ipairs({
        {"uni_speed", "uni_speed_d", "Speed", "walkspeed", "SpeedV", 0, 250},
        {"uni_jump", "uni_jump_d", "Jump", "jumppower", "JumpV", 0, 300},
        {"uni_grav", "uni_grav_d", "Grav", "gravity_v", "GravV", 0, 400},
    }) do
        makeToggleRow(universalPage, {
            key = d[1], desc = d[2],
            get = function() return RX.uni[d[3]] end,
            set = function(v) RX.uni[d[3]] = v end,
        })
        makeSlider(universalPage, {
            key = d[4], min = d[6], max = d[7],
            get = function() return RX.uni[d[5]] end,
            set = function(v) RX.uni[d[5]] = math.floor(v + 0.5) end,
            format = function(v) return tostring(math.floor(v + 0.5)) end,
        })
    end
end

makeToggleRow(screenPage, {
    key = "motionblur", desc = "motionblur_d",
    get = function() return screenFX.Blur end,
    set = function(v) screenFX.Blur = v end,
})
makeSlider(screenPage, {
    key = "blur_strength", min = 10, max = 100,
    get = function() return RX.blurK end,
    set = function(v) RX.blurK = math.floor(v + 0.5) end,
    format = function(v) return math.floor(v + 0.5) .. "%" end,
})
makeToggleRow(settingsPage, {
    key = "sounds", desc = "sounds_d",
    get = function() return RX.sound end,
    set = function(v) RX.sound = v end,
})

-- ============================================================================
-- ESP EXTRAS / AIMBOT / MUSIC / TINT / STRETCH
-- ============================================================================
do
    -- ESP extras: head dot, look line, off-screen arrows, radar
    local layer = Instance.new("Frame")
    layer.Name = "RMEXEspExtra"
    layer.BackgroundTransparency = 1
    layer.Size = UDim2.fromScale(1, 1)
    layer.Active = false
    layer.Parent = gui
    local radar = Instance.new("Frame")
    radar.AnchorPoint = Vector2.new(1, 0)
    radar.Position = UDim2.new(1, -14, 0, 70)
    radar.Size = UDim2.fromOffset(120, 120)
    radar.BackgroundColor3 = Color3.fromRGB(10, 10, 16)
    radar.BackgroundTransparency = 0.35
    radar.BorderSizePixel = 0
    radar.Visible = false
    radar.Parent = layer
    corner(radar, 999)
    local rst = Instance.new("UIStroke")
    rst.Thickness = 1.5
    rst.Transparency = 0.3
    rst.Parent = radar
    local me = Instance.new("Frame")
    me.AnchorPoint = Vector2.new(0.5, 0.5)
    me.Position = UDim2.fromScale(0.5, 0.5)
    me.Size = UDim2.fromOffset(6, 6)
    me.BorderSizePixel = 0
    me.Parent = radar
    corner(me, 999)

    local objs = {}
    local function mkFrame(w, h, parent, round)
        local f = Instance.new("Frame")
        f.AnchorPoint = Vector2.new(0.5, 0.5)
        f.Size = UDim2.fromOffset(w, h)
        f.BorderSizePixel = 0
        f.Visible = false
        f.Parent = parent
        if round then corner(f, 999) end
        return f
    end
    local function getObj(player)
        local o = objs[player]
        if not o then
            o = {dot = mkFrame(7, 7, layer, true), rd = mkFrame(5, 5, radar, true),
                look = mkFrame(10, 2, layer), arrow = mkFrame(18, 5, layer)}
            objs[player] = o
        end
        return o
    end

    RX.espExtras = function(cam, vp)
        radar.Visible = settings.Radar
        me.BackgroundColor3 = P.text
        for player, o in pairs(objs) do
            if not tracked[player] then
                for _, v in pairs(o) do v:Destroy() end
                objs[player] = nil
            end
        end
        local sx, sy = esp.StretchX / 100, esp.StretchY / 100
        local cx, cy = vp.X * 0.5, vp.Y * 0.5
        local myChar = localPlayer.Character
        local myRoot = myChar and myChar:FindFirstChild("HumanoidRootPart")
        local function proj(pos)
            local pt = cam:WorldToViewportPoint(pos)
            local x, y = pt.X, pt.Y
            if pt.Z <= 0 then x, y = vp.X - x, vp.Y - y end
            return (x - cx) * sx + cx, (y - cy) * sy + cy, pt.Z > 0
        end
        for player, data in pairs(tracked) do
            local o = getObj(player)
            local alive = data.humanoid.Health > 0
            local col = P.accent
            -- head dot
            local hx, hy, hok = proj(data.head.Position)
            o.dot.Visible = settings.HeadDot and hok and alive
            if o.dot.Visible then
                o.dot.Position = UDim2.fromOffset(hx, hy)
                o.dot.BackgroundColor3 = col
            end
            -- look direction
            local lx, ly, lok = proj(data.head.Position + data.head.CFrame.LookVector * 6)
            local show = settings.LookLine and hok and lok and alive
            o.look.Visible = show
            if show then
                local d = Vector2.new(lx - hx, ly - hy)
                o.look.Position = UDim2.fromOffset((hx + lx) / 2, (hy + ly) / 2)
                o.look.Size = UDim2.fromOffset(math.max(d.Magnitude, 1), 2)
                o.look.Rotation = math.deg(math.atan2(d.Y, d.X))
                o.look.BackgroundColor3 = col
            end
            -- off-screen arrow
            local rx2, ry2, rok = proj(data.root.Position)
            local off = not rok or rx2 < 0 or rx2 > vp.X or ry2 < 0 or ry2 > vp.Y
            o.arrow.Visible = settings.Arrows and off and alive
            if o.arrow.Visible then
                local dir = Vector2.new(rx2 - cx, ry2 - cy)
                dir = dir.Magnitude < 1 and Vector2.new(0, -1) or dir.Unit
                local rad = math.min(vp.X, vp.Y) * 0.5 - 40
                o.arrow.Position = UDim2.fromOffset(cx + dir.X * rad, cy + dir.Y * rad)
                o.arrow.Rotation = math.deg(math.atan2(dir.Y, dir.X))
                o.arrow.BackgroundColor3 = col
            end
            -- radar
            o.rd.Visible = settings.Radar and myRoot ~= nil and alive
            if o.rd.Visible then
                local rel = cam.CFrame:VectorToObjectSpace(data.root.Position - myRoot.Position)
                local v = Vector2.new(rel.X, rel.Z) * 0.4
                if v.Magnitude > 56 then v = v.Unit * 56 end
                o.rd.Position = UDim2.new(0.5, v.X, 0.5, v.Y)
                o.rd.BackgroundColor3 = Color3.fromRGB(255, 80, 80)
            end
        end
    end

    -- Tint / stretch UI (screen page)
    makeToggleRow(screenPage, {
        key = "tint", desc = "tint_d",
        get = function() return screenFX.Tint end,
        set = function(v) screenFX.Tint = v end,
    })
    makeSwatchRow(screenPage, "tint_color", {
        Color3.fromRGB(190, 70, 255), Color3.fromRGB(255, 80, 190), Color3.fromRGB(255, 70, 70), Color3.fromRGB(255, 170, 60),
        Color3.fromRGB(80, 255, 150), Color3.fromRGB(70, 200, 255), Color3.fromRGB(90, 110, 255), Color3.fromRGB(255, 255, 255),
    }, function() return RX.tint.Color end, function(c) RX.tint.Color = c end)
    makeSlider(screenPage, {
        key = "tint_strength", min = 5, max = 100,
        get = function() return RX.tint.Strength end,
        set = function(v) RX.tint.Strength = math.floor(v + 0.5) end,
        format = function(v) return math.floor(v + 0.5) .. "%" end,
    })
    makeToggleRow(screenPage, {
        key = "mono",
        get = function() return RX.tint.Mono end,
        set = function(v) RX.tint.Mono = v end,
    })
    makeToggleRow(screenPage, {
        key = "stretch", desc = "stretch_d",
        get = function() return screenFX.Stretch end,
        set = function(v) screenFX.Stretch = v end,
    })
    makeSlider(screenPage, {
        key = "stretch_k", min = 30, max = 100,
        get = function() return RX.stretchK end,
        set = function(v) RX.stretchK = math.floor(v + 0.5) end,
        format = function(v) return math.floor(v + 0.5) .. "%" end,
    })
    RunService:BindToRenderStep("RMEXStretch", Enum.RenderPriority.Camera.Value + 5, function()
        if not screenFX.Stretch then return end
        local cam = workspace.CurrentCamera
        if cam then cam.CFrame = cam.CFrame * CFrame.new(0, 0, 0, 1, 0, 0, 0, RX.stretchK / 100, 0, 0, 0, 1) end
    end)

    -- Aimbot
    local A = RX.aim
    local function aimToggle(key, field, onChange)
        makeToggleRow(aimbotPage, {
            key = "aim_" .. key, desc = "aim_" .. key .. "_d",
            get = function() return A[field] end,
            set = function(v) A[field] = v end,
            onChange = onChange,
        })
    end
    local function aimSlider(key, field, lo, hi, fmt)
        makeSlider(aimbotPage, {
            key = key, min = lo, max = hi,
            get = function() return A[field] end,
            set = function(v) A[field] = math.floor(v + 0.5) end,
            format = function(v) return math.floor(v + 0.5) .. (fmt or "") end,
        })
    end
    aimToggle("on", "On")
    aimToggle("hold", "Hold")
    aimSlider("aim_fov", "FOV", 30, 500, "px")
    aimSlider("aim_smooth", "Smooth", 0, 95, "%")
    aimSlider("aim_pred", "Pred", 0, 100, "%")
    aimSlider("aim_dist", "Dist", 50, 2000, "")
    makeSegmented(aimbotPage, "aim_part", {{key = "ap_head", value = 1}, {key = "ap_body", value = 2}},
        function() return A.Part end, function(v) A.Part = v end)
    aimToggle("team", "Team")
    aimToggle("wall", "Wall")
    aimToggle("sticky", "Sticky")
    aimToggle("circle", "Circle")

    local circ = Instance.new("Frame")
    circ.Name = "RMEXAimFOV"
    circ.AnchorPoint = Vector2.new(0.5, 0.5)
    circ.Position = UDim2.fromScale(0.5, 0.5)
    circ.BackgroundTransparency = 1
    circ.BorderSizePixel = 0
    circ.Active = false
    circ.Visible = false
    circ.Parent = gui
    corner(circ, 999)
    local cst = Instance.new("UIStroke")
    cst.Thickness = 1.5
    cst.Transparency = 0.35
    cst.Parent = circ

    local rayParams = RaycastParams.new()
    rayParams.FilterType = Enum.RaycastFilterType.Exclude
    local aimTarget
    local function partOf(ch)
        if A.Part == 1 then return ch:FindFirstChild("Head") end
        return ch:FindFirstChild("UpperTorso") or ch:FindFirstChild("Torso") or ch:FindFirstChild("HumanoidRootPart")
    end
    local function candidate(player, cam, center)
        local ch = player.Character
        local hum = ch and ch:FindFirstChildOfClass("Humanoid")
        local part = ch and partOf(ch)
        if not hum or not part or hum.Health <= 0 then return nil end
        if A.Team and player.Team ~= nil and player.Team == localPlayer.Team then return nil end
        if (part.Position - cam.CFrame.Position).Magnitude > A.Dist then return nil end
        local v, onScreen = cam:WorldToViewportPoint(part.Position)
        if not onScreen then return nil end
        local d = (Vector2.new(v.X, v.Y) - center).Magnitude
        if d > A.FOV then return nil end
        if A.Wall then
            rayParams.FilterDescendantsInstances = {localPlayer.Character}
            local r = workspace:Raycast(cam.CFrame.Position, part.Position - cam.CFrame.Position, rayParams)
            if r and not r.Instance:IsDescendantOf(ch) then return nil end
        end
        return {player = player, part = part, d = d}
    end

    -- Floating AIM button: visible while the aimbot toggle is on. Tap = start/stop aiming, drag = move it.
    A.Live = false
    local aimBtn = Instance.new("TextButton")
    aimBtn.Name = "RMEXAimBtn"
    aimBtn.AnchorPoint = Vector2.new(0.5, 0.5)
    aimBtn.Position = UDim2.fromScale(0.88, 0.5)
    aimBtn.Size = UDim2.fromOffset(64, 64)
    aimBtn.AutoButtonColor = false
    aimBtn.Text = "AIM"
    aimBtn.Font = Enum.Font.GothamBold
    aimBtn.TextSize = 13
    aimBtn.BorderSizePixel = 0
    aimBtn.BackgroundColor3 = Color3.fromRGB(18, 18, 24)
    aimBtn.BackgroundTransparency = 0.55
    aimBtn.ZIndex = 60
    aimBtn.Visible = false
    aimBtn.Parent = gui
    corner(aimBtn, 999)
    local abStroke = Instance.new("UIStroke")
    abStroke.Thickness = 2
    abStroke.Parent = aimBtn
    local abDrag, abMoved, abStart, abPos, abInput = false, false, nil, nil, nil
    aimBtn.InputBegan:Connect(function(i)
        if i.UserInputType == Enum.UserInputType.MouseButton1 or i.UserInputType == Enum.UserInputType.Touch then
            abDrag, abMoved, abStart, abPos, abInput = true, false, i.Position, aimBtn.Position, i
        end
    end)
    UserInputService.InputChanged:Connect(function(i)
        if abDrag and (i == abInput or i.UserInputType == Enum.UserInputType.MouseMovement or i.UserInputType == Enum.UserInputType.Touch) then
            local d = i.Position - abStart
            if d.Magnitude > 8 then abMoved = true end
            if abMoved then
                aimBtn.Position = UDim2.new(abPos.X.Scale, abPos.X.Offset + d.X, abPos.Y.Scale, abPos.Y.Offset + d.Y)
            end
        end
    end)
    UserInputService.InputEnded:Connect(function(i)
        if abDrag and (i == abInput or i.UserInputType == Enum.UserInputType.MouseButton1 or i.UserInputType == Enum.UserInputType.Touch) then
            abDrag = false
            if not abMoved then A.Live = not A.Live end
        end
    end)

    RunService:BindToRenderStep("RMEXAim", Enum.RenderPriority.Camera.Value + 10, function(dt)
        local cam = workspace.CurrentCamera
        circ.Visible = A.On and A.Circle
        circ.Size = UDim2.fromOffset(A.FOV * 2, A.FOV * 2)
        cst.Color = P.accent
        aimBtn.Visible = A.On
        if not A.On then A.Live = false end
        aimBtn.Text = "AIM\n" .. (A.Live and "ON" or "OFF")
        aimBtn.TextColor3 = A.Live and P.accent or Color3.fromRGB(205, 205, 215)
        abStroke.Color = A.Live and P.accent or Color3.fromRGB(120, 120, 135)
        aimBtn.BackgroundTransparency = A.Live and 0.35 or 0.55
        if not A.On or not cam then aimTarget = nil return end
        if not (A.Live or (A.Hold and UserInputService:IsMouseButtonPressed(Enum.UserInputType.MouseButton2))) then
            aimTarget = nil
            return
        end
        local vp = cam.ViewportSize
        local center = Vector2.new(vp.X * 0.5, vp.Y * 0.5)
        local cur
        if A.Sticky and aimTarget then cur = candidate(aimTarget.player, cam, center) end
        if not cur then
            for _, pl in ipairs(Players:GetPlayers()) do
                if pl ~= localPlayer then
                    local c = candidate(pl, cam, center)
                    if c and (not cur or c.d < cur.d) then cur = c end
                end
            end
        end
        aimTarget = cur
        if not cur then return end
        local pos = cur.part.Position + cur.part.AssemblyLinearVelocity * (A.Pred / 100) * 0.3
        local look = CFrame.lookAt(cam.CFrame.Position, pos)
        local alpha = A.Smooth <= 0 and 1 or math.clamp(1 - (A.Smooth / 100) ^ (dt * 60), 0.02, 1)
        cam.CFrame = cam.CFrame:Lerp(look, alpha)
    end)

    -- Music
    local M = RX.music
    local SoundService = game:GetService("SoundService")
    local function makeBtnRow(parent, specs)
        local card = makeCard(parent, 40)
        local n = #specs
        for i, sp in ipairs(specs) do
            local b = Instance.new("TextButton")
            b.Position = UDim2.new((i - 1) / n, 6, 0, 7)
            b.Size = UDim2.new(1 / n, -8, 0, 26)
            b.Text = ""
            b.AutoButtonColor = false
            b.BorderSizePixel = 0
            b.Parent = card
            corner(b, 7)
            local lbl = makeLabel(b, {
                key = sp[1], size = UDim2.fromScale(1, 1), font = Enum.Font.GothamBold,
                textSize = 10, align = Enum.TextXAlignment.Center, role = false, zindex = 3,
            })
            addPress(b, 0.95)
            b.Activated:Connect(sp[2])
            bindTheme(function(p, instant)
                setOrTween(b, {BackgroundColor3 = p.bg}, instant)
                setOrTween(lbl, {TextColor3 = p.accent}, instant)
            end)
        end
    end

    local idCard = makeCard(musicPage, 62)
    makeLabel(idCard, {key = "mus_id", pos = UDim2.fromOffset(10, 6), size = UDim2.new(1, -20, 0, 14), textSize = 10, role = "muted"})
    local box = Instance.new("TextBox")
    box.Position = UDim2.fromOffset(8, 26)
    box.Size = UDim2.new(1, -16, 0, 28)
    box.Text = ""
    box.PlaceholderText = "1843463175"
    box.PlaceholderColor3 = Color3.fromRGB(130, 130, 140)
    box.ClearTextOnFocus = false
    box.Font = Enum.Font.GothamMedium
    box.TextSize = 12
    box.BorderSizePixel = 0
    box.ZIndex = 3
    box.Parent = idCard
    corner(box, 7)
    bindTheme(function(p, instant)
        setOrTween(box, {BackgroundColor3 = p.bg, TextColor3 = p.text}, instant)
    end)

    local stCard = makeCard(musicPage, 30)
    local status = Instance.new("TextLabel")
    status.BackgroundTransparency = 1
    status.Position = UDim2.fromOffset(10, 0)
    status.Size = UDim2.new(1, -20, 1, 0)
    status.Font = Enum.Font.GothamBold
    status.TextSize = 10
    status.TextXAlignment = Enum.TextXAlignment.Left
    status.Text = "STOPPED"
    status.ZIndex = 3
    status.Parent = stCard
    bindTheme(function(p, instant) setOrTween(status, {TextColor3 = p.accent}, instant) end)

    local function stopMusic()
        if RX.mus then RX.mus:Destroy() RX.mus = nil end
    end
    local function playMusic()
        local id = box.Text:match("%d+")
        if not id then status.Text = "ENTER ID" return end
        local cur = RX.mus
        if cur and cur.SoundId == "rbxassetid://" .. id and not cur.IsPlaying then
            cur:Resume()
            status.Text = "PLAYING " .. id
            return
        end
        stopMusic()
        local s = Instance.new("Sound")
        s.Name = "RMEXMusic"
        s.SoundId = "rbxassetid://" .. id
        s.Volume = M.Vol / 100
        s.Looped = M.Loop
        s.PlaybackSpeed = M.Speed / 100
        s.Parent = SoundService
        s:Play()
        RX.mus = s
        status.Text = "LOADING " .. id
        task.spawn(function()
            local w = 0
            while s.Parent and not s.IsLoaded and w < 8 do
                w += 0.1
                task.wait(0.1)
            end
            if not s.Parent then return end
            status.Text = s.IsLoaded and ("PLAYING " .. id) or "FAILED (private or missing)"
        end)
    end
    box.FocusLost:Connect(function(enter) if enter then playMusic() end end)
    makeBtnRow(musicPage, {
        {"mus_play", playMusic},
        {"mus_pause", function() if RX.mus then RX.mus:Pause() status.Text = "PAUSED" end end},
        {"mus_stop", function() stopMusic() status.Text = "STOPPED" end},
    })
    makeSlider(musicPage, {
        key = "mus_vol", min = 0, max = 100,
        get = function() return M.Vol end,
        set = function(v) M.Vol = math.floor(v + 0.5); if RX.mus then RX.mus.Volume = M.Vol / 100 end end,
        format = function(v) return math.floor(v + 0.5) .. "%" end,
    })
    makeSlider(musicPage, {
        key = "mus_speed", min = 25, max = 200,
        get = function() return M.Speed end,
        set = function(v) M.Speed = math.floor(v + 0.5); if RX.mus then RX.mus.PlaybackSpeed = M.Speed / 100 end end,
        format = function(v) return math.floor(v + 0.5) .. "%" end,
    })
    makeToggleRow(musicPage, {
        key = "mus_loop", desc = "mus_loop_d",
        get = function() return M.Loop end,
        set = function(v) M.Loop = v; if RX.mus then RX.mus.Looped = v end end,
    })
end

-- ============================================================================
-- PERFORMANCE WINDOWS
-- ============================================================================
do
    local Stats = game:GetService("Stats")
    local GREEN, YELLOW, RED = Color3.fromRGB(110, 235, 160), Color3.fromRGB(255, 200, 80), Color3.fromRGB(255, 90, 90)
    local function mkWin(x)
        local f = Instance.new("Frame")
        f.AnchorPoint = Vector2.new(0.5, 0)
        f.Position = UDim2.new(0.5, x, 0, 8)
        f.Size = UDim2.fromOffset(96, 26)
        f.BackgroundColor3 = Color3.fromRGB(10, 10, 16)
        f.BackgroundTransparency = 0.25
        f.BorderSizePixel = 0
        f.Active = true
        f.Visible = false
        f.Parent = gui
        corner(f, 8)
        local st = Instance.new("UIStroke")
        st.Thickness = 1
        st.Transparency = 0.5
        st.Parent = f
        local l = Instance.new("TextLabel")
        l.BackgroundTransparency = 1
        l.Size = UDim2.fromScale(1, 1)
        l.Font = Enum.Font.GothamBold
        l.TextSize = 12
        l.Text = "--"
        l.ZIndex = 2
        l.Parent = f
        makeDraggable(f, f)
        return f, l, st
    end
    local fpsF, fpsL, fpsS = mkWin(-52)
    local pingF, pingL, pingS = mkWin(52)
    local acc, frames = 0, 0
    RX.perf = function(dt)
        fpsF.Visible = RX.perfFps
        pingF.Visible = RX.perfPing
        frames += 1
        acc += dt
        if acc < 0.5 then return end
        local fps = math.floor(frames / acc + 0.5)
        frames, acc = 0, 0
        if RX.perfFps then
            local c = fps >= 50 and GREEN or (fps >= 30 and YELLOW or RED)
            fpsL.Text = "FPS " .. fps
            fpsL.TextColor3 = c
            fpsS.Color = c
        end
        if RX.perfPing then
            local ok, ms = pcall(function() return Stats.Network.ServerStatsItem["Data Ping"]:GetValue() end)
            ms = ok and math.floor(ms + 0.5) or 0
            local c = ms <= 80 and GREEN or (ms <= 160 and YELLOW or RED)
            pingL.Text = "PING " .. ms .. " ms"
            pingL.TextColor3 = c
            pingS.Color = c
        end
    end
    makeToggleRow(screenPage, {
        key = "fps_win", desc = "fps_win_d",
        get = function() return RX.perfFps end,
        set = function(v) RX.perfFps = v end,
    })
    makeToggleRow(screenPage, {
        key = "ping_win", desc = "ping_win_d",
        get = function() return RX.perfPing end,
        set = function(v) RX.perfPing = v end,
    })
end

-- ============================================================================
-- ZOOM + FOV MAPPING
-- ============================================================================

-- Maps zoom 1x..100x onto the FOV range. Zoom divides the base FOV smoothly.
local function zoomTargetFOV()
    local base = esp.FOV
    local progress = (zoomLevel - 1) / 119
    return math.clamp(math.clamp(base * ((1 / base) ^ progress), 1, math.min(base, 120)) + (RX.fovKick or 0), 1, 120)
end

-- ============================================================================
-- ESP
-- ============================================================================

local function removeESP(player)
    local data = tracked[player]
    if not data then return end
    if data.highlight then data.highlight:Destroy() end
    if data.box then data.box:Destroy() end
    tracked[player] = nil
end

-- Rounded tag with auto-width text (name / distance).
local function espPill(parent, anchorY, pos, height, font, size)
    local pill = Instance.new("Frame")
    pill.AnchorPoint = Vector2.new(0.5, anchorY)
    pill.Position = pos
    pill.Size = UDim2.fromOffset(0, height)
    pill.AutomaticSize = Enum.AutomaticSize.X
    pill.BackgroundColor3 = Color3.fromRGB(12, 12, 18)
    pill.BackgroundTransparency = 0.3
    pill.BorderSizePixel = 0
    pill.ZIndex = 7
    pill.Parent = parent
    corner(pill, 999)
    local pad = Instance.new("UIPadding")
    pad.PaddingLeft = UDim.new(0, 9)
    pad.PaddingRight = UDim.new(0, 9)
    pad.Parent = pill
    local stroke = Instance.new("UIStroke")
    stroke.Thickness = 1
    stroke.Transparency = 0.45
    stroke.Parent = pill
    local label = Instance.new("TextLabel")
    label.BackgroundTransparency = 1
    label.Size = UDim2.fromOffset(0, height)
    label.AutomaticSize = Enum.AutomaticSize.X
    label.Font = font
    label.TextSize = size
    label.TextColor3 = Color3.new(1, 1, 1)
    label.ZIndex = 8
    label.Parent = pill
    return pill, label, stroke
end

-- Smooth green -> amber -> red.
local function healthColor(ratio)
    local amber = Color3.fromRGB(255, 205, 90)
    if ratio > 0.5 then
        return amber:Lerp(HEALTH_GOOD, (ratio - 0.5) * 2)
    end
    return HEALTH_LOW:Lerp(amber, ratio * 2)
end

-- Corner brackets + soft gradient fill + side health bar + name/distance pills.
local function makeBox(player)
    local ui = {corners = {}, hp = 1}

    local box = Instance.new("Frame")
    box.Name = "RMEXBox_" .. player.Name
    box.BackgroundTransparency = 1
    box.BorderSizePixel = 0
    box.Visible = false
    box.ZIndex = 5
    box.Parent = gui
    ui.box = box

    local fill = Instance.new("Frame")
    fill.Name = "Fill"
    fill.Size = UDim2.fromScale(1, 1)
    fill.BorderSizePixel = 0
    fill.BackgroundColor3 = P.accent
    fill.ZIndex = 5
    fill.Parent = box
    corner(fill, 5)
    local fillGradient = Instance.new("UIGradient")
    fillGradient.Rotation = 90
    fillGradient.Transparency = NumberSequence.new({
        NumberSequenceKeypoint.new(0, 0.8),
        NumberSequenceKeypoint.new(1, 0.96),
    })
    fillGradient.Parent = fill
    ui.fill = fill

    local anchors = {Vector2.new(0, 0), Vector2.new(1, 0), Vector2.new(0, 1), Vector2.new(1, 1)}
    for _, a in ipairs(anchors) do
        for _, horizontal in ipairs({true, false}) do
            local bar = Instance.new("Frame")
            bar.AnchorPoint = a
            bar.Position = UDim2.fromScale(a.X, a.Y)
            bar.Size = horizontal and UDim2.fromOffset(10, 2) or UDim2.fromOffset(2, 10)
            bar.BorderSizePixel = 0
            bar.BackgroundColor3 = P.accent
            bar.ZIndex = 6
            bar.Parent = box
            corner(bar, 2)
            local glow = Instance.new("UIStroke")
            glow.Thickness = 2.5
            glow.Transparency = 0.72
            glow.Color = P.accent
            glow.Parent = bar
            table.insert(ui.corners, {frame = bar, stroke = glow, horizontal = horizontal})
        end
    end

    local hbBack = Instance.new("Frame")
    hbBack.Name = "HealthBar"
    hbBack.AnchorPoint = Vector2.new(1, 0)
    hbBack.Position = UDim2.new(0, -6, 0, 0)
    hbBack.Size = UDim2.new(0, 4, 1, 0)
    hbBack.BackgroundColor3 = Color3.fromRGB(14, 14, 20)
    hbBack.BackgroundTransparency = 0.3
    hbBack.BorderSizePixel = 0
    hbBack.ZIndex = 6
    hbBack.Parent = box
    corner(hbBack, 999)
    local hbFill = Instance.new("Frame")
    hbFill.AnchorPoint = Vector2.new(0, 1)
    hbFill.Position = UDim2.fromScale(0, 1)
    hbFill.Size = UDim2.fromScale(1, 1)
    hbFill.BackgroundColor3 = HEALTH_GOOD
    hbFill.BorderSizePixel = 0
    hbFill.ZIndex = 7
    hbFill.Parent = hbBack
    corner(hbFill, 999)
    ui.hbBack, ui.hbFill = hbBack, hbFill

    ui.namePill, ui.nameLabel, ui.nameStroke =
        espPill(box, 1, UDim2.new(0.5, 0, 0, -6), 18, Enum.Font.GothamBold, 11)
    ui.distPill, ui.distLabel, ui.distStroke =
        espPill(box, 0, UDim2.new(0.5, 0, 1, 6), 16, Enum.Font.GothamMedium, 10)

    return ui
end

local function buildESP(player, character)
    removeESP(player)
    if player == localPlayer then return end

    local humanoid = character:WaitForChild("Humanoid", 5)
    local root = character:WaitForChild("HumanoidRootPart", 5)
    local head = character:FindFirstChild("Head") or root
    if not humanoid or not root or not head then return end

    local highlight = Instance.new("Highlight")
    highlight.Name = "RMEXESPHighlight"
    highlight.Adornee = character
    highlight.FillTransparency = 0.82
    highlight.OutlineTransparency = 0.05
    highlight.DepthMode = Enum.HighlightDepthMode.Occluded
    highlight.Enabled = false
    highlight.Parent = character

    local ui = makeBox(player)
    ui.character, ui.humanoid, ui.root, ui.head = character, humanoid, root, head
    ui.highlight = highlight
    tracked[player] = ui
    applySettings()
end

applySettings = function()
    for _, data in pairs(tracked) do
        data.highlight.Enabled = settings.Outline
        data.highlight.DepthMode = settings.ThroughWalls
            and Enum.HighlightDepthMode.AlwaysOnTop
            or Enum.HighlightDepthMode.Occluded
        data.fill.Visible = settings.Boxes
        for _, c in ipairs(data.corners) do c.frame.Visible = settings.Boxes end
        data.namePill.Visible = settings.Names
        data.distPill.Visible = settings.Distance
        data.hbBack.Visible = settings.Health
    end
    if not settings.Zoom then setZoom(1) end
    setZoomVisible(settings.Zoom)
end

-- Projects the character's bounding box to screen, applies overlay stretch and smoothing.
local function updateESPBox(data, dt, vp)
    local box = data.box
    if not (settings.Boxes or settings.Names or settings.Distance or settings.Health) then
        box.Visible = false
        data.boxPos, data.boxSize = nil, nil
        return
    end

    local cam = getCam()
    local cf, size = data.character:GetBoundingBox()
    local minX, minY = math.huge, math.huge
    local maxX, maxY = -math.huge, -math.huge
    local valid = 0
    for _, sx in ipairs({-1, 1}) do
        for _, sy in ipairs({-1, 1}) do
            for _, sz in ipairs({-1, 1}) do
                local worldCorner = cf:PointToWorldSpace(
                    Vector3.new(size.X * 0.5 * sx, size.Y * 0.5 * sy, size.Z * 0.5 * sz))
                local pr = cam:WorldToViewportPoint(worldCorner)
                if pr.Z > 0 then
                    valid += 1
                    minX = math.min(minX, pr.X)
                    minY = math.min(minY, pr.Y)
                    maxX = math.max(maxX, pr.X)
                    maxY = math.max(maxY, pr.Y)
                end
            end
        end
    end

    if valid < 4 or maxX <= minX or maxY <= minY then
        box.Visible = false
        data.boxPos, data.boxSize = nil, nil
        return
    end

    local sx, sy = esp.StretchX / 100, esp.StretchY / 100
    local cx0, cy0 = vp.X * 0.5, vp.Y * 0.5
    minX = (minX - cx0) * sx + cx0
    maxX = (maxX - cx0) * sx + cx0
    minY = (minY - cy0) * sy + cy0
    maxY = (maxY - cy0) * sy + cy0

    minX = math.clamp(minX, 0, vp.X)
    maxX = math.clamp(maxX, 0, vp.X)
    minY = math.clamp(minY, 0, vp.Y)
    maxY = math.clamp(maxY, 0, vp.Y)

    local targetPos = Vector2.new(minX, minY)
    local targetSize = Vector2.new(math.max(1, maxX - minX), math.max(1, maxY - minY))

    if data.boxPos then
        local a = 1 - math.exp(-18 * math.clamp(dt, 0, 0.1))
        data.boxPos = data.boxPos:Lerp(targetPos, a)
        data.boxSize = data.boxSize:Lerp(targetSize, a)
    else
        data.boxPos, data.boxSize = targetPos, targetSize
    end

    box.Position = UDim2.fromOffset(data.boxPos.X, data.boxPos.Y)
    box.Size = UDim2.fromOffset(data.boxSize.X, data.boxSize.Y)
    box.Visible = true

    -- Corner bracket length follows the box size.
    local len = math.clamp(math.min(data.boxSize.X, data.boxSize.Y) * 0.28, 5, 24)
    if math.abs(len - (data.cornerLen or 0)) > 0.5 then
        data.cornerLen = len
        for _, c in ipairs(data.corners) do
            c.frame.Size = c.horizontal and UDim2.fromOffset(len, 2) or UDim2.fromOffset(2, len)
        end
    end
end

local function updateESPInfo(player, data, myRoot, dt)
    local dist = myRoot and (myRoot.Position - data.root.Position).Magnitude or 0
    local fade = 1 - math.clamp((dist - 120) / 380, 0, 0.55) -- far players are softer
    local fadeT = 1 - fade
    local accentC = P.accent

    -- Style: follows the theme accent, fades with distance.
    data.highlight.FillColor = accentC
    data.highlight.OutlineColor = P.text
    data.fill.BackgroundColor3 = accentC
    data.fill.BackgroundTransparency = fadeT
    for _, c in ipairs(data.corners) do
        c.frame.BackgroundColor3 = accentC
        c.frame.BackgroundTransparency = fadeT * 0.8
        c.stroke.Color = accentC
        c.stroke.Transparency = 0.72 + fadeT * 0.28
    end
    data.nameStroke.Color = accentC
    data.distStroke.Color = accentC
    data.distLabel.TextColor3 = accentC
    data.namePill.BackgroundTransparency = 0.3 + fadeT * 0.5
    data.distPill.BackgroundTransparency = 0.3 + fadeT * 0.5
    data.nameLabel.TextTransparency = fadeT * 0.6
    data.distLabel.TextTransparency = fadeT * 0.6

    -- Line of sight (checked a few times per second). Without "Through walls"
    -- the name / distance / health tags hide behind obstacles.
    data.losT = (data.losT or 0) - dt
    if data.losT <= 0 then
        data.losT = 0.12
        local cam = getCam()
        local filter = {data.character, cam}
        if localPlayer.Character then table.insert(filter, localPlayer.Character) end
        if fx.folder then table.insert(filter, fx.folder) end
        local params = RaycastParams.new()
        params.FilterType = Enum.RaycastFilterType.Exclude
        params.FilterDescendantsInstances = filter
        local origin = cam.CFrame.Position
        data.los = workspace:Raycast(origin, data.root.Position - origin, params) == nil
    end
    local show = settings.ThroughWalls or data.los ~= false
    data.namePill.Visible = settings.Names and show
    data.distPill.Visible = settings.Distance and show
    data.hbBack.Visible = settings.Health and show

    local nameText = player.DisplayName
    if player.DisplayName ~= player.Name then
        nameText = player.DisplayName .. "  @" .. player.Name
    end
    if data.nameLabel.Text ~= nameText then data.nameLabel.Text = nameText end
    local distText = string.format("%d %s", math.floor(dist + 0.5), STRINGS[lang].studs)
    if data.distLabel.Text ~= distText then data.distLabel.Text = distText end

    local ratio = math.clamp(data.humanoid.Health / math.max(data.humanoid.MaxHealth, 1), 0, 1)
    data.hp += (ratio - data.hp) * (1 - math.exp(-dt * 10))
    data.hbFill.Size = UDim2.fromScale(1, math.max(data.hp, 0.02))
    data.hbFill.BackgroundColor3 = healthColor(data.hp)
end

local function setupPlayer(player)
    if player == localPlayer then return end

    if not tracers[player] then
        local line = Instance.new("Frame")
        line.Name = "RMEXTracer_" .. player.Name
        line.AnchorPoint = Vector2.new(0.5, 0.5)
        line.Size = UDim2.fromOffset(2, 0)
        line.BorderSizePixel = 0
        line.BackgroundTransparency = 0
        line.Visible = false
        line.Parent = gui
        -- Fades in from the bottom of the screen towards the target.
        local lineGradient = Instance.new("UIGradient")
        lineGradient.Transparency = NumberSequence.new({
            NumberSequenceKeypoint.new(0, 0.97),
            NumberSequenceKeypoint.new(0.55, 0.6),
            NumberSequenceKeypoint.new(1, 0.1),
        })
        lineGradient.Parent = line
        local dot = Instance.new("Frame")
        dot.Name = "Dot"
        dot.AnchorPoint = Vector2.new(0.5, 0.5)
        dot.Position = UDim2.fromScale(1, 0.5)
        dot.Size = UDim2.fromOffset(8, 8)
        dot.BorderSizePixel = 0
        dot.ZIndex = 2
        dot.Parent = line
        corner(dot, 999)
        local dotStroke = Instance.new("UIStroke")
        dotStroke.Thickness = 2
        dotStroke.Transparency = 0.3
        dotStroke.Parent = dot
        tracers[player] = line
    end

    playerConns[player] = {
        player.CharacterAdded:Connect(function(character)
            task.spawn(buildESP, player, character)
        end),
        player.CharacterRemoving:Connect(function()
            removeESP(player)
        end),
    }

    if player.Character then
        task.spawn(buildESP, player, player.Character)
    end
end

-- ============================================================================
-- PERSONAL EFFECTS
-- ============================================================================

local function clearEffects()
    for _, c in ipairs(fx.conns) do c:Disconnect() end
    for _, inst in ipairs(fx.instances) do inst:Destroy() end
    fx = newFX()
end

local function makeFXPart(shape, size, parent)
    local p = Instance.new("Part")
    p.Shape = shape
    p.Size = size
    p.Anchored = true
    p.CanCollide = false
    p.CanTouch = false
    p.CanQuery = false
    p.CastShadow = false
    p.Material = Enum.Material.Neon
    p.Transparency = 1
    p.Parent = parent
    return p
end

local buildEffects, updateEffects

-- Everything below lives in a do-block so it does not eat into the 200-local limit of the main chunk.
local function __block1()
    local WHITE = Color3.new(1, 1, 1)
    local DARK = Color3.new(0.05, 0.05, 0.08)
    local function lw(c, a)
        if c.R * 0.3 + c.G * 0.59 + c.B * 0.11 < 0.12 then return c:Lerp(WHITE, 0.08) end
        return c:Lerp(WHITE, a)
    end
    local function coreOf(c) return lw(c, 0.82) end
    local SMOKE_TEX = "rbxasset://textures/particles/smoke_main.dds"
    local WIND_COUNT = 10
    local STREAK_COUNT = 70
    local STREAK_RADIUS = 90
    local STREAK_HEIGHT = 55
    local GHOST_HISTORY = 150
    local GHOST_BACK = 3.2

    ----------------------------------------------------------------------
    -- Color helpers
    ----------------------------------------------------------------------

    local function shiftHue(c, dh, ds, dv)
        local h, s, v = c:ToHSV()
        return Color3.fromHSV((h + dh) % 1, math.clamp(s + (ds or 0), 0, 1), math.clamp(v + (dv or 0), 0, 1))
    end

    -- White-hot head -> pure color -> slightly shifted, darker tail.
    local function glowSeq(c)
        return ColorSequence.new({
            ColorSequenceKeypoint.new(0, lw(c, 0.7)),
            ColorSequenceKeypoint.new(0.35, c),
            ColorSequenceKeypoint.new(1, shiftHue(c, 0.08, 0, -0.3)),
        })
    end

    local function softSeq(c)
        return ColorSequence.new(c, shiftHue(c, 0.06, -0.1, -0.15))
    end

    -- True once per color change for each effect group (so we don't recolor every frame).
    local function stale(name)
        local c = fx.cur[name]
        if fx.applied[name] == c then return false end
        fx.applied[name] = c
        return true
    end

    local FIRE_TEX = "rbxasset://textures/particles/fire_main.dds"
    local FIRE = {
        {rate = 14, lmin = 0.5, lmax = 0.9, v1 = 1, v2 = 3, ac = 5, ember = 20, smoke = 0},
        {rate = 34, lmin = 0.7, lmax = 1.3, v1 = 2, v2 = 5, ac = 8, ember = 30, smoke = 14},
        {rate = 5, lmin = 0.4, lmax = 0.7, v1 = 1, v2 = 2, ac = 3, ember = 60, smoke = 0},
        {rate = 10, lmin = 1.0, lmax = 1.8, v1 = 0.4, v2 = 1.2, ac = 2, ember = 6, smoke = 4},
    }

    local PET = {
        {rate = 14, l1 = 2.5, l2 = 4, v1 = 0.3, v2 = 1, ac = -3, sz = 1},
        {rate = 40, l1 = 3, l2 = 5, v1 = 0, v2 = 0.5, ac = -1.5, sz = 0.45},
        {rate = 10, l1 = 1.5, l2 = 2.5, v1 = 1, v2 = 3, ac = 2, sz = 0.8},
    }
    local SMK = {
        {rate = 18, l1 = 1.2, l2 = 2.2, v1 = 1, v2 = 2.5, ac = 1, sz = 1},
        {rate = 30, l1 = 2, l2 = 3, v1 = 0.5, v2 = 1.5, ac = 0, sz = 1.7},
        {rate = 22, l1 = 1.5, l2 = 2.5, v1 = 2, v2 = 4, ac = 3, sz = 0.8},
    }
    local emB = setmetatable({}, {__mode = "k"})
    local function tuneSize(e, sk, vk)
        local b = emB[e]
        if not b then
            b = {size = e.Size, speed = e.Speed, accel = e.Acceleration}
            emB[e] = b
        end
        if b.sk ~= sk then
            b.sk = sk
            local kp = {}
            for i, k in ipairs(b.size.Keypoints) do
                kp[i] = NumberSequenceKeypoint.new(k.Time, k.Value * sk, k.Envelope * sk)
            end
            e.Size = NumberSequence.new(kp)
        end
        e.TimeScale = vk
        return b
    end
    local function tune(e, sk, vk, mode)
        local b = tuneSize(e, sk, vk)
        if b.mode ~= mode then
            b.mode = mode
            e.Acceleration = mode == 2 and (b.accel + Vector3.new(0, 6, 0)) or b.accel
            local m = mode == 3 and 2.5 or 1
            e.Speed = NumberRange.new(b.speed.Min * m, b.speed.Max * m)
        end
    end
    local trB = setmetatable({}, {__mode = "k"})
    local function tuneTrail(tr, sk, vk)
        local b = trB[tr]
        if not b then
            b = {w = tr.WidthScale, life = tr.Lifetime}
            trB[tr] = b
        end
        if b.sk ~= sk then
            b.sk = sk
            local kp = {}
            for i, k in ipairs(b.w.Keypoints) do
                kp[i] = NumberSequenceKeypoint.new(k.Time, k.Value * sk, k.Envelope * sk)
            end
            tr.WidthScale = NumberSequence.new(kp)
        end
        tr.Lifetime = b.life / math.max(vk, 0.2)
    end
    -- Per-effect settings: returns cfg, own clock (speed applied), color, glow, soft.
    local function FXC(name, dt)
        local C0 = visual.cfg[name]
        local k = fx.clk
        local tt = k[name] or 0
        local C, c = RX.fxMod.apply(name, C0, tt, C0.Color or getEffectColor())
        k[name] = tt + dt * C.Speed
        fx.cur[name:lower()] = c
        if name == "Aura" then fx.cur.shell = c end
        if fx.gcol[name] ~= c then
            fx.gcol[name] = c
            fx.gs[name] = glowSeq(c)
            fx.ss[name] = softSeq(c)
        end
        return C, k[name], c, fx.gs[name], fx.ss[name]
    end

    local function showGroup(name, on)
        if fx.shown[name] == on then return end
        fx.shown[name] = on
        for _, item in ipairs(fx.groups[name]) do
            item.part.Transparency = on and item.tr or 1
        end
    end

    local function groupAdd(name, part, tr)
        table.insert(fx.groups[name], {part = part, tr = tr})
        return part
    end

    ----------------------------------------------------------------------
    -- Batched CFrame moves (one engine call per frame instead of hundreds)
    ----------------------------------------------------------------------

    local mvParts, mvCFs, mvN = {}, {}, 0

    local function pushMove(part, cf)
        mvN += 1
        mvParts[mvN] = part
        mvCFs[mvN] = cf
    end

    local function flushMoves()
        if mvN > 0 then
            for i = #mvParts, mvN + 1, -1 do
                mvParts[i] = nil
                mvCFs[i] = nil
            end
            workspace:BulkMoveTo(mvParts, mvCFs, Enum.BulkMoveMode.FireCFrameChanged)
        end
        mvN = 0
    end

    ----------------------------------------------------------------------
    -- Ground rings, bursts, footsteps
    ----------------------------------------------------------------------

    local function groundPoint(maxDist)
        if not fx.root then return nil end
        local params = fx.gpParams
        if not params then
            params = RaycastParams.new()
            params.FilterType = Enum.RaycastFilterType.Exclude
            fx.gpParams = params
        end
        params.FilterDescendantsInstances = {fx.character, fx.folder}
        local hit = workspace:Raycast(fx.root.Position, Vector3.new(0, -(maxDist or 7), 0), params)
        return hit and hit.Position or nil
    end

    -- A crisp expanding ring drawn on the ground (hollow circle, not a filled disc).
    -- v15: rings come from a small pool with a fixed-size canvas, so a jump / step never creates a
    -- SurfaceGui at runtime (that allocation was the hitch on jump and landing).
    local RING_BASE_T = {0.08, 0.25, 0.45}
    local function newRingEntry()
        local part = makeFXPart(Enum.PartType.Block, Vector3.new(0.8, 0.05, 0.8), fx.folder)
        part.Material = Enum.Material.SmoothPlastic
        local gui = Instance.new("SurfaceGui")
        gui.Face = Enum.NormalId.Top
        gui.SizingMode = Enum.SurfaceGuiSizingMode.FixedSize
        gui.CanvasSize = Vector2.new(256, 256)
        gui.LightInfluence = 0
        gui.Brightness = 3
        gui.ClipsDescendants = false
        gui.Enabled = false
        gui.Adornee = part
        gui.Parent = part
        local strokes = {}
        local function addRing(scale, thick)
            local f = Instance.new("Frame")
            f.AnchorPoint = Vector2.new(0.5, 0.5)
            f.Position = UDim2.fromScale(0.5, 0.5)
            f.Size = UDim2.fromScale(scale, scale)
            f.BackgroundTransparency = 1
            f.BorderSizePixel = 0
            f.Parent = gui
            local uc = Instance.new("UICorner")
            uc.CornerRadius = UDim.new(0.5, 0)
            uc.Parent = f
            local st = Instance.new("UIStroke")
            st.Thickness = thick
            st.Transparency = 1
            st.Parent = f
            table.insert(strokes, st)
        end
        addRing(0.94, 6)
        addRing(0.8, 2.5)
        addRing(0.56, 3.5)
        return {part = part, gui = gui, strokes = strokes, busy = false}
    end

    local function spawnRing(pos, color, diameter, duration)
        if fx.stepCount >= STEP_LIMIT or not fx.folder then return end
        fx.ringPool = fx.ringPool or {}
        local e
        for _, r in ipairs(fx.ringPool) do
            if not r.busy then
                e = r
                break
            end
        end
        if not e then
            if #fx.ringPool >= 8 then return end
            e = newRingEntry()
            table.insert(fx.ringPool, e)
        end
        fx.stepCount += 1
        e.busy = true
        local part = e.part
        part.Size = Vector3.new(0.8, 0.05, 0.8)
        part.CFrame = CFrame.new(pos + Vector3.new(0, 0.08, 0))
        e.strokes[1].Color = color
        e.strokes[2].Color = color:Lerp(WHITE, 0.75)
        e.strokes[3].Color = color
        for k, st in ipairs(e.strokes) do st.Transparency = RING_BASE_T[k] end
        e.gui.Enabled = true

        local tw = tween(part, {Size = Vector3.new(diameter, 0.05, diameter)}, duration, Enum.EasingStyle.Quart, Enum.EasingDirection.Out)
        for _, st in ipairs(e.strokes) do
            tween(st, {Transparency = 1}, duration, Enum.EasingStyle.Quad, Enum.EasingDirection.In)
        end
        tw.Completed:Connect(function()
            fx.stepCount = math.max(0, fx.stepCount - 1)
            e.gui.Enabled = false
            e.busy = false
        end)
    end

    local spawnBurst
    local function spawnStep(color, sk, mode)
        if fx.stepCount >= STEP_LIMIT or not fx.root or not fx.folder then return end
        local ground = groundPoint(6)
        if not ground then return end
        if mode == 3 then
            spawnBurst(7, color, 0, "sparks")
        else
            spawnRing(ground, color, 4.8 * sk, 0.75)
            if mode == 2 then
                task.delay(0.14, function()
                    if fx.folder then spawnRing(ground, color, 7.2 * sk, 0.8) end
                end)
            end
        end
    end

    local function newBurstEntry()
        local anchor = makeFXPart(Enum.PartType.Ball, Vector3.new(0.2, 0.2, 0.2), fx.folder)
        local sparks = Instance.new("ParticleEmitter")
        sparks.Rate = 0
        sparks.Lifetime = NumberRange.new(0.45, 0.95)
        sparks.Speed = NumberRange.new(6, 16)
        sparks.EmissionDirection = Enum.NormalId.Top
        sparks.SpreadAngle = Vector2.new(60, 60)
        sparks.Acceleration = Vector3.new(0, -24, 0)
        sparks.Drag = 1.4
        sparks.LightEmission = 1
        sparks.LightInfluence = 0
        sparks.Rotation = NumberRange.new(0, 360)
        sparks.RotSpeed = NumberRange.new(-200, 200)
        sparks.Size = NumberSequence.new({NumberSequenceKeypoint.new(0, 0.32), NumberSequenceKeypoint.new(1, 0)})
        sparks.Transparency = NumberSequence.new({
            NumberSequenceKeypoint.new(0, 0), NumberSequenceKeypoint.new(0.7, 0.2), NumberSequenceKeypoint.new(1, 1),
        })
        sparks.Parent = anchor
        local puff = Instance.new("ParticleEmitter")
        puff.Texture = SMOKE_TEX
        puff.Rate = 0
        puff.Lifetime = NumberRange.new(0.5, 0.9)
        puff.Speed = NumberRange.new(2, 6)
        puff.EmissionDirection = Enum.NormalId.Top
        puff.SpreadAngle = Vector2.new(85, 85)
        puff.Drag = 3
        puff.LightEmission = 0.8
        puff.LightInfluence = 0
        puff.Rotation = NumberRange.new(0, 360)
        puff.Size = NumberSequence.new({NumberSequenceKeypoint.new(0, 0.8), NumberSequenceKeypoint.new(1, 2.8)})
        puff.Transparency = NumberSequence.new({NumberSequenceKeypoint.new(0, 0.65), NumberSequenceKeypoint.new(1, 1)})
        puff.Parent = anchor
        return {anchor = anchor, sparks = sparks, puff = puff, busy = false}
    end

    spawnBurst = function(count, color, ringSize, mode)
        if not fx.root or not fx.folder then return end
        local ground = groundPoint(8) or (fx.root.Position - Vector3.new(0, 2.8, 0))
        fx.burstPool = fx.burstPool or {}
        local e
        for _, b in ipairs(fx.burstPool) do
            if not b.busy then
                e = b
                break
            end
        end
        if not e and #fx.burstPool < 4 then
            e = newBurstEntry()
            table.insert(fx.burstPool, e)
        end
        if e and mode ~= "ring" then
            e.busy = true
            e.anchor.CFrame = CFrame.new(ground + Vector3.new(0, 0.15, 0))
            e.sparks.Color = glowSeq(color)
            e.puff.Color = softSeq(color)
            e.sparks:Emit(count)
            e.puff:Emit(math.max(2, math.floor(count / 5)))
            task.delay(1.6, function() e.busy = false end)
        end
        if mode ~= "sparks" then spawnRing(ground, color, ringSize or 7, 0.8) end
    end

    -- create the pooled objects right after the character is built, so the first jump is already smooth
    local function prewarmPools()
        if not fx.folder then return end
        fx.ringPool, fx.burstPool = fx.ringPool or {}, fx.burstPool or {}
        for _ = #fx.ringPool + 1, 3 do table.insert(fx.ringPool, newRingEntry()) end
        for _ = #fx.burstPool + 1, 2 do table.insert(fx.burstPool, newBurstEntry()) end
    end

    ----------------------------------------------------------------------
    -- Lightning (real jagged bolts built from thin neon segments)
    ----------------------------------------------------------------------

    local function hideBolt(bolt)
        if not bolt.visible then return end
        bolt.visible = false
        for i = 1, #bolt.glow do
            bolt.glow[i].Transparency = 1
            bolt.core[i].Transparency = 1
        end
    end

    local function layoutBolt(bolt, p0, p1, color)
        local dir = p1 - p0
        local len = dir.Magnitude
        if len < 0.5 then return false end
        local fwd = dir / len
        local ref = math.abs(fwd.Y) > 0.9 and Vector3.xAxis or Vector3.yAxis
        local sideV = fwd:Cross(ref).Unit
        local upV = fwd:Cross(sideV)

        if not bolt.visible then
            bolt.visible = true
            for i = 1, #bolt.glow do
                bolt.glow[i].Transparency = 0.5
                bolt.core[i].Transparency = 0.03
            end
        end
        if bolt.col ~= color then
            bolt.col = color
            for i = 1, #bolt.glow do
                bolt.glow[i].Color = color
                bolt.core[i].Color = coreOf(color)
            end
        end

        local n = #bolt.glow
        local pts = table.create(n + 1)
        pts[1] = p0
        local amp = math.min(len * 0.2, 0.95)
        for i = 1, n - 1 do
            local f = i / n
            local fall = math.sin(f * math.pi)
            pts[i + 1] = p0 + dir * f
                + sideV * ((math.random() - 0.5) * 2 * amp * fall)
                + upV * ((math.random() - 0.5) * 2 * amp * fall)
        end
        pts[n + 1] = p1

        local w = (0.045 + math.random() * 0.04) * (fx.boltW or 1)
        for i = 1, n do
            local a, b = pts[i], pts[i + 1]
            local d = b - a
            local l = d.Magnitude
            local mid = a + d * 0.5
            local look = CFrame.lookAt(mid, mid + (l > 0.001 and d or fwd))
            bolt.glow[i].Size = Vector3.new(w * 3.4, w * 3.4, l + w * 2)
            bolt.core[i].Size = Vector3.new(w, w, l + w)
            pushMove(bolt.glow[i], look)
            pushMove(bolt.core[i], look)
        end
        return true
    end

    ----------------------------------------------------------------------
    -- Sword colors
    ----------------------------------------------------------------------

    local function swordPartColor(kind, color)
        if kind == "white" then
            return WHITE:Lerp(color, 0.12)
        elseif kind == "accent" then
            return color:Lerp(WHITE, 0.5)
        elseif kind == "grip" then
            return color:Lerp(DARK, 0.7)
        end
        return color
    end

    ----------------------------------------------------------------------
    -- Small builders
    ----------------------------------------------------------------------

    local function newEmitter(parent, o)
        local e = Instance.new("ParticleEmitter")
        e.Enabled = false
        if o.texture then e.Texture = o.texture end
        e.Rate = o.rate
        e.Lifetime = NumberRange.new(o.lifeMin, o.lifeMax)
        e.Speed = NumberRange.new(o.speedMin, o.speedMax)
        e.Drag = o.drag or 1
        e.Acceleration = o.accel or Vector3.zero
        e.LightEmission = o.emission or 1
        e.LightInfluence = 0
        e.Rotation = NumberRange.new(0, 360)
        e.RotSpeed = NumberRange.new(-o.rot, o.rot)
        e.SpreadAngle = o.spread or Vector2.new(180, 180)
        if o.sphere then
            e.Shape = Enum.ParticleEmitterShape.Sphere
            e.ShapeStyle = Enum.ParticleEmitterShapeStyle.Volume
            e.ShapeInOut = Enum.ParticleEmitterShapeInOut.Outward
        end
        if o.top then e.EmissionDirection = Enum.NormalId.Top end
        e.Size = NumberSequence.new({
            NumberSequenceKeypoint.new(0, o.size * (o.startScale or 0.4)),
            NumberSequenceKeypoint.new(0.4, o.size),
            NumberSequenceKeypoint.new(1, o.endSize or 0),
        })
        e.Transparency = NumberSequence.new({
            NumberSequenceKeypoint.new(0, o.t0 or 0.1),
            NumberSequenceKeypoint.new(0.6, o.t1 or 0.35),
            NumberSequenceKeypoint.new(1, 1),
        })
        e.Parent = parent
        return e
    end

    local function newTrail(a0, a1, parent, o)
        local tr = Instance.new("Trail")
        tr.Attachment0 = a0
        tr.Attachment1 = a1
        tr.Lifetime = o.life
        tr.MinLength = 0.02
        tr.FaceCamera = true
        tr.LightEmission = 1
        tr.LightInfluence = 0
        tr.WidthScale = NumberSequence.new({
            NumberSequenceKeypoint.new(0, o.w0 or 1),
            NumberSequenceKeypoint.new(0.35, o.w1 or 0.6),
            NumberSequenceKeypoint.new(1, 0),
        })
        tr.Transparency = NumberSequence.new({
            NumberSequenceKeypoint.new(0, o.t0 or 0.05),
            NumberSequenceKeypoint.new(0.5, o.t1 or 0.4),
            NumberSequenceKeypoint.new(1, 1),
        })
        tr.Enabled = false
        tr.Parent = parent
        return tr
    end

    local function chatColor(item, color)
        if item.kind == "rim" then return color:Lerp(WHITE, 0.4) end
        if item.kind == "tip" then return color:Lerp(WHITE, 0.6) end
        local c = color:Lerp(DARK, 0.5 - 0.35 * item.u)
        if item.i % 3 == 0 then c = c:Lerp(WHITE, 0.18) end
        return c
    end

    local function hatColor(kind, color)
        if kind == "dark" then
            return color:Lerp(DARK, 0.7)
        elseif kind == "rim" then
            return color:Lerp(WHITE, 0.45)
        end
        return color
    end

    -- Puts a streak at a random place around the player and restarts its trail.
    local function respawnStreak(s, center, anywhere)
        local ang = math.random() * math.pi * 2
        local rad = anywhere and STREAK_RADIUS * math.sqrt(math.random())
            or STREAK_RADIUS * (0.85 + 0.15 * math.random())
        local h = (math.random() - 0.35) * STREAK_HEIGHT
        s.pos = center + Vector3.new(math.cos(ang) * rad, h, math.sin(ang) * rad)
        local inward = Vector3.new(center.X - s.pos.X, 0, center.Z - s.pos.Z)
        inward = inward.Magnitude > 0.1 and inward.Unit or Vector3.zero
        local d = inward * (anywhere and 0 or 0.9)
            + Vector3.new(math.random() - 0.5, (math.random() - 0.5) * 0.4, math.random() - 0.5)
        if d.Magnitude < 0.1 then d = Vector3.new(1, 0, 0) end
        s.vel = d.Unit * (6 + math.random() * 10)
        s.phase = math.random() * 6.28
        s.wait = 2
        s.trail.Enabled = false
    end

    -- Finds the recorded pose from time T (interpolating between two snapshots).
    local function ghostSample(g, T)
        local i, last = g.idx, nil
        for _ = 1, g.count do
            local s = g.hist[i]
            if s.t <= T then
                if i == g.idx then return s, s, 0 end
                local nx = g.hist[i % GHOST_HISTORY + 1]
                local span = nx.t - s.t
                return s, nx, span > 1e-4 and (T - s.t) / span or 0
            end
            last = s
            i = (i == 1) and GHOST_HISTORY or (i - 1)
        end
        return last, last, 0
    end

    ----------------------------------------------------------------------
    -- Live copies of the character (lagging bot + aura shell).
    -- The game can replace body parts / accessories after we spawn (skin
    -- loading, avatar change, new outfit), so we never trust parts found once:
    -- a cheap "appearance signature" is polled and the copies are rebuilt
    -- from the CURRENT character whenever it changes.
    ----------------------------------------------------------------------

    local Rep = {}
    local partIds = setmetatable({}, {__mode = "k"})
    local nextPartId = 0

    function Rep.id(part)
        local id = partIds[part]
        if not id then
            nextPartId += 1
            id = nextPartId
            partIds[part] = id
        end
        return id
    end

    function Rep.set(obj, prop, value)
        pcall(function() obj[prop] = value end)
    end

    -- Clone() returns nil for non-archivable instances, so allow it for a moment.
    function Rep.clone(inst)
        local was = inst.Archivable
        inst.Archivable = true
        local ok, copy = pcall(function() return inst:Clone() end)
        inst.Archivable = was
        if ok and typeof(copy) == "Instance" then return copy end
        return nil
    end

    -- Changes whenever the look of the character changes (parts, meshes, colors, clothes, face...).
    function Rep.sig(character)
        local out, n = {}, 0
        for _, d in ipairs(character:GetDescendants()) do
            local item
            if d:IsA("BasePart") then
                local sz = d.Size
                item = string.format("%d:%.2f,%.2f,%.2f:%s:%d:%d", Rep.id(d), sz.X, sz.Y, sz.Z,
                    d.Color:ToHex(), d.Material.Value, d.Transparency >= 0.95 and 1 or 0)
                if d:IsA("MeshPart") then item = item .. d.MeshId .. d.TextureID end
            elseif d:IsA("SpecialMesh") then
                item = "m" .. d.MeshId .. d.TextureId .. tostring(d.Scale)
            elseif d:IsA("Decal") then
                item = "d" .. d.Texture
            elseif d:IsA("Shirt") then
                item = "s" .. d.ShirtTemplate
            elseif d:IsA("Pants") then
                item = "p" .. d.PantsTemplate
            elseif d:IsA("ShirtGraphic") then
                item = "g" .. d.Graphic
            elseif d:IsA("SurfaceAppearance") then
                item = "a" .. d.ColorMap
            end
            if item then
                n += 1
                out[n] = item
            end
        end
        return table.concat(out, ";")
    end

    -- Full copy of the character (real colors, face, clothes, accessories),
    -- cut into independent anchored parts. Returns the model and a part list.
    function Rep.cloneCharacter(character)
        local srcById, descs = {}, character:GetDescendants()
        local wasArch = {}
        for _, d in ipairs(descs) do
            wasArch[d] = d.Archivable
            d.Archivable = true
            if d:IsA("BasePart") then
                local id = Rep.id(d)
                srcById[id] = d
                d:SetAttribute("RMEXid", id)
            end
        end
        local wasModel = character.Archivable
        character.Archivable = true
        local model = Rep.clone(character)
        character.Archivable = wasModel
        for _, d in ipairs(descs) do
            if d:IsA("BasePart") then d:SetAttribute("RMEXid", nil) end
            d.Archivable = wasArch[d]
        end
        if not model then return nil end

        model.Name = "RMEX_Ghost"
        local entries = {}
        for _, d in ipairs(model:GetDescendants()) do
            if d:IsA("LuaSourceContainer") or d:IsA("JointInstance") or d:IsA("Constraint")
                or d:IsA("WeldConstraint") or d:IsA("ParticleEmitter") or d:IsA("Trail")
                or d:IsA("Beam") or d:IsA("Light") or d:IsA("Highlight") or d:IsA("Sound")
                or d:IsA("Fire") or d:IsA("Smoke") or d:IsA("Sparkles") or d:IsA("ForceField")
                or d:IsA("BillboardGui") or d:IsA("SurfaceGui") then
                d:Destroy()
            elseif d:IsA("BasePart") then
                local id = d:GetAttribute("RMEXid")
                d:SetAttribute("RMEXid", nil)
                local src = id and srcById[id]
                if src then
                    d.Anchored = true
                    d.CanCollide = false
                    d.CanTouch = false
                    d.CanQuery = false
                    d.CastShadow = false
                    d.Massless = true
                    local base = d.Transparency
                    table.insert(entries, {
                        src = src, part = d, id = id, base = base, hidden = base >= 0.95,
                    })
                    d.Transparency = 1
                end
            elseif d:IsA("Humanoid") then
                d.DisplayDistanceType = Enum.HumanoidDisplayDistanceType.None
                d.HealthDisplayType = Enum.HumanoidHealthDisplayType.AlwaysOff
                Rep.set(d, "RequiresNeck", false)
                Rep.set(d, "BreakJointsOnDeath", false)
                Rep.set(d, "AutomaticScalingEnabled", false)
                Rep.set(d, "EvaluateStateMachine", false)
            end
        end
        return model, entries
    end

    -- Thin neon copies of the visible body parts, slightly inflated: the aura shell.
    function Rep.buildShell(character, root, folder)
        local list = {}
        for _, d in ipairs(character:GetDescendants()) do
            if #list >= 40 then break end
            if d:IsA("BasePart") and d ~= root and d.Transparency < 0.95 and d.Size.Magnitude > 0.2 then
                local p = Rep.clone(d)
                if p then
                    p:ClearAllChildren()
                    local mesh = d:FindFirstChildOfClass("SpecialMesh")
                    if mesh then
                        local m = Rep.clone(mesh)
                        if m then m.Parent = p end
                    end
                    if p:IsA("MeshPart") then p.TextureID = "" end
                    p.Anchored = true
                    p.CanCollide = false
                    p.CanTouch = false
                    p.CanQuery = false
                    p.CastShadow = false
                    p.Massless = true
                    p.Material = Enum.Material.Neon
                    p.Reflectance = 0
                    p.Size = d.Size + Vector3.new(0.16, 0.16, 0.16)
                    p.Transparency = 1
                    p.Parent = folder
                    table.insert(list, {src = d, part = p})
                end
            end
        end
        return list
    end

    ----------------------------------------------------------------------
    -- Distant lightning: a rare big bolt 100-500 studs away, with branches,
    -- a flare on the ground and a faint screen flash.
    ----------------------------------------------------------------------

    local FAR = {main = 18, branches = 2, bseg = 7}

    local function spawnFarStrike(color)
        local far = fx.far
        local origin = fx.root.Position
        local ang = math.random() * math.pi * 2
        local dist = 100 + math.random() * 400
        local dir2 = Vector3.new(math.cos(ang), 0, math.sin(ang))
        local gx, gz = origin.X + dir2.X * dist, origin.Z + dir2.Z * dist

        local params = RaycastParams.new()
        params.FilterType = Enum.RaycastFilterType.Exclude
        params.FilterDescendantsInstances = {fx.character, fx.folder}
        local hit = workspace:Raycast(Vector3.new(gx, origin.Y + 300, gz), Vector3.new(0, -700, 0), params)
        local ground = hit and hit.Position or Vector3.new(gx, origin.Y - 3, gz)
        local height = 260 + math.random() * 160
        local top = Vector3.new(gx + (math.random() - 0.5) * 60, ground.Y + height, gz + (math.random() - 0.5) * 60)
        local side = dir2:Cross(Vector3.yAxis).Unit

        local function path(p0, p1, n, amp)
            local pts = {p0}
            for i = 1, n - 1 do
                local f = i / n
                local fall = math.sin(f * math.pi) ^ 0.5
                pts[i + 1] = p0:Lerp(p1, f)
                    + side * ((math.random() - 0.5) * 2 * amp * fall)
                    + dir2 * ((math.random() - 0.5) * 2 * amp * fall * 0.6)
            end
            pts[n + 1] = p1
            return pts
        end

        local function layout(idx, a, b, width)
            local slot = far.slots[idx]
            local d = b - a
            local mid = a + d * 0.5
            local cf = CFrame.lookAt(mid, mid + d)
            slot.core.Size = Vector3.new(width, width, d.Magnitude + width)
            slot.glow.Size = Vector3.new(width * 3.2, width * 3.2, d.Magnitude + width * 2)
            slot.core.CFrame = cf
            slot.glow.CFrame = cf
            slot.core.Color = coreOf(color)
            slot.glow.Color = color
        end

        -- thick enough to be seen from far away
        local w = 0.5 + dist * 0.009
        local pts = path(top, ground, FAR.main, height * 0.05)
        for i = 1, FAR.main do
            layout(i, pts[i], pts[i + 1], w * (0.7 + 0.3 * i / FAR.main))
        end

        local used = FAR.main
        for _ = 1, FAR.branches do
            local a0 = pts[math.random(4, FAR.main - 5)]
            local sgn = math.random() < 0.5 and -1 or 1
            local bdir = ((ground - a0).Unit * 0.7 + side * sgn * 0.9 + dir2 * (math.random() - 0.5) * 0.6).Unit
            local blen = height * (0.18 + math.random() * 0.15)
            local bp = path(a0, a0 + bdir * blen, FAR.bseg, blen * 0.07)
            for i = 1, FAR.bseg do
                used += 1
                layout(used, bp[i], bp[i + 1], w * 0.45)
            end
        end
        far.used = used

        far.flare.Size = Vector3.new(w * 7, w * 7, w * 7)
        far.flare.CFrame = CFrame.new(ground + Vector3.new(0, w, 0))
        far.flare.Color = color
        far.power = 0.05 + 0.13 * (1 - (dist - 100) / 400)
        far.active = true
        far.t0 = os.clock()
    end

    -- Brightness over time: a hard flash, a flicker, then a slow fade.
    local function strikeBrightness(a)
        if a < 0.06 then return 1 end
        if a < 0.11 then return 0.25 end
        if a < 0.2 then return 0.9 end
        if a < 0.26 then return 0.3 end
        if a < 0.34 then return 0.75 end
        return math.max(0, 1 - (a - 0.34) / 0.5) * 0.7
    end

    -- Body parts for glitch / attachments for lightning, looked up on the live
    -- character (the old lists die together with replaced parts).
    local function refreshBody()
        local character = fx.character
        if not character then return end
        local parts = {}
        for _, child in ipairs(character:GetChildren()) do
            if child:IsA("BasePart") and child ~= fx.root then table.insert(parts, child) end
        end
        fx.bodyParts = parts
        local atts = {}
        for _, name in ipairs(BEAM_PARTS) do
            local part = character:FindFirstChild(name)
            if part and part:IsA("BasePart") then
                local a = part:FindFirstChild("RMEX_Beam")
                if not a then
                    a = Instance.new("Attachment")
                    a.Name = "RMEX_Beam"
                    a.Parent = part
                    table.insert(fx.instances, a)
                end
                table.insert(atts, a)
            end
        end
        fx.attachments = atts
    end

    local function rebuildGhost()
        local g = fx.ghost
        if g.model then g.model:Destroy() end
        g.model, g.entries, g.sig, g.shownAlpha = nil, {}, fx.sig, -1
        local model, entries = Rep.cloneCharacter(fx.character)
        if not model then return end
        for _, e in ipairs(entries) do e.cur = nil end
        model.Parent = fx.folder
        g.model, g.entries = model, entries
    end

    local function rebuildShell()
        local sh = fx.shell
        for _, e in ipairs(sh.entries) do e.part:Destroy() end
        sh.entries = Rep.buildShell(fx.character, fx.root, fx.folder)
        sh.sig, sh.tr, sh.fresh = fx.sig, nil, true
    end

    ----------------------------------------------------------------------
    -- BUILD
    ----------------------------------------------------------------------

    buildEffects = function(character)
        clearEffects()
        local root = character:WaitForChild("HumanoidRootPart", 10)
        local humanoid = character:WaitForChild("Humanoid", 10)
        if not root or not humanoid then return end

        local function keep(inst)
            table.insert(fx.instances, inst)
            return inst
        end

        fx.folder = keep(Instance.new("Folder"))
        fx.folder.Name = "RMEX_FX"
        fx.folder.Parent = workspace

        -- Aura: pulsing outline, soft light, rising mist ------------------
        local aura = keep(Instance.new("Highlight"))
        aura.Name = "RMEX_Aura"
        aura.Adornee = character
        aura.DepthMode = Enum.HighlightDepthMode.Occluded
        aura.FillTransparency = 0.85
        aura.OutlineTransparency = 0
        aura.Enabled = false
        aura.Parent = character
        fx.aura = aura
        fx.shell = {entries = {}, sig = nil, tr = nil, fresh = true, shown = false}

        local light = keep(Instance.new("PointLight"))
        light.Brightness = 0.9
        light.Range = 9
        light.Shadows = false
        light.Enabled = false
        light.Parent = root
        fx.light = light

        fx.mist = keep(newEmitter(root, {
            texture = SMOKE_TEX, rate = 9, lifeMin = 1.2, lifeMax = 2.1, speedMin = 0.4, speedMax = 1.2,
            drag = 0.8, accel = Vector3.new(0, 1.6, 0), emission = 0.8, rot = 25,
            spread = Vector2.new(25, 25), top = true,
            size = 2.2, startScale = 0.5, endSize = 3.4, t0 = 1, t1 = 0.84,
        }))

        -- Particles: fine sparkles, soft motes, rising embers -------------
        local layers = {
            {rate = 32, lifeMin = 0.8, lifeMax = 1.5, speedMin = 0.4, speedMax = 2.2, size = 0.2, rot = 140,
                drag = 1.2, accel = Vector3.new(0, 0.9, 0), sphere = true, t0 = 0.05, t1 = 0.3},
            {texture = SMOKE_TEX, rate = 10, lifeMin = 1.2, lifeMax = 2.2, speedMin = 0.2, speedMax = 0.9, size = 0.55,
                rot = 30, drag = 1, sphere = true, startScale = 0.3, t0 = 0.55, t1 = 0.75},
            {rate = 9, lifeMin = 1.4, lifeMax = 2.6, speedMin = 0.6, speedMax = 1.6, size = 0.14, rot = 90,
                drag = 0.6, accel = Vector3.new(0, 2.6, 0), spread = Vector2.new(40, 40), top = true, t0 = 0, t1 = 0.25},
        }
        for _, cfg in ipairs(layers) do
            local e = keep(newEmitter(root, cfg))
            table.insert(fx.emitters, e)
        end

        -- Energy trail: soft body ribbon + white-hot core -----------------
        local top = keep(Instance.new("Attachment"))
        top.Position = Vector3.new(0, 1.25, 0)
        top.Parent = root
        local bottom = keep(Instance.new("Attachment"))
        bottom.Position = Vector3.new(0, -1.2, 0)
        bottom.Parent = root
        fx.trail = keep(newTrail(top, bottom, root, {life = 0.6, w0 = 1, w1 = 0.7, t0 = 0.12, t1 = 0.55}))

        local topC = keep(Instance.new("Attachment"))
        topC.Position = Vector3.new(0, 0.55, 0)
        topC.Parent = root
        local bottomC = keep(Instance.new("Attachment"))
        bottomC.Position = Vector3.new(0, -0.55, 0)
        bottomC.Parent = root
        fx.trailCore = keep(newTrail(topC, bottomC, root, {life = 0.32, w0 = 1, w1 = 0.5, t0 = 0, t1 = 0.35}))

        -- Rings: three tilted gyroscope rings, each with two comets -------
        for ri = 1, #RINGS do
            fx.rings[ri] = {}
            for seg = 1, RING_SEGMENTS do
                local u = (((seg - 1) / RING_SEGMENTS) * 2) % 1
                local sz = 0.05 + 0.12 * u ^ 1.5
                local part = makeFXPart(Enum.PartType.Ball, Vector3.new(sz, sz, sz), fx.folder)
                groupAdd("rings", part, 0.9 - 0.86 * u * u)
                fx.rings[ri][seg] = {part = part, u = u}
            end
        end

        -- Swords: tapered glowing blades hovering tip-down with swoosh trails
        for i = 1, SWORD_COUNT do
            local sword = {phase = (i - 1) * math.pi * 2 / SWORD_COUNT, parts = {}}
            local function add(shape, size, off, kind, tr, material)
                local p = makeFXPart(shape, size, fx.folder)
                if material then p.Material = material end
                groupAdd("swords", p, tr)
                table.insert(sword.parts, {part = p, off = off, kind = kind})
                return p
            end
            local B, Ball = Enum.PartType.Block, Enum.PartType.Ball
            add(B, Vector3.new(0.12, 0.55, 0.12), CFrame.new(0, 1.15, 0), "grip", 0.05, Enum.Material.SmoothPlastic)
            add(Ball, Vector3.new(0.24, 0.24, 0.24), CFrame.new(0, 1.5, 0), "accent", 0.04)
            add(B, Vector3.new(0.12, 0.1, 0.74), CFrame.new(0, 0.82, 0), "color", 0.04)
            add(Ball, Vector3.new(0.15, 0.15, 0.15), CFrame.new(0, 0.82, 0.39), "white", 0.04)
            add(Ball, Vector3.new(0.15, 0.15, 0.15), CFrame.new(0, 0.82, -0.39), "white", 0.04)
            add(B, Vector3.new(0.07, 0.9, 0.30), CFrame.new(0, 0.32, 0), "color", 0.06)
            add(B, Vector3.new(0.065, 0.8, 0.25), CFrame.new(0, -0.55, 0), "color", 0.06)
            add(B, Vector3.new(0.06, 0.55, 0.17), CFrame.new(0, -1.22, 0), "color", 0.06)
            add(B, Vector3.new(0.055, 0.3, 0.095), CFrame.new(0, -1.65, 0), "color", 0.06)
            add(B, Vector3.new(0.05, 0.17, 0.17), CFrame.new(0, -1.88, 0) * CFrame.Angles(math.rad(45), 0, 0), "white", 0.04)
            local spine = add(B, Vector3.new(0.085, 2.35, 0.045), CFrame.new(0, -0.45, 0), "white", 0.05)

            local a0 = keep(Instance.new("Attachment"))
            a0.Position = Vector3.new(0, 1.0, 0)
            a0.Parent = spine
            local a1 = keep(Instance.new("Attachment"))
            a1.Position = Vector3.new(0, -1.15, 0)
            a1.Parent = spine
            sword.trail = keep(newTrail(a0, a1, fx.folder, {life = 0.55, w0 = 1, w1 = 0.8, t0 = 0.3, t1 = 0.65}))
            sword.sparks = keep(newEmitter(spine, {
                rate = 8, lifeMin = 0.5, lifeMax = 0.9, speedMin = 0.2, speedMax = 0.9, size = 0.09, rot = 120,
                drag = 1, accel = Vector3.new(0, -0.6, 0),
            }))
            fx.swords[i] = sword
        end

        -- Orbs: glowing cores on tilted "atom" orbits with ribbon trails ---
        for i = 1, ORB_COUNT do
            local core = makeFXPart(Enum.PartType.Ball, Vector3.new(0.5, 0.5, 0.5), fx.folder)
            groupAdd("orbs", core, 0)
            local shell = makeFXPart(Enum.PartType.Ball, Vector3.new(1, 1, 1), fx.folder)
            groupAdd("orbs", shell, 0.5)
            local halo = makeFXPart(Enum.PartType.Ball, Vector3.new(1.9, 1.9, 1.9), fx.folder)
            groupAdd("orbs", halo, 0.88)

            local a0 = keep(Instance.new("Attachment"))
            a0.Position = Vector3.new(0, 0.36, 0)
            a0.Parent = core
            local a1 = keep(Instance.new("Attachment"))
            a1.Position = Vector3.new(0, -0.36, 0)
            a1.Parent = core
            local b0 = keep(Instance.new("Attachment"))
            b0.Position = Vector3.new(0.36, 0, 0)
            b0.Parent = core
            local b1 = keep(Instance.new("Attachment"))
            b1.Position = Vector3.new(-0.36, 0, 0)
            b1.Parent = core

            local trail = keep(newTrail(a0, a1, fx.folder, {life = 1.0, w0 = 1, w1 = 0.7, t0 = 0.03, t1 = 0.4}))
            local trail2 = keep(newTrail(b0, b1, fx.folder, {life = 0.7, w0 = 0.7, w1 = 0.4, t0 = 0.12, t1 = 0.5}))

            local glow = keep(Instance.new("PointLight"))
            glow.Brightness = 1.5
            glow.Range = 12
            glow.Shadows = false
            glow.Enabled = false
            glow.Parent = core

            local sparks = keep(newEmitter(core, {
                rate = 14, lifeMin = 0.45, lifeMax = 0.9, speedMin = 0.4, speedMax = 1.6, size = 0.12, rot = 150,
                drag = 1.5,
            }))

            fx.orbs[i] = {
                core = core, shell = shell, halo = halo, trail = trail, trail2 = trail2,
                glow = glow, sparks = sparks,
                phase = (i - 1) * math.pi * 2 / ORB_COUNT,
                yaw = (i - 1) * math.pi * 2 / ORB_COUNT,
                tilt = 1.0,
            }
        end

        -- Halo: ring of beads with two travelling highlights --------------
        for i = 1, HALO_BEADS do
            local u = (((i - 1) / HALO_BEADS) * 2) % 1
            local sz = 0.06 + 0.09 * u ^ 1.5
            local part = makeFXPart(Enum.PartType.Ball, Vector3.new(sz, sz, sz), fx.folder)
            groupAdd("halo", part, 0.62 - 0.56 * u * u)
            fx.halo[i] = {part = part, u = u}
        end
        fx.haloCore = makeFXPart(Enum.PartType.Ball, Vector3.new(0.2, 0.2, 0.2), fx.folder)
        fx.haloSparks = keep(newEmitter(fx.haloCore, {
            rate = 7, lifeMin = 0.7, lifeMax = 1.3, speedMin = 0.1, speedMax = 0.5, size = 0.1, rot = 100,
            drag = 1, accel = Vector3.new(0, -0.8, 0), sphere = true,
        }))

        -- Wings: layered, swept-back feather fans that ripple when flapping
        fx.wingSparks = {}
        for _, side in ipairs({1, -1}) do
            for i, f in ipairs(WING_FEATHERS) do
                local ang, len = f[1], f[2]
                local width = 0.14 + 0.1 * (len / 2.75)
                local main = makeFXPart(Enum.PartType.Block, Vector3.new(len, width, 0.035), fx.folder)
                groupAdd("wings", main, 0.1 + 0.3 * (1 - len / 2.75))
                local cov = makeFXPart(Enum.PartType.Block, Vector3.new(len * 0.55, width * 1.35, 0.03), fx.folder)
                groupAdd("wings", cov, 0.45)
                table.insert(fx.wings, {
                    main = main, cov = cov, side = side, ang = ang, len = len,
                    idx = i, mix = i / #WING_FEATHERS,
                })
                if i == 5 then
                    table.insert(fx.wingSparks, keep(newEmitter(main, {
                        rate = 14, lifeMin = 0.8, lifeMax = 1.5, speedMin = 0.2, speedMax = 0.8, size = 0.14, rot = 120,
                        drag = 1, accel = Vector3.new(0, -1.3, 0),
                    })))
                end
            end
        end

        -- Lightning: attachments on body parts + pooled jagged bolts ------
        for b = 1, BOLT_COUNT do
            local bolt = {glow = {}, core = {}, visible = false, cs = -1}
            for s = 1, BOLT_SEGMENTS do
                bolt.glow[s] = makeFXPart(Enum.PartType.Block, Vector3.new(0.15, 0.15, 0.5), fx.folder)
                bolt.core[s] = makeFXPart(Enum.PartType.Block, Vector3.new(0.05, 0.05, 0.5), fx.folder)
            end
            fx.bolts[b] = bolt
        end

        -- Glitch: chromatic outline flashes on top of the old flicker -----
        local glitchHL = keep(Instance.new("Highlight"))
        glitchHL.Name = "RMEX_Glitch"
        glitchHL.Adornee = character
        glitchHL.DepthMode = Enum.HighlightDepthMode.Occluded
        glitchHL.FillTransparency = 0.78
        glitchHL.OutlineTransparency = 0
        glitchHL.Enabled = false
        glitchHL.Parent = character
        fx.glitchHL = glitchHL

        -- Top hat: translucent cylinder hat. The head is looked up every frame
        -- (the game may replace it after spawn), so only the pieces are built here.
        local function hatAdd(h, d, y, kind, tr)
            local p = makeFXPart(Enum.PartType.Cylinder, Vector3.new(h, d, d), fx.folder)
            p.Material = kind == "band" and Enum.Material.Neon or Enum.Material.SmoothPlastic
            groupAdd("hat", p, tr)
            table.insert(fx.hatParts, {part = p, h = h, d = d, y = y, kind = kind})
        end
        hatAdd(0.12, 2.15, 0.05, "dark", 0.48) -- brim
        hatAdd(1.15, 1.32, 0.68, "dark", 0.5)  -- crown
        hatAdd(0.26, 1.36, 0.25, "band", 0.3)  -- band
        hatAdd(0.07, 1.40, 1.27, "rim", 0.4)   -- top edge

        -- Chinese hat: smooth cone built from thin stacked discs, woven stripes, glowing rim
        do
            local N, R, H = 18, 2.45, 1.15
            for i = 0, N - 1 do
                local f = i / (N - 1)
                local d = R * 2 * (1 - f) ^ 0.95 + 0.14
                local h = H / N * 2.1
                local p = makeFXPart(Enum.PartType.Cylinder, Vector3.new(h, d, d), fx.folder)
                p.Material = Enum.Material.SmoothPlastic
                groupAdd("chat", p, 0.18 + 0.2 * f)
                table.insert(fx.chatParts, {part = p, h = h, d = d, y = H * f ^ 0.8 + 0.04, u = f, i = i, kind = "layer"})
            end
            local rim = makeFXPart(Enum.PartType.Cylinder, Vector3.new(0.07, R * 2 + 0.1, R * 2 + 0.1), fx.folder)
            groupAdd("chat", rim, 0.25)
            table.insert(fx.chatParts, {part = rim, h = 0.07, d = R * 2 + 0.1, y = 0.02, u = 0, i = 0, kind = "rim"})
            local tip = makeFXPart(Enum.PartType.Ball, Vector3.new(0.3, 0.3, 0.3), fx.folder)
            groupAdd("chat", tip, 0.1)
            table.insert(fx.chatParts, {part = tip, h = 0.3, d = 0.3, y = H + 0.1, u = 1, i = 0, kind = "tip"})
        end

        -- Fire: flames on the body parts, embers and smoke
        do
            local F = {flames = {}}
            local names = {"Head", "UpperTorso", "LowerTorso", "Torso", "LeftUpperArm", "RightUpperArm", "Left Arm",
                "Right Arm", "LeftUpperLeg", "RightUpperLeg", "Left Leg", "Right Leg"}
            for _, n in ipairs(names) do
                local part = character:FindFirstChild(n)
                if part and part:IsA("BasePart") then
                    table.insert(F.flames, keep(newEmitter(part, {
                        texture = FIRE_TEX, rate = 14, lifeMin = 0.5, lifeMax = 0.9, speedMin = 1, speedMax = 3,
                        size = 1.3, rot = 70, drag = 1, accel = Vector3.new(0, 5, 0), emission = 1,
                        spread = Vector2.new(25, 25), top = true, startScale = 0.6, endSize = 0.15, t0 = 0.25, t1 = 0.55,
                    })))
                end
            end
            F.embers = keep(newEmitter(root, {
                rate = 20, lifeMin = 0.8, lifeMax = 1.6, speedMin = 1, speedMax = 4, size = 0.14, rot = 90,
                drag = 0.5, accel = Vector3.new(0, 4, 0), sphere = true, t0 = 0, t1 = 0.3,
            }))
            F.smoke = keep(newEmitter(root, {
                texture = SMOKE_TEX, rate = 10, lifeMin = 1, lifeMax = 1.8, speedMin = 0.6, speedMax = 1.6, size = 2,
                startScale = 0.4, endSize = 3.5, rot = 25, drag = 0.8, accel = Vector3.new(0, 3, 0), emission = 0.2,
                spread = Vector2.new(30, 30), top = true, t0 = 0.6, t1 = 0.85,
            }))
            F.light = keep(Instance.new("PointLight"))
            F.light.Range = 10
            F.light.Brightness = 1.2
            F.light.Shadows = false
            F.light.Enabled = false
            F.light.Parent = root
            fx.fire = F
        end

        -- Petals / snow, smoke, crystals, rune circle
        do
            local layers = {}
            local ks, rks, hs = {1, 2, 4}, {8, 12, 20}, {15, 25, 40}
            for i, area in ipairs({60, 250, 1000}) do
                local pp = makeFXPart(Enum.PartType.Block, Vector3.new(area, 0.2, area), fx.folder)
                local pe = keep(newEmitter(pp, {
                    rate = 14, lifeMin = 5, lifeMax = 8, speedMin = 0.3, speedMax = 1, size = 0.5, rot = 180, drag = 0.5,
                    accel = Vector3.new(0, -3, 0), emission = 0.3, spread = Vector2.new(25, 25), t0 = 0.05, t1 = 0.2,
                }))
                pe.EmissionDirection = Enum.NormalId.Bottom
                layers[i] = {part = pp, em = pe, k = ks[i], rk = rks[i], h = hs[i]}
            end
            fx.petal = {layers = layers}

            for i = 1, 4 do
                local handle = makeFXPart(Enum.PartType.Cylinder, Vector3.new(0.9, 0.22, 0.22), fx.folder)
                handle.Material = Enum.Material.Metal
                handle.Color = Color3.fromRGB(70, 72, 80)
                groupAdd("saber", handle, 0)
                local blade = makeFXPart(Enum.PartType.Cylinder, Vector3.new(4.2, 0.24, 0.24), fx.folder)
                blade.Material = Enum.Material.Neon
                groupAdd("saber", blade, 0.25)
                local core = makeFXPart(Enum.PartType.Cylinder, Vector3.new(4.2, 0.1, 0.1), fx.folder)
                core.Material = Enum.Material.Neon
                core.Color = Color3.new(1, 1, 1)
                groupAdd("saber", core, 0)
                table.insert(fx.saberParts, {handle = handle, blade = blade, core = core, i = i})
            end

            fx.smk = keep(newEmitter(root, {
                texture = SMOKE_TEX, rate = 18, lifeMin = 1.2, lifeMax = 2.2, speedMin = 1, speedMax = 2.5, size = 2.6,
                startScale = 0.5, endSize = 4, rot = 30, drag = 1, accel = Vector3.new(0, 1, 0), emission = 0,
                sphere = true, t0 = 0.35, t1 = 0.75,
            }))

            for i = 1, 8 do
                local p = makeFXPart(Enum.PartType.Block, Vector3.new(0.28, 1.1, 0.28), fx.folder)
                groupAdd("crys", p, 0.2)
                table.insert(fx.crysParts, {part = p, i = i})
            end

            local R = 3.0
            local disc = makeFXPart(Enum.PartType.Cylinder, Vector3.new(0.05, R * 2.3, R * 2.3), fx.folder)
            groupAdd("rune", disc, 0.8)
            table.insert(fx.runeParts, {part = disc, ox = 0, oz = 0, yaw = 0, layer = 1, sx = 0.05, sy = R * 2.3, sz = R * 2.3, cyl = true})
            for k = 0, 11 do
                local a = k / 12 * math.pi * 2
                local p = makeFXPart(Enum.PartType.Block, Vector3.new(0.35, 0.06, 0.9), fx.folder)
                groupAdd("rune", p, 0.15)
                table.insert(fx.runeParts, {part = p, ox = math.cos(a) * R * 1.05, oz = math.sin(a) * R * 1.05,
                    yaw = math.pi / 2 - a, layer = 1, sx = 0.35, sy = 0.06, sz = 0.9})
            end
            for k = 0, 5 do
                local a = k / 6 * math.pi * 2 + math.pi / 6
                local p = makeFXPart(Enum.PartType.Block, Vector3.new(R * 1.732, 0.06, 0.16), fx.folder)
                groupAdd("rune", p, 0.2)
                table.insert(fx.runeParts, {part = p, ox = math.cos(a) * R * 0.5, oz = math.sin(a) * R * 0.5,
                    yaw = -a - math.pi / 2, layer = 2, sx = R * 1.732, sy = 0.06, sz = 0.16})
            end
        end

        -- Wind: thin ribbons spiralling around the body -------------------
        for i = 1, WIND_COUNT do
            local part = makeFXPart(Enum.PartType.Ball, Vector3.new(0.2, 0.2, 0.2), fx.folder)
            local a0 = keep(Instance.new("Attachment"))
            a0.Position = Vector3.new(0, 0.045, 0)
            a0.Parent = part
            local a1 = keep(Instance.new("Attachment"))
            a1.Position = Vector3.new(0, -0.045, 0)
            a1.Parent = part
            local trail = keep(newTrail(a0, a1, fx.folder, {life = 0.9, w0 = 1, w1 = 0.8, t0 = 0.12, t1 = 0.5}))
            fx.wind[i] = {
                part = part, trail = trail,
                phase = (i - 1) * math.pi * 2 / WIND_COUNT,
                speed = 2.4 + (i % 4) * 0.45,
                radius = 2.0 + (i % 3) * 0.5,
                y = -1.3 + (i - 1) / (WIND_COUNT - 1) * 3.0,
                wob = 0.6 + (i % 5) * 0.15,
            }
        end

        -- Space streaks: small thin streaks drifting through the whole area
        for i = 1, STREAK_COUNT do
            local part = makeFXPart(Enum.PartType.Ball, Vector3.new(0.1, 0.1, 0.1), fx.folder)
            local a0 = keep(Instance.new("Attachment"))
            a0.Position = Vector3.new(0, 0.05, 0)
            a0.Parent = part
            local a1 = keep(Instance.new("Attachment"))
            a1.Position = Vector3.new(0, -0.05, 0)
            a1.Parent = part
            local trail = keep(newTrail(a0, a1, fx.folder, {
                life = 0.3 + (i % 5) * 0.06, w0 = 1, w1 = 0.6, t0 = 0.2, t1 = 0.65,
            }))
            fx.streaks[i] = {part = part, trail = trail, pos = Vector3.zero, vel = Vector3.zero, phase = 0, wait = 0}
        end

        -- Lagging bot: translucent copy that replays our pose with a delay.
        -- The copy itself is (re)built lazily from the live character, see rebuildGhost.
        local ghost = {entries = {}, hist = {}, idx = 0, count = 0, lastRec = 0, wasOn = false,
            shownAlpha = -1, sig = nil, model = nil}
        for h = 1, GHOST_HISTORY do
            ghost.hist[h] = {t = 0, root = CFrame.identity, cfs = {}}
        end
        fx.ghost = ghost

        -- Distant lightning pool (positioned once per strike)
        local far = {slots = {}, active = false, wasOn = false, nextAt = 0, t0 = 0, used = 0, power = 0.1}
        for i = 1, FAR.main + FAR.branches * FAR.bseg do
            far.slots[i] = {
                glow = makeFXPart(Enum.PartType.Block, Vector3.new(1, 1, 1), fx.folder),
                core = makeFXPart(Enum.PartType.Block, Vector3.new(1, 1, 1), fx.folder),
            }
        end
        far.flare = makeFXPart(Enum.PartType.Ball, Vector3.new(1, 1, 1), fx.folder)
        fx.far = far
        task.defer(prewarmPools)

        -- Jump / landing bursts ------------------------------------------
        table.insert(fx.conns, humanoid.StateChanged:Connect(function(_, new)
            if not (visual.Master and visual.Jumps) then return end
            local C = visual.cfg.Jumps
            local mode = C.Anim == 2 and "ring" or (C.Anim == 3 and "sparks" or nil)
            local col = C.Color or getEffectColor()
            if new == Enum.HumanoidStateType.Jumping then
                spawnBurst(12, col, 5.5 * C.Size, mode)
            elseif new == Enum.HumanoidStateType.Landed then
                spawnBurst(30, col, 10 * C.Size, mode)
            end
        end))

        fx.root = root
        fx.humanoid = humanoid
        fx.character = character
        refreshBody()
    end

    ----------------------------------------------------------------------
    -- UPDATE
    ----------------------------------------------------------------------

    updateEffects = function(dt)
        if not fx.character or not fx.root or not fx.root.Parent or not fx.aura or not fx.ghost or not fx.shell or not fx.far then return end
        local root = fx.root
        local on = visual.Master
        local t = os.clock()
        local color = getEffectColor()
        if fx.lastColor ~= color then
            fx.lastColor = color
            fx.cs += 1
            fx.glow = glowSeq(color)
            fx.soft = softSeq(color)
        end
        local glow, soft = fx.glow, fx.soft
        local rpos = root.Position

        -- Appearance tracking: rebuild the bot / aura shell when the skin changes
        local head = fx.character:FindFirstChild("Head")
        local camNear = false -- first person / camera glued to the head: keep the view clear
        if head and head:IsA("BasePart") then
            local cam = getCam()
            camNear = head.LocalTransparencyModifier > 0.95
                or (cam ~= nil and (cam.CFrame.Position - head.Position).Magnitude < 1.0)
        else
            head = nil
        end
        if on and (visual.Aura or visual.Ghost) then
            fx.sigAcc += dt
            if fx.sigAcc >= 0.35 or not fx.sig then
                fx.sigAcc = 0
                fx.sig = Rep.sig(fx.character)
            end
        end

        -- Aura: strong outline + soft light + mist + glowing body shell ----
        do local C, t, color, glow, soft = FXC("Aura", dt)
        local auraOn = on and visual.Aura
        fx.aura.Enabled = auraOn
        fx.light.Enabled = auraOn
        fx.mist.Enabled = auraOn
        local inten = C.Intensity / 100
        local pulse
        if C.Anim == 2 then
            pulse = 0.5 + 0.5 * math.sin(t * 0.9)
        elseif C.Anim == 3 then
            pulse = math.clamp(0.5 + 1.4 * math.noise(t * 5, 3.7), 0, 1)
        else
            pulse = 0.5 + 0.5 * math.sin(t * 2.2)
        end
        if auraOn then
            local lv = 0.65 + 0.35 * pulse
            fx.aura.FillColor = color
            fx.aura.OutlineColor = color:Lerp(WHITE, 0.12 * pulse)
            fx.aura.FillTransparency = 1 - 0.16 * inten * lv
            fx.aura.OutlineTransparency = 0.92 - 0.8 * inten * lv
            fx.light.Color = color
            fx.light.Brightness = 0.2 + 0.9 * inten * lv
            fx.light.Range = (6 + 3 * pulse) * C.Size
            tune(fx.mist, C.Size, C.Speed, 1)
            if stale("aura") then fx.mist.Color = soft end
        end

        local shell = fx.shell
        if auraOn and not camNear then
            if shell.sig ~= fx.sig then rebuildShell() end
            local tr = math.floor((0.97 - 0.3 * inten * (0.65 + 0.35 * pulse)) * 50 + 0.5) / 50
            local recolor = stale("shell")
            if shell.fresh then
                recolor = true
                shell.fresh = false
            end
            local retint = shell.tr ~= tr
            for _, e in ipairs(shell.entries) do
                if e.src.Parent then pushMove(e.part, e.src.CFrame) end
                if retint then e.part.Transparency = tr end
                if recolor then e.part.Color = color end
            end
            shell.tr = tr
            shell.shown = true
        elseif shell.shown then
            shell.shown = false
            shell.tr = nil
            for _, e in ipairs(shell.entries) do e.part.Transparency = 1 end
        end

        end
        -- Particles ------------------------------------------------------
        do local C, t, color, glow, soft = FXC("Particles", dt)
        local particlesOn = on and visual.Particles
        for _, e in ipairs(fx.emitters) do
            e.Enabled = particlesOn
            tune(e, C.Size, C.Speed, C.Anim)
        end
        if particlesOn and stale("particles") then
            for _, e in ipairs(fx.emitters) do e.Color = glow end
        end

        end
        -- Trails ---------------------------------------------------------
        do local C, t, color, glow, soft = FXC("Trails", dt)
        local trailsOn = on and visual.Trails
        fx.trail.Enabled = trailsOn
        tuneTrail(fx.trail, C.Size, C.Speed)
        tuneTrail(fx.trailCore, C.Size, C.Speed)
        fx.trailCore.Enabled = trailsOn
        if trailsOn and stale("trails") then
            fx.trail.Color = glow
            fx.trailCore.Color = ColorSequence.new(coreOf(color))
        end

        end
        -- Rings ----------------------------------------------------------
        do local C, t, color, glow, soft = FXC("Rings", dt)
        local ringsOn = on and visual.Rings
        showGroup("rings", ringsOn)
        if ringsOn then
            local recolor = stale("rings")
            for ri, ring in ipairs(RINGS) do
                local sign = ring.speed >= 0 and 1 or -1
                local tx, tz, ry = ring.tx, ring.tz, ring.y
                if C.Anim == 2 then
                    tx, tz, ry = 0, 0, ring.y * 1.5
                elseif C.Anim == 3 then
                    tx, tz = tx + t * 0.35 * ri, tz + t * 0.45
                end
                local base = CFrame.new(rpos + Vector3.new(0, ry, 0))
                    * CFrame.Angles(tx + math.sin(t * 0.6 + ri) * 0.07, t * 0.12 * ri, tz + math.cos(t * 0.5 + ri) * 0.07)
                for seg, item in ipairs(fx.rings[ri]) do
                    local angle = sign * (seg / RING_SEGMENTS) * math.pi * 2 + t * ring.speed
                    pushMove(item.part, base * CFrame.new(math.cos(angle) * ring.radius * C.Size, 0, math.sin(angle) * ring.radius * C.Size))
                    if recolor then
                        item.part.Color = color:Lerp(WHITE, item.u * item.u * 0.7)
                    end
                end
            end
        end

        end
        -- Orbs -----------------------------------------------------------
        do local C, t, color, glow, soft = FXC("Orbs", dt)
        local orbsOn = on and visual.Orbs
        showGroup("orbs", orbsOn)
        local orbRecolor = orbsOn and stale("orbs")
        for _, orb in ipairs(fx.orbs) do
            orb.glow.Enabled = orbsOn
            orb.trail.Enabled = orbsOn
            orb.trail2.Enabled = orbsOn
            orb.sparks.Enabled = orbsOn
            if orbRecolor then
                orb.core.Color = coreOf(color)
                orb.shell.Color = color
                orb.halo.Color = color
                orb.glow.Color = color
                orb.trail.Color = glow
                orb.trail2.Color = glow
                orb.sparks.Color = glow
            end
            if orbsOn then
                local a = t * 0.85 + orb.phase
                local radius = (3.0 + math.sin(t * 0.7 + orb.phase) * 0.22) * C.Size
                if C.Anim == 3 then radius = radius * (1 + 0.3 * math.sin(t * 1.6)) end
                local tiltA = C.Anim == 2 and 0.15 or orb.tilt
                local plane = CFrame.Angles(0, orb.yaw + t * (C.Anim == 2 and 0.5 or 0.22), 0) * CFrame.Angles(tiltA, 0, 0)
                local pos = rpos + Vector3.new(0, 0.2, 0)
                    + plane * Vector3.new(math.cos(a) * radius, 0, math.sin(a) * radius)
                pushMove(orb.core, CFrame.new(pos) * CFrame.Angles(t * 1.1 + orb.phase, t * 0.7, 0))
                pushMove(orb.shell, CFrame.new(pos))
                pushMove(orb.halo, CFrame.new(pos))
                local pulse = math.sin(t * 3.1 + orb.phase)
                local s = 1.0 + pulse * 0.1
                orb.shell.Size = Vector3.new(s, s, s)
                local h = 1.9 + math.sin(t * 2.2 + orb.phase * 1.7) * 0.22
                orb.halo.Size = Vector3.new(h, h, h)
                orb.glow.Brightness = 1.4 + pulse * 0.4
            end
        end

        end
        -- Swords ---------------------------------------------------------
        do local C, t, color, glow, soft = FXC("Swords", dt)
        local swordsOn = on and visual.Swords
        showGroup("swords", swordsOn)
        local swordRecolor = swordsOn and stale("swords")
        for _, sw in ipairs(fx.swords) do
            sw.trail.Enabled = swordsOn
            sw.sparks.Enabled = swordsOn
            if swordRecolor then
                sw.trail.Color = glow
                sw.sparks.Color = glow
                for _, item in ipairs(sw.parts) do
                    item.part.Color = swordPartColor(item.kind, color)
                end
            end
            if swordsOn then
                local a = (C.Anim == 2 and -t * 1.6 or t * 1.0) + sw.phase
                local radius = (2.5 + math.sin(t * 1.2 + sw.phase * 2) * 0.1) * C.Size
                if C.Anim == 3 then radius = radius * (1 + 0.3 * math.sin(t * 1.8)) end
                local y = 0.3 + math.sin(t * 1.5 + sw.phase * 2) * 0.22
                local pos = rpos + Vector3.new(math.cos(a) * radius, y, math.sin(a) * radius)
                local base = CFrame.new(pos) * CFrame.Angles(0, -a, 0)
                    * CFrame.Angles(math.sin(t * 1.3 + sw.phase) * 0.07, 0, 0.2 + math.sin(t * 1.7 + sw.phase) * 0.05)
                for _, item in ipairs(sw.parts) do
                    pushMove(item.part, base * item.off)
                end
            end
        end

        end
        -- Halo -----------------------------------------------------------
        do local C, t, color, glow, soft = FXC("Halo", dt)
        local haloOn = on and visual.Halo
        showGroup("halo", haloOn)
        fx.haloSparks.Enabled = haloOn
        if haloOn then
            local recolor = stale("halo")
            local wob = C.Anim == 2 and 0.35 or 0.1
            local base = CFrame.new(rpos + Vector3.new(0, 3.05 + math.sin(t * 1.8) * (C.Anim == 2 and 0.25 or 0.1), 0))
                * CFrame.Angles(math.sin(t * 1.3) * wob, 0, math.cos(t * 1.1) * wob)
            local hr = 0.9 * C.Size * (C.Anim == 3 and (1 + 0.25 * math.sin(t * 3)) or 1)
            for i, bead in ipairs(fx.halo) do
                local ang = (i / HALO_BEADS) * math.pi * 2 + t * (C.Anim == 3 and 3.2 or 1.9)
                pushMove(bead.part, base * CFrame.new(math.cos(ang) * hr, 0, math.sin(ang) * hr))
                if recolor then
                    bead.part.Color = color:Lerp(WHITE, bead.u * bead.u * 0.75)
                end
            end
            pushMove(fx.haloCore, base)
            if recolor then fx.haloSparks.Color = glow end
        end

        end
        -- Wings ----------------------------------------------------------
        do local C, t, color, glow, soft = FXC("Wings", dt)
        local wingsOn = on and visual.Wings
        showGroup("wings", wingsOn)
        for _, s in ipairs(fx.wingSparks) do s.Enabled = wingsOn end
        if wingsOn then
            local airborne = fx.humanoid and fx.humanoid.FloorMaterial == Enum.Material.Air
            local v = root.AssemblyLinearVelocity
            local spd = Vector3.new(v.X, 0, v.Z).Magnitude
            local ampT = airborne and 0.34 or (spd > 3 and 0.16 or 0.09)
            local spdT = airborne and 6.5 or (spd > 3 and 3.2 or 2.0)
            if C.Anim == 2 then ampT, spdT = ampT * 0.5, spdT * 0.5
            elseif C.Anim == 3 then ampT, spdT = ampT * 0.55, spdT * 2.6 end
            local k = 1 - math.exp(-dt * 4)
            fx.wingAmp += (ampT - fx.wingAmp) * k
            fx.wingSpeed += (spdT - fx.wingSpeed) * k
            fx.wingPhase += dt * fx.wingSpeed * C.Speed
            local recolor = stale("wings")
            local rootCF = root.CFrame
            for _, w in ipairs(fx.wings) do
                local pivot = rootCF * CFrame.new(w.side * 0.4, 0.9, 0.5) * CFrame.Angles(0, -w.side * 0.4, 0)
                local flap = math.sin(fx.wingPhase - w.idx * 0.28) * fx.wingAmp * (0.35 + 0.65 * w.mix) + 0.04
                pushMove(w.main,
                    pivot * CFrame.Angles(0, 0, w.side * (w.ang + flap)) * CFrame.new(w.side * w.len / 2, 0, 0))
                pushMove(w.cov,
                    pivot * CFrame.Angles(0, 0, w.side * (w.ang + flap * 0.8 + 0.1))
                        * CFrame.new(w.side * (w.len * 0.55 / 2 + 0.12), 0, 0.02))
                if recolor then
                    local c = shiftHue(color, 0.09 * (1 - w.mix), 0, 0):Lerp(WHITE, 0.12 + 0.2 * w.mix)
                    w.main.Color = c
                    w.cov.Color = c:Lerp(WHITE, 0.35)
                end
            end
            if recolor then
                for _, s in ipairs(fx.wingSparks) do s.Color = glow end
            end
        end

        end
        -- Lightning ------------------------------------------------------
        do local C, t, color, glow, soft = FXC("Lightning", dt)
        local lightOn = on and visual.Lightning
        fx.boltW = C.Size
        if lightOn or (on and visual.Glitch) then
            fx.bodyAcc = (fx.bodyAcc or 0) + dt
            if fx.bodyAcc >= 0.5 then
                fx.bodyAcc = 0
                refreshBody()
            end
        end
        if lightOn and #fx.attachments >= 2 then
            fx.lightAcc += dt
            if fx.lightAcc >= 0.06 / C.Speed then
                fx.lightAcc = 0
                fx.boltsShown = true
                for _, bolt in ipairs(fx.bolts) do
                    local alive = math.random() < 0.72
                    if alive then
                        local p0 = fx.attachments[math.random(#fx.attachments)].WorldPosition
                        local p1
                        if C.Anim == 2 then
                            p0 = rpos
                            local d = Vector3.new(math.random() - 0.5, math.random() - 0.4, math.random() - 0.5)
                            p1 = rpos + (d.Magnitude > 0.05 and d.Unit or Vector3.yAxis) * (2.6 + math.random() * 1.6)
                        elseif C.Anim == 3 then
                            p0 = head and head.Position or rpos
                            p1 = p0 + Vector3.new((math.random() - 0.5) * 3, 1.5 + math.random() * 2.5, (math.random() - 0.5) * 3)
                        elseif math.random() < 0.4 then
                            local d = Vector3.new(math.random() - 0.5, math.random() - 0.35, math.random() - 0.5)
                            if d.Magnitude < 0.05 then d = Vector3.yAxis end
                            p1 = rpos + d.Unit * (2.4 + math.random() * 1.4)
                        else
                            p1 = fx.attachments[math.random(#fx.attachments)].WorldPosition
                        end
                        alive = layoutBolt(bolt, p0, p1, color)
                    end
                    if not alive then hideBolt(bolt) end
                end
            end
        elseif fx.boltsShown then
            fx.boltsShown = false
            for _, bolt in ipairs(fx.bolts) do hideBolt(bolt) end
        end

        end
        -- Glitch ---------------------------------------------------------
        do local C, t, color, glow, soft = FXC("Glitch", dt)
        local glitchOn = on and visual.Glitch
        if glitchOn then
            fx.glitchAcc += dt
            if fx.glitchAcc >= 0.07 / C.Speed then
                fx.glitchAcc = 0
                for _, part in ipairs(fx.bodyParts) do
                    part.LocalTransparencyModifier = 0
                end
                local r = math.random()
                if C.Anim == 1 and r < 0.4 and #fx.bodyParts > 0 then
                    fx.bodyParts[math.random(#fx.bodyParts)].LocalTransparencyModifier = 0.6 + math.random() * 0.3
                end
                if r < (C.Anim == 2 and 0.5 or 0.28) then
                    local c = (math.random() < 0.5) and color or shiftHue(color, 0.5, 0, 0)
                    fx.glitchHL.FillColor = c
                    fx.glitchHL.OutlineColor = c:Lerp(WHITE, 0.35)
                    fx.glitchHL.Enabled = true
                else
                    fx.glitchHL.Enabled = false
                end
                fx.glitching = true
            end
        elseif fx.glitching then
            fx.glitching = false
            fx.glitchHL.Enabled = false
            for _, part in ipairs(fx.bodyParts) do
                part.LocalTransparencyModifier = 0
            end
        end

        end
        -- Top hat -------------------------------------------------------
        do local C, t, color, glow, soft = FXC("Hat", dt)
        local hatOn = on and visual.Hat and head ~= nil and not camNear
        showGroup("hat", hatOn)
        if hatOn then
            local k = math.clamp(math.min(head.Size.X, head.Size.Z) / 1.2, 0.7, 1.6) * C.Size
            local resize = fx.hatK == nil or math.abs(k - fx.hatK) > 0.01
            fx.hatK = k
            local recolor = stale("hat")
            local bob = C.Anim == 2 and math.sin(t * 2.5) * 0.18 or 0
            local sway = C.Anim == 3 and CFrame.Angles(math.sin(t * 1.6) * 0.12, 0, math.cos(t * 1.3) * 0.12) or CFrame.identity
            local base = head.CFrame * CFrame.new(0, head.Size.Y / 2 + bob, 0) * sway
            for _, item in ipairs(fx.hatParts) do
                if resize then item.part.Size = Vector3.new(item.h * k, item.d * k, item.d * k) end
                pushMove(item.part, base * CFrame.new(0, item.y * k, 0) * CFrame.Angles(0, 0, math.rad(90)))
                if recolor then item.part.Color = hatColor(item.kind, color) end
            end
        end

        end
        -- Chinese hat ---------------------------------------------------
        do local C, t, color, glow, soft = FXC("ChineseHat", dt)
        local chatOn = on and visual.ChineseHat and head ~= nil and not camNear
        showGroup("chat", chatOn)
        if chatOn then
            local k = math.clamp(math.min(head.Size.X, head.Size.Z) / 1.2, 0.7, 1.6) * C.Size
            local resize = fx.chatK == nil or math.abs(k - fx.chatK) > 0.01
            fx.chatK = k
            local shimmer = C.Anim == 4
            local recolor = shimmer or stale("chinesehat")
            local tilt = CFrame.identity
            local bob = 0
            if C.Anim == 2 then
                tilt = CFrame.Angles(math.sin(t * 1.5) * 0.09, 0, math.cos(t * 1.2) * 0.09)
            elseif C.Anim == 3 then
                bob = math.sin(t * 2.2) * 0.14
                tilt = CFrame.Angles(math.sin(t * 0.8) * 0.04, 0, 0)
            end
            local base = head.CFrame * CFrame.new(0, head.Size.Y / 2 - 0.05 + bob * k, 0) * tilt
            for _, item in ipairs(fx.chatParts) do
                if resize then item.part.Size = Vector3.new(item.h * k, item.d * k, item.d * k) end
                pushMove(item.part, base * CFrame.new(0, item.y * k, 0) * CFrame.Angles(0, 0, math.rad(90)))
                if recolor then
                    local c = chatColor(item, color)
                    if shimmer then c = c:Lerp(WHITE, 0.6 * math.max(0, math.sin(t * 3.2 - item.u * 7))) end
                    item.part.Color = c
                end
            end
        end

        end
        -- Fire ----------------------------------------------------------
        do local C, t, color, glow, soft = FXC("Fire", dt)
        local F = fx.fire
        if F then
            local fireOn = on and visual.Fire
            local m = FIRE[C.Anim]
            for _, e in ipairs(F.flames) do
                e.Enabled = fireOn
                if fireOn then
                    tuneSize(e, C.Size, C.Speed)
                    if F.mode ~= C.Anim then
                        e.Rate = m.rate
                        e.Lifetime = NumberRange.new(m.lmin, m.lmax)
                        e.Speed = NumberRange.new(m.v1, m.v2)
                        e.Acceleration = Vector3.new(0, m.ac, 0)
                    end
                end
            end
            F.embers.Enabled = fireOn
            F.smoke.Enabled = fireOn and m.smoke > 0
            F.light.Enabled = fireOn
            if fireOn then
                tuneSize(F.embers, C.Size, C.Speed)
                tuneSize(F.smoke, C.Size, C.Speed)
                if F.mode ~= C.Anim then
                    F.embers.Rate = m.ember
                    F.smoke.Rate = math.max(m.smoke, 1)
                    F.mode = C.Anim
                end
                if stale("fire") then
                    for _, e in ipairs(F.flames) do e.Color = glow end
                    F.embers.Color = glow
                    F.smoke.Color = ColorSequence.new(Color3.fromRGB(60, 55, 55):Lerp(color, 0.15))
                end
                F.light.Color = color
                F.light.Range = 9 * C.Size
                F.light.Brightness = 1.1 + 0.5 * math.noise(t * 6, 1.3)
            end
        end

        end
        -- Petals ---------------------------------------------------------
        do
            local C, t, color = FXC("Petals", dt)
            local P = fx.petal
            if P then
                local pOn = on and visual.Petals
                local m = PET[C.Anim]
                local recolor = pOn and stale("petals")
                local modeChanged = P.mode ~= C.Anim
                if pOn then P.mode = C.Anim end
                for _, L in ipairs(P.layers) do
                    L.em.Enabled = pOn
                    if pOn then
                        tuneSize(L.em, C.Size * m.sz * L.k, C.Speed)
                        if modeChanged then
                            L.em.Rate = m.rate * L.rk
                            L.em.Lifetime = NumberRange.new(m.l1 * 1.8, m.l2 * 1.8)
                            L.em.Speed = NumberRange.new(m.v1, m.v2)
                            L.em.Acceleration = Vector3.new(0, m.ac, 0)
                        end
                        if recolor then L.em.Color = ColorSequence.new(color) end
                        pushMove(L.part, CFrame.new(rpos + Vector3.new(0, C.Anim == 3 and -1 or L.h, 0)))
                    end
                end
            end
        end

        -- Smoke -----------------------------------------------------------
        do
            local C, t, color = FXC("Smoke", dt)
            local e = fx.smk
            if e then
                local sOn = on and visual.Smoke
                e.Enabled = sOn
                if sOn then
                    local m = SMK[C.Anim]
                    tuneSize(e, C.Size * m.sz, C.Speed)
                    if fx.smkMode ~= C.Anim then
                        fx.smkMode = C.Anim
                        e.Rate = m.rate
                        e.Lifetime = NumberRange.new(m.l1, m.l2)
                        e.Speed = NumberRange.new(m.v1, m.v2)
                        e.Acceleration = Vector3.new(0, m.ac, 0)
                    end
                    if stale("smoke") then e.Color = ColorSequence.new(color) end
                end
            end
        end

        -- Crystals --------------------------------------------------------
        do
            local C, t, color = FXC("Crystals", dt)
            local cOn = on and visual.Crystals
            showGroup("crys", cOn)
            if cOn then
                local recolor = stale("crystals")
                local n = #fx.crysParts
                for _, it in ipairs(fx.crysParts) do
                    local a = t * (C.Anim == 2 and 0.5 or 1.3) + it.i / n * math.pi * 2
                    local r = (C.Anim == 2 and 2.7 or 3.2) * C.Size
                    local y = 0.2
                    if C.Anim == 2 then
                        y = (it.i % 2 == 0) and 1.0 or -0.6
                    elseif C.Anim == 3 then
                        y = ((t * 0.35 + it.i / n) % 1) * 4 - 2
                        r = 2.8 * C.Size
                    end
                    local pos = rpos + Vector3.new(math.cos(a) * r, y + math.sin(t * 2 + it.i) * 0.12, math.sin(a) * r)
                    pushMove(it.part, CFrame.new(pos) * CFrame.Angles(0, -a, 0) * CFrame.Angles(0, 0, math.rad(25)))
                    if recolor then it.part.Color = lw(color, 0.3) end
                end
            end
        end

        -- Runes -----------------------------------------------------------
        do
            local C, t, color = FXC("Runes", dt)
            local rOn = on and visual.Runes
            showGroup("rune", rOn)
            if rOn then
                local gp = groundPoint(10) or (rpos - Vector3.new(0, 3, 0))
                local k = C.Size * (C.Anim == 3 and (1 + 0.12 * math.sin(t * 2.5)) or 1)
                local resize = fx.runeK == nil or math.abs(k - fx.runeK) > 0.005
                fx.runeK = k
                local recolor = stale("runes")
                local rise = C.Anim == 3 and 0.05 * math.sin(t * 2.5) or 0
                for _, it in ipairs(fx.runeParts) do
                    if resize then
                        it.part.Size = it.cyl and Vector3.new(it.sx, it.sy * k, it.sz * k)
                            or Vector3.new(it.sx * k, it.sy, it.sz * k)
                    end
                    local rot = (it.layer == 2 and C.Anim == 2) and -t * 0.9 or t * 0.5
                    pushMove(it.part, CFrame.new(gp + Vector3.new(0, 0.1 + rise, 0)) * CFrame.Angles(0, rot, 0)
                        * CFrame.new(it.ox * k, 0, it.oz * k) * CFrame.Angles(0, it.yaw, 0)
                        * (it.cyl and CFrame.Angles(0, 0, math.rad(90)) or CFrame.identity))
                    if recolor then it.part.Color = it.layer == 1 and color:Lerp(DARK, 0.15) or color end
                end
            end
        end

        -- Lightsabers -----------------------------------------------------
        do
            local C, t, color = FXC("Sabers", dt)
            local sOn = on and visual.Sabers
            showGroup("saber", sOn)
            if sOn then
                local k = C.Size
                local L = 4.2 * k
                local resize = fx.saberK ~= k
                fx.saberK = k
                local recolor = stale("sabers")
                local n = #fx.saberParts
                for _, it in ipairs(fx.saberParts) do
                    local ph = it.i / n * math.pi * 2
                    local S
                    if C.Anim == 1 then
                        local a = t * 1.5 + ph
                        S = CFrame.new(rpos + Vector3.new(math.cos(a) * 3.2 * k, 0.3 + math.sin(t * 2 + ph) * 0.3, math.sin(a) * 3.2 * k))
                            * CFrame.Angles(0, -a - math.pi / 2, 0)
                    elseif C.Anim == 2 then
                        local a = t * 0.8 + ph
                        S = CFrame.new(rpos + Vector3.new(math.cos(a) * 3.4 * k, 0.4, math.sin(a) * 3.4 * k))
                            * CFrame.Angles(0, -a, t * 7 + ph)
                    elseif C.Anim == 3 then
                        local a = t * 2 + ph
                        local base = CFrame.Angles(0, t * 0.3, 0)
                        local rv = base:VectorToWorldSpace(Vector3.new(0, math.cos(a), math.sin(a)))
                        S = CFrame.fromMatrix(rpos + rv * 3 * k, rv, base.RightVector)
                    else
                        local side = (it.i % 2 == 0) and 1 or -1
                        local row = it.i <= 2 and 0 or 1
                        local hold = CFrame.new(rpos) * fx.root.CFrame.Rotation
                        S = hold * CFrame.new(side * (1.2 + row * 1.2) * k, 1.2 + row * 0.9 + math.sin(t * 2.2 + ph) * 0.2, 2.2 + row * 0.4)
                            * CFrame.Angles(0, 0, side * (math.rad(50) + math.sin(t * 1.5 + ph) * 0.12))
                    end
                    pushMove(it.handle, S * CFrame.new(-L / 2 - 0.05, 0, 0))
                    pushMove(it.blade, S * CFrame.new(0.5, 0, 0))
                    pushMove(it.core, S * CFrame.new(0.5, 0, 0))
                    if resize then
                        it.blade.Size = Vector3.new(L, 0.24, 0.24)
                        it.core.Size = Vector3.new(L, 0.1, 0.1)
                    end
                    if recolor then it.blade.Color = color end
                end
            end
        end

        -- Pulse rings -----------------------------------------------------
        do
            local C, t, color = FXC("Pulse", dt)
            if on and visual.Pulse then
                fx.pulseAcc = (fx.pulseAcc or 0) + dt
                if fx.pulseAcc >= 0.8 / C.Speed then
                    fx.pulseAcc = 0
                    spawnStep(color, C.Size * (C.Anim == 3 and 2.6 or 1.4), C.Anim == 2 and 2 or 1)
                end
            end
        end

        -- Wind streaks around the body ------------------------------------
        do local C, t, color, glow, soft = FXC("Wind", dt)
        local windOn = on and visual.Wind
        local windRecolor = windOn and stale("wind")
        for _, w in ipairs(fx.wind) do
            w.trail.Enabled = windOn
            if windRecolor then w.trail.Color = glow end
            local a = t * w.speed + w.phase
            if C.Anim == 3 then a = -a end
            local r = (w.radius + math.sin(t * 1.1 + w.phase * 2) * 0.35) * C.Size * (C.Anim == 3 and 1.35 or 1)
            local y = w.y + math.sin(t * w.wob + w.phase) * 0.5 + math.sin(a * 0.5) * 0.18
            if C.Anim == 2 then y = ((t * 0.7 + w.phase / 6.28) % 1) * 3.4 - 1.6 end
            pushMove(w.part, CFrame.new(rpos + Vector3.new(math.cos(a) * r, y, math.sin(a) * r)))
        end

        end
        -- Space streaks (whole area, not only around the player) ----------
        do local C, t, color, glow, soft = FXC("Streaks", dt)
        local streaksOn = on and visual.Streaks
        if streaksOn then
            local recolor = stale("streaks")
            if not fx.streaksOn then
                fx.streaksOn = true
                for _, s in ipairs(fx.streaks) do respawnStreak(s, rpos, true) end
            end
            for _, s in ipairs(fx.streaks) do
                if s.wait > 0 then
                    s.wait -= 1
                    if s.wait == 0 then s.trail.Enabled = true end
                end
                s.pos += (s.vel + Vector3.new(0, math.sin(t * 1.7 + s.phase) * 1.4 + (C.Anim == 2 and -16 or (C.Anim == 3 and 12 or 0)), 0)) * dt * C.Speed
                pushMove(s.part, CFrame.new(s.pos))
                local off = s.pos - rpos
                if Vector3.new(off.X, 0, off.Z).Magnitude > STREAK_RADIUS * 1.08 or math.abs(off.Y) > STREAK_HEIGHT then
                    respawnStreak(s, rpos, false)
                end
                tuneTrail(s.trail, C.Size, 1)
                if recolor then s.trail.Color = glow end
            end
        elseif fx.streaksOn then
            fx.streaksOn = false
            for _, s in ipairs(fx.streaks) do s.trail.Enabled = false end
        end

        end
        -- Lagging bot -------------------------------------------------------
        local ghost = fx.ghost
        if on and visual.Ghost then
            if ghost.sig ~= fx.sig then rebuildGhost() end
            if ghost.model and ghost.model.Parent ~= fx.folder then ghost.model.Parent = fx.folder end
            if not ghost.wasOn then
                ghost.wasOn = true
                ghost.count, ghost.idx, ghost.lastRec = 0, 0, 0
                for _, e in ipairs(ghost.entries) do e.cur = nil end
            end
            if t - ghost.lastRec >= 1 / 60 then
                ghost.lastRec = t
                ghost.idx = ghost.idx % GHOST_HISTORY + 1
                ghost.count = math.min(ghost.count + 1, GHOST_HISTORY)
                local snap = ghost.hist[ghost.idx]
                snap.t = t
                snap.root = root.CFrame
                for _, e in ipairs(ghost.entries) do
                    if e.src.Parent then snap.cfs[e.id] = e.src.CFrame end
                end
            end
            local a, b, k = ghostSample(ghost, t - visual.GhostDelay)
            if a then
                local look = a.root.LookVector
                local flat = Vector3.new(look.X, 0, look.Z)
                flat = flat.Magnitude > 0.01 and flat.Unit or Vector3.new(0, 0, -1)
                local shift = CFrame.new(-flat * GHOST_BACK)
                local follow = 1 - math.exp(-dt * 16)
                local alpha = visual.GhostAlpha / 100
                local retint = ghost.shownAlpha ~= alpha
                for _, e in ipairs(ghost.entries) do
                    local ca, cb = a.cfs[e.id], b.cfs[e.id]
                    ca, cb = ca or cb, cb or ca
                    local target = ca and (shift * ca:Lerp(cb, k)) or (shift * e.src.CFrame)
                    e.cur = e.cur and e.cur:Lerp(target, follow) or target
                    pushMove(e.part, e.cur)
                    if retint then
                        e.part.Transparency = e.hidden and 1 or (1 - (1 - e.base) * alpha)
                    end
                end
                ghost.shownAlpha = alpha
            end
        elseif ghost.wasOn then
            ghost.wasOn = false
            ghost.shownAlpha = -1
            if ghost.model then ghost.model.Parent = nil end
            for _, e in ipairs(ghost.entries) do e.cur = nil end
        end

        -- Distant lightning -----------------------------------------------
        do local C, _, color = FXC("FarLightning", dt); local t = os.clock()
        local far = fx.far
        local farOn = on and visual.FarLightning
        if farOn and not far.wasOn then
            far.wasOn = true
            far.nextAt = t + 1.2
        elseif not farOn then
            far.wasOn = false
        end
        if farOn and not far.active and t >= far.nextAt then
            spawnFarStrike(color)
        end
        if far.active then
            local age = t - far.t0
            if not farOn or age > 0.9 then
                far.active = false
                far.nextAt = t + (3 + math.random() * 8) / C.Speed
                for i = 1, far.used do
                    far.slots[i].glow.Transparency = 1
                    far.slots[i].core.Transparency = 1
                end
                far.flare.Transparency = 1
                farFlash.Visible = false
            else
                local b = strikeBrightness(age)
                local coreT, glowT = 1 - b, 1 - b * 0.6
                for i = 1, far.used do
                    far.slots[i].core.Transparency = coreT
                    far.slots[i].glow.Transparency = glowT
                end
                far.flare.Transparency = 1 - b * 0.55
                farFlash.BackgroundTransparency = 1 - far.power * b
                farFlash.Visible = true
            end
        end

        end
        -- Footstep rings -------------------------------------------------
        do local C, t, color, glow, soft = FXC("Footsteps", dt)
        local hum = fx.humanoid
        local stepsOn = on and visual.Footsteps
        if stepsOn and hum and hum.MoveDirection.Magnitude > 0.1 and hum.FloorMaterial ~= Enum.Material.Air then
            local v = root.AssemblyLinearVelocity
            local spd = Vector3.new(v.X, 0, v.Z).Magnitude
            fx.stepAcc += dt
            if fx.stepAcc >= math.clamp(6 / math.max(spd, 1), 0.26, 0.6) / C.Speed then
                fx.stepAcc = 0
                spawnStep(color, C.Size, C.Anim)
            end
        else
            fx.stepAcc = 0
        end


        end
        flushMoves()
    end
end
__block1()

-- ============================================================================
-- CAMERA: FOV + zoom, sway + shake, stable camera, free camera
-- ============================================================================

local function __block2()
    local ContextActionService = game:GetService("ContextActionService")
    local K = Enum.KeyCode

    local cs = {
        mode = nil, prevType = nil,
        yaw = 0, pitch = 0, dist = 14, focus = nil, target = nil,
        pos = Vector3.zero, vel = Vector3.zero,
        lastOff = nil, swayK = 0,
        lookDelta = Vector2.zero, rmb = false, lockedByUs = false, lookTouch = nil,
        joy = Vector2.zero, joyInput = nil, up = false, down = false,
        controls = nil, rayParams = nil, rayChar = nil,
    }

    -- Touch pad for the free camera (joystick + up / down) --------------------
    local pad = Instance.new("Frame")
    pad.Name = "RMEXFreeCamPad"
    pad.BackgroundTransparency = 1
    pad.Size = UDim2.fromScale(1, 1)
    pad.Active = false
    pad.Visible = false
    pad.ZIndex = 3
    pad.Parent = gui

    local function padButton(text, pos)
        local b = Instance.new("TextButton")
        b.AnchorPoint = Vector2.new(0.5, 0.5)
        b.Size = UDim2.fromOffset(56, 56)
        b.Position = pos
        b.Text = text
        b.Font = Enum.Font.GothamBold
        b.TextSize = 22
        b.TextColor3 = Color3.new(1, 1, 1)
        b.BackgroundColor3 = Color3.fromRGB(20, 20, 28)
        b.BackgroundTransparency = 0.4
        b.AutoButtonColor = false
        b.BorderSizePixel = 0
        b.ZIndex = 3
        b.Parent = pad
        corner(b, 999)
        return b
    end

    local joyBase = padButton("", UDim2.new(0, 100, 1, -120))
    joyBase.Size = UDim2.fromOffset(120, 120)
    local joyKnob = Instance.new("Frame")
    joyKnob.AnchorPoint = Vector2.new(0.5, 0.5)
    joyKnob.Size = UDim2.fromOffset(48, 48)
    joyKnob.Position = UDim2.fromScale(0.5, 0.5)
    joyKnob.BorderSizePixel = 0
    joyKnob.ZIndex = 4
    joyKnob.Parent = joyBase
    corner(joyKnob, 999)

    local upBtn = padButton("▲", UDim2.new(1, -150, 1, -150))
    local downBtn = padButton("▼", UDim2.new(1, -150, 1, -84))

    local function setJoy(pos)
        local center = joyBase.AbsolutePosition + joyBase.AbsoluteSize / 2
        local d = Vector2.new(pos.X, pos.Y) - center
        if d.Magnitude > 48 then d = d.Unit * 48 end
        joyKnob.Position = UDim2.new(0.5, d.X, 0.5, d.Y)
        cs.joy = d / 48
    end

    joyBase.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.Touch and not cs.joyInput then
            cs.joyInput = input
            setJoy(input.Position)
        end
    end)

    local function holdButton(btn, key)
        local held
        btn.InputBegan:Connect(function(input)
            if isPointer(input) and not held then
                held = input
                cs[key] = true
            end
        end)
        UserInputService.InputEnded:Connect(function(input)
            if input == held then
                held = nil
                cs[key] = false
            end
        end)
    end
    holdButton(upBtn, "up")
    holdButton(downBtn, "down")

    -- Look / zoom input ---------------------------------------------------------
    local function releaseMouse()
        cs.rmb = false
        if cs.lockedByUs then
            cs.lockedByUs = false
            UserInputService.MouseBehavior = Enum.MouseBehavior.Default
        end
    end

    UserInputService.InputBegan:Connect(function(input, processed)
        if not cs.mode or processed then return end
        if input.UserInputType == Enum.UserInputType.MouseButton2 then
            cs.rmb = true
            if UserInputService.MouseBehavior == Enum.MouseBehavior.Default then
                cs.lockedByUs = true
                UserInputService.MouseBehavior = Enum.MouseBehavior.LockCurrentPosition
            end
        elseif input.UserInputType == Enum.UserInputType.Touch and not cs.lookTouch then
            cs.lookTouch = input
        end
    end)

    UserInputService.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton2 then
            releaseMouse()
        elseif input == cs.lookTouch then
            cs.lookTouch = nil
        elseif input == cs.joyInput then
            cs.joyInput = nil
            cs.joy = Vector2.zero
            joyKnob.Position = UDim2.fromScale(0.5, 0.5)
        end
    end)

    UserInputService.InputChanged:Connect(function(input, processed)
        local t = input.UserInputType
        if input == cs.joyInput then
            setJoy(input.Position)
        elseif input == cs.lookTouch then
            cs.lookDelta += Vector2.new(input.Delta.X, input.Delta.Y) * 0.0055
        elseif t == Enum.UserInputType.MouseMovement then
            if cs.mode and (cs.rmb or UserInputService.MouseBehavior == Enum.MouseBehavior.LockCenter) then
                cs.lookDelta += Vector2.new(input.Delta.X, input.Delta.Y) * 0.0035
            end
        elseif t == Enum.UserInputType.MouseWheel and cs.mode and not processed then
            if cs.mode == "free" then
                camFX.FreeSpeed = math.clamp(math.floor(camFX.FreeSpeed * (1 + 0.12 * input.Position.Z) + 0.5), 5, 200)
                if camFX.speedRender then camFX.speedRender(true) end
            else
                camFX.Distance = math.clamp(math.floor(camFX.Distance - input.Position.Z * 1.5 + 0.5), 3, 60)
                if camFX.distRender then camFX.distRender(true) end
            end
        end
    end)

    -- Free camera must not walk the character around ----------------------------
    local function setControls(enabled)
        task.spawn(function()
            if cs.controls == nil then
                local ok, res = pcall(function()
                    local scripts = localPlayer:WaitForChild("PlayerScripts", 3)
                    local module = scripts:WaitForChild("PlayerModule", 3)
                    return require(module):GetControls()
                end)
                cs.controls = ok and res or false
            end
            if cs.controls then
                pcall(function()
                    if enabled then cs.controls:Enable() else cs.controls:Disable() end
                end)
            end
        end)
    end

    local function sink()
        return Enum.ContextActionResult.Sink
    end

    local function enterMode(newMode, cam)
        local old = cs.mode
        if old == "free" then
            setControls(true)
            ContextActionService:UnbindAction("RMEXFreeSink")
        end
        releaseMouse()
        cs.lookDelta = Vector2.zero
        cs.lookTouch, cs.focus, cs.vel = nil, nil, Vector3.zero
        if old == nil and newMode ~= nil then cs.prevType = cam.CameraType end
        cs.mode = newMode

        if newMode == nil then
            cam.CameraType = cs.prevType or Enum.CameraType.Custom
            cs.prevType = nil
            return
        end

        cam.CameraType = Enum.CameraType.Scriptable
        local look = cam.CFrame.LookVector
        cs.yaw = math.atan2(-look.X, -look.Z)
        cs.pitch = math.asin(math.clamp(look.Y, -1, 1))
        if newMode == "stable" then
            local char = localPlayer.Character
            local part = char and (char:FindFirstChild("Head") or char:FindFirstChild("HumanoidRootPart"))
            local d = part and (cam.CFrame.Position - part.Position).Magnitude or camFX.Distance
            camFX.Distance = math.clamp(math.floor(d + 0.5), 3, 60)
            cs.dist = d
            if camFX.distRender then camFX.distRender(true) end
        else
            cs.pos = cam.CFrame.Position
            setControls(false)
            ContextActionService:BindActionAtPriority("RMEXFreeSink", sink, false, 3000,
                K.W, K.A, K.S, K.D, K.E, K.Q, K.Space, K.LeftControl, K.LeftShift)
        end
    end

    local function takeLook()
        local d = cs.lookDelta
        cs.lookDelta = Vector2.zero
        cs.yaw -= d.X
        cs.pitch = math.clamp(cs.pitch - d.Y, -1.45, 1.45)
        return CFrame.fromEulerAnglesYXZ(cs.pitch, cs.yaw, 0)
    end

    -- Stable camera: keeps its own angle (only YOUR drag turns it) and follows the character.
    local function updateStable(cam, dt)
        local char = localPlayer.Character
        local part = char and (char:FindFirstChild("Head") or char:FindFirstChild("HumanoidRootPart"))
        if part then cs.target = part.Position + Vector3.new(0, 0.3, 0) end
        if not cs.target then return end
        cs.focus = cs.focus and cs.focus:Lerp(cs.target, 1 - math.exp(-dt * 18)) or cs.target
        cs.dist += (camFX.Distance - cs.dist) * (1 - math.exp(-dt * 8))

        local rot = takeLook()
        local dir = rot.LookVector
        local want = cs.focus - dir * cs.dist

        if char and cs.rayChar ~= char then
            cs.rayChar = char
            local rp = RaycastParams.new()
            rp.FilterType = Enum.RaycastFilterType.Exclude
            rp.RespectCanCollide = true
            rp.FilterDescendantsInstances = {char, fx.folder}
            cs.rayParams = rp
        end
        local pos = want
        if cs.rayParams then
            local hit = workspace:Raycast(cs.focus, want - cs.focus, cs.rayParams)
            if hit then pos = hit.Position + dir * 0.35 end
        end
        cam.CFrame = CFrame.new(pos) * rot
        cam.Focus = CFrame.new(cs.focus)
    end

    -- Free camera: detached, flies with WASD / E / Q (Shift = fast) or the touch pad.
    local function updateFree(cam, dt)
        local rot = takeLook()
        local x, y, z = cs.joy.X, 0, -cs.joy.Y
        if cs.up then y += 1 end
        if cs.down then y -= 1 end
        local fast = false
        if not UserInputService:GetFocusedTextBox() then
            local function down(k) return UserInputService:IsKeyDown(k) end
            if down(K.W) then z += 1 end
            if down(K.S) then z -= 1 end
            if down(K.D) then x += 1 end
            if down(K.A) then x -= 1 end
            if down(K.E) or down(K.Space) then y += 1 end
            if down(K.Q) or down(K.LeftControl) then y -= 1 end
            fast = down(K.LeftShift)
        end
        local move = rot.LookVector * z + rot.RightVector * x + Vector3.yAxis * y
        if move.Magnitude > 1 then move = move.Unit end
        cs.vel = cs.vel:Lerp(move * camFX.FreeSpeed * (fast and 3 or 1), 1 - math.exp(-dt * 9))
        cs.pos += cs.vel * dt
        cam.CFrame = CFrame.new(cs.pos) * rot
        cam.Focus = CFrame.new(cs.pos + rot.LookVector * 20)
    end

    -- Undo last frame's sway / shake before the game's camera runs, so small
    -- offsets never pile up on top of each other.
    RunService:BindToRenderStep("RMEXCameraPre", Enum.RenderPriority.Camera.Value - 1, function()
        local cam = getCam()
        if cam and cs.lastOff then
            cam.CFrame = cam.CFrame * cs.lastOff:Inverse()
            cs.lastOff = nil
        end
    end)

    RunService:BindToRenderStep("RMEXCameraFX", Enum.RenderPriority.Camera.Value + 1, function(dt)
        local cam = getCam()
        if not cam then return end

        local spd, grounded = 0, false
        local root = fx.root
        if root and root.Parent and fx.humanoid then
            local v = root.AssemblyLinearVelocity
            spd = Vector3.new(v.X, 0, v.Z).Magnitude
            grounded = fx.humanoid.FloorMaterial ~= Enum.Material.Air
        end

        -- FOV (base from settings, zoom applied on top). Engine limit is 120.
        local targetFOV = zoomTargetFOV()
        cam.FieldOfView = cam.FieldOfView + (targetFOV - cam.FieldOfView) * (1 - math.exp(-dt * 10))

        -- Camera mode
        local want = camFX.Free and "free" or (camFX.Stable and "stable" or nil)
        if want ~= cs.mode then enterMode(want, cam) end
        if cs.mode then
            if cam.CameraType ~= Enum.CameraType.Scriptable then cam.CameraType = Enum.CameraType.Scriptable end
            if cs.mode == "free" then updateFree(cam, dt) else updateStable(cam, dt) end
        end
        local showPad = cs.mode == "free" and UserInputService.TouchEnabled
        if pad.Visible ~= showPad then
            pad.Visible = showPad
            joyKnob.BackgroundColor3 = P.accent
        end

        -- Shake while running on the ground
        local shakeTarget = 0
        if screenFX.Shake and grounded then
            shakeTarget = math.clamp((spd - 6) / 18, 0, 1) * 0.012
        end
        shakeAmp += (shakeTarget - shakeAmp) * (1 - math.exp(-dt * 10))

        -- Sway: slow, small, smooth drift (fades in / out)
        cs.swayK += ((camFX.Sway and 1 or 0) - cs.swayK) * (1 - math.exp(-dt * 3))

        local off, applied = CFrame.identity, false
        if cs.swayK > 0.002 then
            local t = os.clock()
            local k = cs.swayK * camFX.SwayStrength / 100
            local rx = (math.sin(t * 0.61) * 0.55 + math.sin(t * 1.17 + 1.7) * 0.45) * 0.02 * k
            local ry = (math.sin(t * 0.47 + 0.5) * 0.6 + math.sin(t * 0.93) * 0.4) * 0.024 * k
            local rz = math.sin(t * 0.37 + 2.0) * 0.012 * k
            local ox = math.sin(t * 0.53) * 0.12 * k
            local oy = (math.sin(t * 0.71 + 1.0) * 0.6 + math.sin(t * 1.3) * 0.4) * 0.14 * k
            off = off * CFrame.new(ox, oy, 0) * CFrame.Angles(rx, ry, rz)
            applied = true
        end
        if shakeAmp > 0.0003 then
            local t = os.clock()
            off = off * CFrame.Angles(
                math.sin(t * 41) * shakeAmp + math.sin(t * 17) * shakeAmp * 0.5,
                math.cos(t * 37) * shakeAmp,
                0
            )
            applied = true
        end
        if applied then
            cam.CFrame = cam.CFrame * off
            cs.lastOff = off
        end
    end)
end
__block2()


-- ============================================================================
-- v12 EXTENSIONS: power-on ritual, detection pulse, screen effects, new world effects
-- (everything is pcall-protected from the main loop, so it can never break the older features)
-- ============================================================================
RX.fovKick = 0
local function __block3()
    local WHITE, BLACK = Color3.new(1, 1, 1), Color3.new(0, 0, 0)
    local TAU = math.pi * 2
    local RED, CYAN = Color3.fromRGB(255, 50, 80), Color3.fromRGB(40, 235, 255)
    local GREEN, ALERT = Color3.fromRGB(70, 255, 130), Color3.fromRGB(255, 45, 55)
    local E = {obj = {}, clk = {}, folder = nil}
    local ex = {}                      -- per-frame context for the world effects

    local function efx(name, dt)
        local C0 = visual.cfg[name]
        local tt = E.clk[name] or 0
        local C, c = RX.fxMod.apply(name, C0, tt, C0.Color or getEffectColor())
        E.clk[name] = tt + dt * C.Speed
        return C, E.clk[name], c
    end

    ----------------------------------------------------------------------
    -- Screen layer
    ----------------------------------------------------------------------
    local overlay = Instance.new("Frame")
    overlay.Name = "RMEXOverlay"
    overlay.Size = UDim2.fromScale(1, 1)
    overlay.BackgroundTransparency = 1
    overlay.Active = false
    overlay.ZIndex = 0
    overlay.ClipsDescendants = true
    overlay.Parent = gui

    -- Four gradient edges (opaque at the screen border, clear inwards).
    local function makeEdges(colors, w, h)
        local set = {frames = {}, w = w, h = h}
        local defs = {
            {Vector2.new(0, 0), UDim2.new(0, 0, 0, 0), true, false},   -- left
            {Vector2.new(1, 0), UDim2.new(1, 0, 0, 0), true, true},    -- right
            {Vector2.new(0, 0), UDim2.new(0, 0, 0, 0), false, false},  -- top
            {Vector2.new(0, 1), UDim2.new(0, 0, 1, 0), false, true},   -- bottom
        }
        for i, d in ipairs(defs) do
            local f = Instance.new("Frame")
            f.AnchorPoint = d[1]
            f.Position = d[2]
            f.BackgroundColor3 = colors[i]
            f.BackgroundTransparency = 1
            f.BorderSizePixel = 0
            f.Active = false
            f.Visible = false
            f.ZIndex = 0
            f.Parent = overlay
            local g = Instance.new("UIGradient")
            local outer, inner = 0, 1
            g.Transparency = NumberSequence.new({
                NumberSequenceKeypoint.new(0, d[4] and inner or outer),
                NumberSequenceKeypoint.new(1, d[4] and outer or inner),
            })
            g.Rotation = d[3] and 0 or 90
            g.Parent = f
            set.frames[i] = f
        end
        function set.show(a, wScale)
            local vis = a > 0.01
            for i, f in ipairs(set.frames) do
                f.Visible = vis
                if vis then
                    f.BackgroundTransparency = 1 - math.clamp(a, 0, 1) * 0.85
                    local k = wScale or 1
                    if i <= 2 then
                        f.Size = UDim2.new(set.w * k, 0, 1, 0)
                    else
                        f.Size = UDim2.new(1, 0, set.h * k, 0)
                    end
                end
            end
        end
        function set.color(c)
            for _, f in ipairs(set.frames) do f.BackgroundColor3 = c end
        end
        return set
    end

    local detEdges = makeEdges({GREEN, GREEN, GREEN, GREEN}, 0.16, 0.26)
    local chromaEdges = makeEdges({RED, CYAN, Color3.fromRGB(190, 70, 255), Color3.fromRGB(255, 210, 60)}, 0.1, 0.16)

    -- Detection banner (typed text)
    local banner = Instance.new("TextLabel")
    banner.AnchorPoint = Vector2.new(0.5, 0)
    banner.Position = UDim2.new(0.5, 0, 0, 14)
    banner.Size = UDim2.fromOffset(240, 24)
    banner.BackgroundColor3 = Color3.fromRGB(10, 10, 14)
    banner.BackgroundTransparency = 0.35
    banner.TextColor3 = GREEN
    banner.Font = Enum.Font.Code
    banner.TextSize = 13
    banner.Text = ""
    banner.Visible = false
    banner.ZIndex = 1
    banner.Parent = gui
    corner(banner, 6)
    local bannerStroke = Instance.new("UIStroke")
    bannerStroke.Thickness = 1.5
    bannerStroke.Color = GREEN
    bannerStroke.Parent = banner

    -- Glitch bars pool
    local bars = {frames = {}, left = 0, acc = 0, k = 1}
    for i = 1, 14 do
        local f = Instance.new("Frame")
        f.BorderSizePixel = 0
        f.Active = false
        f.Visible = false
        f.ZIndex = 0
        f.Size = UDim2.new(1.1, 0, 0, 6)
        f.Parent = overlay
        bars.frames[i] = f
    end
    function bars.burst(d, k)
        bars.left = math.max(bars.left, d)
        bars.k = k or 1
        bars.acc = 1
    end
    local BAR_COLORS = {RED, CYAN, WHITE, Color3.fromRGB(190, 70, 255)}
    function bars.update(dt)
        if bars.left <= 0 then
            if bars.on then
                bars.on = false
                for _, f in ipairs(bars.frames) do f.Visible = false end
            end
            return
        end
        bars.on = true
        bars.left -= dt
        bars.acc += dt
        if bars.acc >= 0.04 then
            bars.acc = 0
            for _, f in ipairs(bars.frames) do
                if math.random() < 0.25 + 0.55 * bars.k then
                    f.Visible = true
                    f.Position = UDim2.new(-0.05 + math.random() * 0.1, 0, math.random(), 0)
                    f.Size = UDim2.new(1.1, 0, 0, math.random(2, 8 + math.floor(30 * bars.k)))
                    f.BackgroundColor3 = BAR_COLORS[math.random(1, #BAR_COLORS)]
                    f.BackgroundTransparency = 0.5 + math.random() * 0.35
                else
                    f.Visible = false
                end
            end
        end
    end

    ----------------------------------------------------------------------
    -- Detection pulse (#3): red edge for aimbot, green for ESP
    ----------------------------------------------------------------------
    local D = {t = nil, text = "", color = GREEN}
    local function detect(color, key)
        if not visual.Detect then return end
        D.t = 0
        D.color = color
        D.text = STRINGS[lang][key] or key
        detEdges.color(color)
        banner.TextColor3 = color
        bannerStroke.Color = color
        banner.Visible = true
        RX.beep(true)
    end
    RX.detectTest = function()
        local was = visual.Detect
        visual.Detect = true
        detect(math.random() < 0.5 and GREEN or ALERT, math.random() < 0.5 and "det_esp" or "det_aim")
        visual.Detect = was
    end
    local function detectStep(dt)
        if not D.t then return end
        D.t += dt
        local t = D.t
        local env = math.min(1, t / 0.15) * math.max(0, 1 - (t - 2.7) / 0.8)
        if t > 3.5 then
            D.t = nil
            detEdges.show(0)
            banner.Visible = false
            return
        end
        local pulse = math.abs(math.sin(t * math.pi * 2.4))
        detEdges.show(env * (0.35 + 0.65 * pulse), 1 + 0.15 * pulse)
        local n = math.clamp(math.floor(t * 38), 0, #D.text)
        banner.Text = D.text:sub(1, n) .. ((t * 6) % 1 < 0.5 and "_" or "")
        banner.TextTransparency = 1 - env
        banner.BackgroundTransparency = 1 - env * 0.65
        bannerStroke.Transparency = 1 - env
    end

    ----------------------------------------------------------------------
    -- Power-on ritual (#2): screen tears (RGB split + glitch bands), then you dissolve in
    ----------------------------------------------------------------------
    local R = {t = nil, parts = {}, decals = {}, last = -100}
    local rCC, rBlur, rRing
    local function ritualCleanup()
        for _, it in ipairs(R.parts) do
            if it.p.Parent then
                it.p.Transparency, it.p.Material, it.p.Color = it.T, it.M, it.C
            end
        end
        for _, it in ipairs(R.decals) do
            if it.d.Parent then it.d.Transparency = it.T end
        end
        R.parts, R.decals, R.t = {}, {}, nil
        if rCC then rCC:Destroy() rCC = nil end
        if rBlur then rBlur:Destroy() rBlur = nil end
        if rRing then rRing:Destroy() rRing = nil end
        R.kick = 0
        R.chroma = 0
    end
    RX.ritualPlay = function()
        local ch, root = fx.character, fx.root
        if R.t or not ch or not root or not root.Parent then return end
        R.t, R.last = 0, os.clock()
        R.char = ch
        R.parts, R.decals = {}, {}
        local minY, maxY = math.huge, -math.huge
        for _, d in ipairs(ch:GetDescendants()) do
            if d:IsA("BasePart") and d.Name ~= "HumanoidRootPart" then
                local y = d.Position.Y
                minY, maxY = math.min(minY, y), math.max(maxY, y)
                table.insert(R.parts, {p = d, T = d.Transparency, M = d.Material, C = d.Color, y = y, th = 0})
            elseif d:IsA("Decal") or d:IsA("Texture") then
                table.insert(R.decals, {d = d, T = d.Transparency})
            end
        end
        for _, it in ipairs(R.parts) do
            local rank = (it.y - minY) / math.max(maxY - minY, 0.01)
            it.th = math.clamp(rank * 0.45 + math.random() * 0.25, 0, 0.7)
            it.p.Transparency = 1
        end
        for _, it in ipairs(R.decals) do it.d.Transparency = 1 end
        rCC = Instance.new("ColorCorrectionEffect")
        rCC.Name = "RMEXRitualCC"
        rCC.Parent = Lighting
        rBlur = Instance.new("BlurEffect")
        rBlur.Name = "RMEXRitualBlur"
        rBlur.Size = 0
        rBlur.Parent = Lighting
        bars.burst(0.5, 1)
        RX.beep(false)
        task.delay(0.12, function() RX.beep(true) end)
        if fx.folder then
            rRing = Instance.new("Part")
            rRing.Name = "RMEX_Ritual"
            rRing.Shape = Enum.PartType.Cylinder
            rRing.Size = Vector3.new(0.14, 5, 5)
            rRing.Material = Enum.Material.Neon
            rRing.Anchored, rRing.CanCollide, rRing.CanTouch, rRing.CanQuery, rRing.CastShadow = true, false, false, false, false
            rRing.Transparency = 1
            rRing.Parent = fx.folder
        end
    end
    local function ritualStep(dt, cam)
        if not R.t then return end
        if fx.character ~= R.char or not fx.root or not fx.root.Parent then
            ritualCleanup()
            return
        end
        R.t += dt
        local t = R.t
        local color = getEffectColor()
        -- stage A: the screen tears
        local k = math.clamp(1 - t / 0.5, 0, 1)
        R.chroma = k
        R.kick = 16 * k * k
        if rCC then
            rCC.TintColor = (math.floor(t * 18) % 2 == 0) and Color3.fromRGB(255, 130, 150) or Color3.fromRGB(130, 255, 255)
            rCC.Contrast = 0.4 * k
            rCC.Saturation = 0.7 * k
            if k <= 0 then rCC.TintColor = WHITE end
        end
        if rBlur then rBlur.Size = 14 * k end
        if k > 0 then
            cam.CFrame = cam.CFrame * CFrame.Angles((math.random() - 0.5) * 0.04 * k, (math.random() - 0.5) * 0.04 * k, (math.random() - 0.5) * 0.07 * k)
        end
        -- stage B: dissolve in from the feet up, with a glowing neon edge
        local s = math.clamp((t - 0.35) / 1.5, 0, 1)
        s = s * s * (3 - 2 * s)
        for _, it in ipairs(R.parts) do
            local p = it.p
            if p.Parent then
                local l = math.clamp((s - it.th) / 0.3, 0, 1)
                if l <= 0 then
                    p.Transparency = 1
                elseif l < 1 then
                    p.Material = Enum.Material.Neon
                    p.Color = color:Lerp(WHITE, 0.4 * (1 - l))
                    p.Transparency = math.random() < 0.3 and 1 or (it.T + (1 - it.T) * (1 - l) * 0.55)
                elseif not it.done then
                    it.done = true
                    p.Material, p.Color, p.Transparency = it.M, it.C, it.T
                end
            end
        end
        if s >= 1 then
            for _, it in ipairs(R.decals) do
                if it.d.Parent then it.d.Transparency = it.T end
            end
        end
        if rRing and fx.root then
            rRing.Transparency = (s > 0 and s < 1) and 0.5 or 1
            rRing.Color = color
            rRing.CFrame = CFrame.new(fx.root.Position + Vector3.new(0, -3 + s * 6.6, 0)) * CFrame.Angles(0, 0, math.pi / 2)
        end
        if t > 2.1 then ritualCleanup() end
    end

    ----------------------------------------------------------------------
    -- World helpers
    ----------------------------------------------------------------------
    local mvP, mvC, mvN = {}, {}, 0
    local function mv(p, cf)
        mvN += 1
        mvP[mvN], mvC[mvN] = p, cf
    end
    local function flush()
        if mvN > 0 then
            for i = #mvP, mvN + 1, -1 do
                mvP[i], mvC[i] = nil, nil
            end
            workspace:BulkMoveTo(mvP, mvC, Enum.BulkMoveMode.FireCFrameChanged)
        end
        mvN = 0
    end
    local function ensureFolder()
        if not E.folder or not E.folder.Parent then
            E.folder = Instance.new("Folder")
            E.folder.Name = "RMEX_FX"
            E.folder.Parent = workspace
            E.obj = {}
        end
        return E.folder
    end
    local function mk(shape, size, mat, o, base)
        local p = Instance.new("Part")
        p.Shape = shape
        p.Size = size
        p.Anchored = true
        p.CanCollide, p.CanTouch, p.CanQuery, p.CastShadow = false, false, false, false
        p.Material = mat or Enum.Material.Neon
        p.Transparency = 1
        p.TopSurface, p.BottomSurface = Enum.SurfaceType.Smooth, Enum.SurfaceType.Smooth
        p.Parent = E.folder
        if o then
            table.insert(o.parts, p)
            o.base[p] = base or 0.15
        end
        return p
    end
    local function newObj()
        local o = {parts = {}, base = {}}
        function o.vis(on)
            for _, p in ipairs(o.parts) do p.Transparency = on and o.base[p] or 1 end
        end
        return o
    end
    local function rdir()
        local v = Vector3.new(math.random() - 0.5, math.random() - 0.5, math.random() - 0.5)
        if v.Magnitude < 0.05 then return Vector3.yAxis end
        return v.Unit
    end
    local BLOCK, BALL, CYL = Enum.PartType.Block, Enum.PartType.Ball, Enum.PartType.Cylinder
    local FXS, ORDER = {}, {}
    local function def(name, build, step)
        FXS[name] = {build = build, step = step}
        table.insert(ORDER, name)
    end

    local function trailOn(part, w, life)
        local a0 = Instance.new("Attachment")
        a0.Position = Vector3.new(0, w, 0)
        a0.Parent = part
        local a1 = Instance.new("Attachment")
        a1.Position = Vector3.new(0, -w, 0)
        a1.Parent = part
        local tr = Instance.new("Trail")
        tr.Attachment0, tr.Attachment1 = a0, a1
        tr.Lifetime = life
        tr.MinLength = 0.02
        tr.LightEmission = 1
        tr.LightInfluence = 0
        tr.FaceCamera = true
        tr.Transparency = NumberSequence.new({NumberSequenceKeypoint.new(0, 0.1), NumberSequenceKeypoint.new(1, 1)})
        tr.WidthScale = NumberSequence.new({NumberSequenceKeypoint.new(0, 1), NumberSequenceKeypoint.new(1, 0)})
        tr.Enabled = false
        tr.Parent = part
        return tr
    end

    ----------------------------------------------------------------------
    -- 1. Scan ring
    ----------------------------------------------------------------------
    def("Scanner", function()
        local o = newObj()
        mk(CYL, Vector3.new(0.12, 4, 4), nil, o, 0.7)
        mk(CYL, Vector3.new(0.12, 4, 4), nil, o, 0.7)
        return o
    end, function(o, C, t, color, cx)
        local a, k = C.Anim, C.Size
        for i, d in ipairs(o.parts) do
            if i == 2 and a ~= 3 then
                d.Transparency = 1
            else
                local ph = (t * 0.55 + (i == 2 and 0.5 or 0)) % 1
                local f = ph
                if a == 2 then f = 1 - math.abs(ph * 2 - 1) elseif a == 4 then f = 1 - ph end
                local s = (3.6 + math.sin(math.pi * ph) * 1.1) * k
                d.Size = Vector3.new(0.12, s, s)
                d.Transparency = 0.55 + 0.4 * (1 - math.sin(math.pi * ph))
                if o.col ~= color then d.Color = color end
                mv(d, CFrame.new(cx.rpos + Vector3.new(0, -3 + f * 6.6, 0)) * CFrame.Angles(0, 0, math.pi / 2))
            end
        end
        o.col = color
    end)

    ----------------------------------------------------------------------
    -- 2. Code rain (hacker glyphs on billboards)
    ----------------------------------------------------------------------
    local GLYPHS = {"0", "1", "0", "1", "A", "F", "7", "#", "$", "%", "&", "X", "<", ">"}
    def("Matrix", function()
        local o = newObj()
        o.items = {}
        for i = 1, 36 do
            local p = mk(BLOCK, Vector3.new(0.2, 0.2, 0.2), nil, nil)
            local b = Instance.new("BillboardGui")
            b.Size = UDim2.fromOffset(16, 18)
            b.AlwaysOnTop = false
            b.LightInfluence = 0
            b.MaxDistance = 140
            b.Adornee = p
            b.Enabled = false
            b.Parent = p
            local l = Instance.new("TextLabel")
            l.Size = UDim2.fromScale(1, 1)
            l.BackgroundTransparency = 1
            l.Font = Enum.Font.Code
            l.TextSize = 15
            l.TextStrokeTransparency = 1
            l.Text = GLYPHS[math.random(1, #GLYPHS)]
            l.Parent = b
            o.items[i] = {
                p = p, gui = b, lab = l, ang = math.random() * TAU, rad = 1.8 + math.random() * 3.2,
                y = -3 + math.random() * 11, spd = 3 + math.random() * 4, nextC = 0, lead = i % 6 == 0,
            }
        end
        function o.vis(on)
            for _, it in ipairs(o.items) do it.gui.Enabled = on end
        end
        return o
    end, function(o, C, t, color, cx, dt)
        local a, k, sp = C.Anim, C.Size, C.Speed
        local recolor = o.col ~= color
        o.col = color
        for _, it in ipairs(o.items) do
            if a == 3 then
                it.y += it.spd * dt * sp
                if it.y > 8.5 then it.y = -3.2 end
            else
                it.y -= it.spd * dt * sp
                if it.y < -3.2 then it.y = 8.5 end
            end
            local r = it.rad * k
            if a == 2 then
                it.ang += dt * sp * 1.5
                r = r * (0.35 + 0.65 * (it.y + 3.2) / 11.7)
            end
            mv(it.p, CFrame.new(cx.rpos + Vector3.new(math.cos(it.ang) * r, it.y, math.sin(it.ang) * r)))
            local edge = math.clamp(math.min(it.y + 3.2, 8.5 - it.y) / 2.5, 0, 1)
            it.lab.TextTransparency = 1 - edge * 0.9
            if recolor then it.lab.TextColor3 = it.lead and color:Lerp(WHITE, 0.7) or color end
            if t > it.nextC then
                it.nextC = t + 0.12 + math.random() * 0.3
                it.lab.Text = GLYPHS[math.random(1, #GLYPHS)]
            end
        end
    end)

    ----------------------------------------------------------------------
    -- 3. Vortex
    ----------------------------------------------------------------------
    def("Vortex", function()
        local o = newObj()
        for i = 1, 48 do mk(BLOCK, Vector3.new(0.28, 0.28, 0.28), nil, o, 0.15) end
        return o
    end, function(o, C, t, color, cx)
        local a, k = C.Anim, C.Size
        local recolor = o.col ~= color
        o.col = color
        for i, p in ipairs(o.parts) do
            local u = i / 48
            local ang, r, y
            if a == 1 then
                ang, r, y = u * TAU * 3 + t * 2.5, (0.8 + u * 3.2) * k, -2.8 + u * 7
            elseif a == 2 then
                ang, r, y = u * TAU * 3 - t * 2.5, (4 - u * 3.2) * k, -2.8 + u * 7
            else
                local f = (u + t * 0.25) % 1
                ang, r, y = u * TAU * 4 + t * 3, (1 + math.sin(math.pi * f) * 2.4) * k, -2.8 + f * 7
            end
            mv(p, CFrame.new(cx.rpos + Vector3.new(math.cos(ang) * r, y, math.sin(ang) * r)) * CFrame.Angles(t * 2 + i, t * 3, 0))
            if recolor then p.Color = color:Lerp(WHITE, (1 - u) * 0.5) end
        end
    end)

    ----------------------------------------------------------------------
    -- 4. DNA helix
    ----------------------------------------------------------------------
    def("Helix", function()
        local o = newObj()
        for i = 1, 36 do mk(BALL, Vector3.new(0.3, 0.3, 0.3), nil, o, 0.12) end
        for i = 1, 9 do mk(BLOCK, Vector3.new(0.05, 0.05, 1), nil, o, 0.5) end
        return o
    end, function(o, C, t, color, cx)
        local a, k = C.Anim, C.Size
        local recolor = o.col ~= color
        o.col = color
        local pos = {}
        for s = 0, 1 do
            for i = 1, 18 do
                local u = i / 18
                local dir = (a == 2 and s == 1) and -1 or 1
                local ang = u * TAU * 1.5 + s * math.pi + t * 2 * dir
                local v = cx.rpos + Vector3.new(math.cos(ang) * 1.9 * k, -2.6 + u * 6.2, math.sin(ang) * 1.9 * k)
                local idx = s * 14 + i
                pos[idx] = v
                local p = o.parts[idx]
                mv(p, CFrame.new(v))
                if a == 3 then p.Transparency = 0.1 + 0.65 * (0.5 + 0.5 * math.sin(u * 8 - t * 5)) end
                if recolor then p.Color = color end
            end
        end
        for j = 1, 9 do
            local A, B = pos[j * 2], pos[18 + j * 2]
            local rung = o.parts[36 + j]
            rung.Size = Vector3.new(0.05, 0.05, math.max((A - B).Magnitude, 0.1))
            mv(rung, CFrame.lookAt((A + B) / 2, B))
            if recolor then rung.Color = color end
        end
    end)

    ----------------------------------------------------------------------
    -- 5. Comets
    ----------------------------------------------------------------------
    def("Comets", function()
        local o = newObj()
        o.trails = {}
        for i = 1, 7 do
            local p = mk(BALL, Vector3.new(0.5, 0.5, 0.5), nil, o, 0.05)
            o.trails[i] = trailOn(p, 0.45, 0.9)
        end
        local base = o.vis
        function o.vis(on)
            base(on)
            for _, tr in ipairs(o.trails) do tr.Enabled = on end
        end
        return o
    end, function(o, C, t, color, cx)
        local a, k = C.Anim, C.Size
        local recolor = o.col ~= color
        o.col = color
        for i, p in ipairs(o.parts) do
            local ph = i / 7 * TAU
            local v
            if a == 1 then
                local ang, r = t * 1.6 + ph, (3.2 + i * 0.25) * k
                v = Vector3.new(math.cos(ang) * r, 0.3 + math.sin(t * 2 + ph) * 0.3, math.sin(ang) * r)
            elseif a == 2 then
                local ang, r = t * 1.8 + ph, 3.6 * k
                v = CFrame.Angles((i - 4) * 0.42, ph, (i - 4) * 0.26):VectorToWorldSpace(Vector3.new(math.cos(ang) * r, 0, math.sin(ang) * r))
            else
                local ang, r = t * (1.2 + 0.3 * i) + ph, (3 + 1.6 * math.sin(t * 1.3 + ph)) * k
                v = Vector3.new(math.cos(ang) * r, math.sin(t * 1.7 + ph * 2) * 2.2, math.sin(ang) * r)
            end
            mv(p, CFrame.new(cx.rpos + v))
            if recolor then
                p.Color = color:Lerp(WHITE, 0.4)
                o.trails[i].Color = ColorSequence.new(color:Lerp(WHITE, 0.5), color)
            end
        end
    end)

    ----------------------------------------------------------------------
    -- 6. Ribbons
    ----------------------------------------------------------------------
    def("Ribbons", function()
        local o = newObj()
        o.trails = {}
        for i = 1, 3 do
            local p = mk(BALL, Vector3.new(0.2, 0.2, 0.2), nil, nil)
            local tr = trailOn(p, 0.4, 1.1)
            tr.Transparency = NumberSequence.new({NumberSequenceKeypoint.new(0, 0.15), NumberSequenceKeypoint.new(1, 1)})
            o.parts[i] = p
            o.base[p] = 1
            o.trails[i] = tr
        end
        function o.vis(on)
            for _, tr in ipairs(o.trails) do tr.Enabled = on end
        end
        return o
    end, function(o, C, t, color, cx)
        local a, k = C.Anim, C.Size
        local recolor = o.col ~= color
        o.col = color
        for i, p in ipairs(o.parts) do
            local ph = i * 2.1
            local rel
            if a == 1 then
                rel = Vector3.new((i - 2) * 1.0 + math.sin(t * 3 + ph) * 0.9 * k, 0.6 + math.sin(t * 2 + ph) * 0.7, 1.4)
            elseif a == 2 then
                local ang = t * 3 + ph
                rel = Vector3.new(math.cos(ang) * 1.4 * k, 0.6 + math.sin(ang) * 1.4 * k, 1.6)
            else
                rel = Vector3.new(math.noise(t * 3, i) * 2.4 * k, 0.6 + math.noise(t * 3.3, i + 9) * 2.2, 1.2 + math.abs(math.noise(t * 2, i)) * 1.5)
            end
            mv(p, CFrame.new(cx.root.CFrame:PointToWorldSpace(rel)))
            if recolor then
                local h, s, v = color:ToHSV()
                local c2 = Color3.fromHSV((h + (i - 2) * 0.07) % 1, s, v)
                o.trails[i].Color = ColorSequence.new(c2:Lerp(WHITE, 0.3), c2)
            end
        end
    end)

    ----------------------------------------------------------------------
    -- 7. Force bubble (ForceField material has a hex pattern)
    ----------------------------------------------------------------------
    def("Bubble", function()
        local o = newObj()
        mk(BALL, Vector3.new(8, 8, 8), Enum.Material.ForceField, o, 0.6)
        return o
    end, function(o, C, t, color, cx)
        local a, k = C.Anim, C.Size
        local p = o.parts[1]
        local s, tr = 7.5 * k, 0.6
        if a == 1 then
            s, tr = s * (1 + 0.04 * math.sin(t * 2)), 0.62 + 0.08 * math.sin(t * 2)
        elseif a == 2 then
            s, tr = s * (1 + 0.08 * math.sin(t * 3)), 0.45 + 0.4 * (0.5 + 0.5 * math.sin(t * 4))
        else
            tr = math.clamp(0.55 + 0.45 * math.noise(t * 12, 2), 0.2, 0.9)
        end
        p.Size = Vector3.new(s, s, s)
        p.Transparency = tr
        p.Color = color
        mv(p, CFrame.new(cx.rpos + Vector3.new(0, 0.3, 0)))
    end)

    ----------------------------------------------------------------------
    -- 8. Wire cage
    ----------------------------------------------------------------------
    local CV = {Vector3.new(-1, -1, -1), Vector3.new(1, -1, -1), Vector3.new(1, 1, -1), Vector3.new(-1, 1, -1),
        Vector3.new(-1, -1, 1), Vector3.new(1, -1, 1), Vector3.new(1, 1, 1), Vector3.new(-1, 1, 1)}
    local CE = {{1, 2}, {2, 3}, {3, 4}, {4, 1}, {5, 6}, {6, 7}, {7, 8}, {8, 5}, {1, 5}, {2, 6}, {3, 7}, {4, 8}}
    def("Cage", function()
        local o = newObj()
        for i = 1, 12 do mk(BLOCK, Vector3.new(0.09, 0.09, 1), nil, o, 0.1) end
        return o
    end, function(o, C, t, color, cx)
        local a, k = C.Anim, C.Size
        local half = 2.7 * k * (a == 3 and (1 + 0.12 * math.sin(t * 2)) or 1)
        local rot = a == 2 and CFrame.Angles(t * 0.7, t * 0.9, t * 0.5) or CFrame.Angles(0, t * (a == 3 and 0.4 or 0.9), 0)
        local recolor = o.col ~= color
        o.col = color
        for i, e in ipairs(CE) do
            local A = cx.rpos + rot:VectorToWorldSpace(CV[e[1]] * half)
            local B = cx.rpos + rot:VectorToWorldSpace(CV[e[2]] * half)
            local p = o.parts[i]
            p.Size = Vector3.new(0.09, 0.09, (A - B).Magnitude)
            mv(p, CFrame.lookAt((A + B) / 2, B))
            if recolor then p.Color = color end
        end
    end)

    ----------------------------------------------------------------------
    -- 9. Laser eyes
    ----------------------------------------------------------------------
    local laserRay = RaycastParams.new()
    laserRay.FilterType = Enum.RaycastFilterType.Exclude
    def("Laser", function()
        local o = newObj()
        mk(BLOCK, Vector3.new(0.1, 0.1, 1), nil, o, 0.05)
        mk(BLOCK, Vector3.new(0.1, 0.1, 1), nil, o, 0.05)
        mk(BALL, Vector3.new(0.5, 0.5, 0.5), nil, o, 0.1)
        return o
    end, function(o, C, t, color, cx)
        local head = cx.char and cx.char:FindFirstChild("Head")
        if not head then
            o.vis(false)
            return
        end
        local a, k = C.Anim, C.Size
        local dir = head.CFrame.LookVector
        if a == 3 then dir = CFrame.Angles(0, math.sin(t * 2.2) * 0.5, 0):VectorToWorldSpace(dir) end
        laserRay.FilterDescendantsInstances = {cx.char, E.folder}
        local hit = workspace:Raycast(head.Position, dir * 70, laserRay)
        local endp = hit and hit.Position or (head.Position + dir * 70)
        local w = (a == 2 and (0.05 + 0.08 * (0.5 + 0.5 * math.sin(t * 14))) or 0.1) * k
        for side = 1, 2 do
            local org = head.CFrame:PointToWorldSpace(Vector3.new(side == 1 and -0.22 or 0.22, 0.12, -0.5))
            local len = math.max((endp - org).Magnitude, 0.2)
            local b = o.parts[side]
            b.Size = Vector3.new(w, w, len)
            b.Color = color
            b.Transparency = 0.05
            mv(b, CFrame.lookAt(org, endp) * CFrame.new(0, 0, -len / 2))
        end
        local ball = o.parts[3]
        ball.Color = color:Lerp(WHITE, 0.5)
        ball.Transparency = hit and 0.1 or 1
        local s = (0.4 + 0.3 * math.sin(t * 20)) * k
        ball.Size = Vector3.new(s, s, s)
        mv(ball, CFrame.new(endp))
    end)

    ----------------------------------------------------------------------
    -- 10. Cheater tag
    ----------------------------------------------------------------------
    local GL = {"#", "%", "@", "0", "1", "X", "?", "/"}
    def("Tag", function()
        local o = newObj()
        local p = mk(BLOCK, Vector3.new(0.2, 0.2, 0.2), nil, nil)
        local b = Instance.new("BillboardGui")
        b.Size = UDim2.fromOffset(170, 38)
        b.AlwaysOnTop = false
        b.LightInfluence = 0
        b.MaxDistance = 250
        b.Enabled = false
        b.Adornee = p
        b.Parent = p
        local bg = Instance.new("Frame")
        bg.Size = UDim2.fromScale(1, 1)
        bg.BackgroundColor3 = Color3.fromRGB(10, 10, 16)
        bg.BackgroundTransparency = 0.35
        bg.BorderSizePixel = 0
        bg.Parent = b
        corner(bg, 8)
        local st = Instance.new("UIStroke")
        st.Thickness = 1.5
        st.Parent = bg
        local function lab(z)
            local l = Instance.new("TextLabel")
            l.Size = UDim2.fromScale(1, 1)
            l.BackgroundTransparency = 1
            l.Font = Enum.Font.Code
            l.TextSize = 22
            l.ZIndex = z
            l.Parent = bg
            return l
        end
        o.gR, o.gC, o.main = lab(1), lab(2), lab(3)
        o.gR.TextColor3, o.gC.TextColor3 = RED, CYAN
        o.gR.TextTransparency, o.gC.TextTransparency = 0.45, 0.45
        o.stroke, o.part, o.gui, o.next, o.glitch = st, p, b, 0, 0
        function o.vis(on) b.Enabled = on end
        return o
    end, function(o, C, t, color, cx, dt)
        local head = cx.char and cx.char:FindFirstChild("Head")
        if not head then return end
        mv(o.part, CFrame.new(head.Position + Vector3.new(0, 2.2 * math.max(C.Size, 0.6), 0)))
        local word = STRINGS[lang].tag_text
        local a = C.Anim
        local txt = word
        local main = color
        o.gui.Size = UDim2.fromOffset(170 * C.Size, 38 * C.Size)
        if a == 1 then
            if t > o.next then
                o.next = t + 0.1 + math.random() * 0.4
                o.glitch = 0.12
            end
            if o.glitch > 0 then
                o.glitch -= dt
                local chars = {}
                for i = 1, #word do
                    chars[i] = (math.random() < 0.3) and GL[math.random(1, #GL)] or word:sub(i, i)
                end
                txt = table.concat(chars)
            end
        elseif a == 2 then
            local n = math.floor(t * 6) % (#word + 6)
            txt = word:sub(1, math.min(n, #word)) .. ((t * 3) % 1 < 0.5 and "_" or " ")
        else
            main = Color3.fromHSV((t * 0.3) % 1, 0.8, 1)
        end
        o.main.Text, o.gR.Text, o.gC.Text = txt, txt, txt
        o.main.TextColor3 = main
        o.stroke.Color = main
        local off = (o.glitch > 0 and 3 or 1) * (a == 1 and 1 or 0.5)
        o.gR.Position, o.gC.Position = UDim2.fromOffset(-off, 0), UDim2.fromOffset(off, 0)
    end)

    ----------------------------------------------------------------------
    -- 11. Rush flames (video look)
    ----------------------------------------------------------------------
    local FIRE_TEX = "rbxasset://textures/particles/fire_main.dds"
    local SPARK_TEX = "rbxasset://textures/particles/sparkles_main.dds"
    def("Rush", function()
        local o = newObj()
        local p = mk(BLOCK, Vector3.new(0.2, 0.2, 0.2), nil, nil)
        local function em(tex, life, spd, szA, szB)
            local e = Instance.new("ParticleEmitter")
            e.Texture = tex
            e.Lifetime = NumberRange.new(life * 0.7, life)
            e.Speed = NumberRange.new(spd * 0.6, spd)
            e.SpreadAngle = Vector2.new(22, 22)
            e.EmissionDirection = Enum.NormalId.Back
            e.Rate = 0
            e.LightEmission = 1
            e.LightInfluence = 0
            e.Rotation = NumberRange.new(0, 360)
            e.RotSpeed = NumberRange.new(-120, 120)
            e.Size = NumberSequence.new({NumberSequenceKeypoint.new(0, szA), NumberSequenceKeypoint.new(0.4, szA * 0.7), NumberSequenceKeypoint.new(1, szB)})
            e.Transparency = NumberSequence.new({NumberSequenceKeypoint.new(0, 0), NumberSequenceKeypoint.new(0.7, 0.3), NumberSequenceKeypoint.new(1, 1)})
            e.Enabled = false
            e.Parent = p
            return e
        end
        o.fire, o.spark, o.part = em(FIRE_TEX, 0.55, 16, 1.6, 0.1), em(SPARK_TEX, 0.5, 22, 0.8, 0), p
        o.acc = 0
        function o.vis(on)
            o.fire.Enabled = on
            o.spark.Enabled = on
        end
        return o
    end, function(o, C, t, color, cx, dt)
        local a, k = C.Anim, C.Size
        if o.col ~= color then
            o.col = color
            o.fire.Color = ColorSequence.new({
                ColorSequenceKeypoint.new(0, WHITE:Lerp(color, 0.2)),
                ColorSequenceKeypoint.new(0.35, color),
                ColorSequenceKeypoint.new(1, color:Lerp(BLACK, 0.6)),
            })
            o.spark.Color = ColorSequence.new(WHITE, color)
        end
        if o.k ~= k then
            o.k = k
            o.fire.Size = NumberSequence.new({NumberSequenceKeypoint.new(0, 1.6 * k), NumberSequenceKeypoint.new(0.4, 1.1 * k), NumberSequenceKeypoint.new(1, 0.1)})
        end
        local speedK = C.Speed
        if a == 1 then
            o.fire.SpreadAngle, o.spark.SpreadAngle = Vector2.new(22, 22), Vector2.new(35, 35)
            local rate = (30 + cx.spd * 4) * speedK
            o.fire.Rate, o.spark.Rate = rate, rate * 0.6
            mv(o.part, cx.root.CFrame * CFrame.new(0, 0.3, 1.2))
        elseif a == 2 then
            o.fire.SpreadAngle, o.spark.SpreadAngle = Vector2.new(180, 180), Vector2.new(180, 180)
            o.fire.Rate, o.spark.Rate = 0, 0
            o.acc += dt * speedK
            if o.acc > 0.7 then
                o.acc = 0
                o.fire:Emit(22)
                o.spark:Emit(14)
            end
            mv(o.part, CFrame.new(cx.rpos))
        else
            o.fire.SpreadAngle, o.spark.SpreadAngle = Vector2.new(25, 25), Vector2.new(25, 25)
            o.fire.Rate, o.spark.Rate = 60 * speedK, 40 * speedK
            local ang = t * 2.4
            local pos = cx.rpos + Vector3.new(math.cos(ang) * 3 * k, 0.5 + math.sin(t * 3) * 0.4, math.sin(ang) * 3 * k)
            local tan = Vector3.new(-math.sin(ang), 0, math.cos(ang))
            mv(o.part, CFrame.lookAt(pos, pos + tan))
        end
    end)

    ----------------------------------------------------------------------
    -- 12. Plasma arcs (video look)
    ----------------------------------------------------------------------
    def("Arcs", function()
        local o = newObj()
        o.arcs = {}
        for i = 1, 4 do
            local pa = mk(BALL, Vector3.new(0.1, 0.1, 0.1), nil, nil)
            local pb = mk(BALL, Vector3.new(0.1, 0.1, 0.1), nil, nil)
            local aa, ab = Instance.new("Attachment", pa), Instance.new("Attachment", pb)
            local bm = Instance.new("Beam")
            bm.Attachment0, bm.Attachment1 = aa, ab
            bm.Segments = 12
            bm.Width0, bm.Width1 = 0.16, 0.16
            bm.LightEmission = 1
            bm.LightInfluence = 0
            bm.FaceCamera = true
            bm.Transparency = NumberSequence.new(0.05)
            bm.Enabled = false
            bm.Parent = pa
            o.arcs[i] = {pa = pa, pb = pb, beam = bm, A = Vector3.zero, B = Vector3.zero}
        end
        o.acc = 1
        function o.vis(on)
            for _, ar in ipairs(o.arcs) do ar.beam.Enabled = on end
        end
        return o
    end, function(o, C, t, color, cx, dt)
        local a, k = C.Anim, C.Size
        o.acc += dt
        local refresh = o.acc > 0.06 / math.max(C.Speed, 0.3)
        if refresh then o.acc = 0 end
        local recolor = o.col ~= color
        o.col = color
        for _, ar in ipairs(o.arcs) do
            if refresh then
                if a == 1 then
                    ar.A, ar.B = rdir() * 2.4 * k + Vector3.new(0, 0.3, 0), rdir() * 2.4 * k + Vector3.new(0, 0.3, 0)
                elseif a == 2 then
                    ar.A, ar.B = Vector3.new(0, 2.4, 0) + rdir() * 1.3 * k, Vector3.new(0, 2.4, 0) + rdir() * 1.3 * k
                else
                    local rx, rz = math.random() - 0.5, math.random() - 0.5
                    ar.A, ar.B = Vector3.new(rx * 3.2, -2.4, rz * 3.2) * k, Vector3.new(-rx * 3.2, 2.4, -rz * 3.2) * k
                end
                ar.beam.CurveSize0, ar.beam.CurveSize1 = (math.random() - 0.5) * 3, (math.random() - 0.5) * 3
                local w = 0.08 + math.random() * 0.12
                ar.beam.Width0, ar.beam.Width1 = w, w
            end
            mv(ar.pa, CFrame.new(cx.rpos + ar.A))
            mv(ar.pb, CFrame.new(cx.rpos + ar.B))
            if recolor then ar.beam.Color = ColorSequence.new(WHITE:Lerp(color, 0.3), color) end
        end
    end)

    ----------------------------------------------------------------------
    -- 13. Neon grid floor (video look)
    ----------------------------------------------------------------------
    local gridRay = RaycastParams.new()
    gridRay.FilterType = Enum.RaycastFilterType.Exclude
    def("Grid", function()
        local o = newObj()
        for i = 1, 11 do mk(BLOCK, Vector3.new(44, 0.05, 0.14), nil, o, 0.3) end
        for i = 1, 11 do mk(BLOCK, Vector3.new(0.14, 0.05, 44), nil, o, 0.3) end
        o.gy, o.acc = nil, 1
        return o
    end, function(o, C, t, color, cx, dt)
        local a = C.Anim
        o.acc += dt
        if o.acc > 0.25 or not o.gy then
            o.acc = 0
            gridRay.FilterDescendantsInstances = {cx.char, E.folder}
            local hit = workspace:Raycast(cx.rpos, Vector3.new(0, -14, 0), gridRay)
            o.gy = hit and hit.Position.Y + 0.04 or cx.rpos.Y - 3
        end
        local sp = 4 * math.max(C.Size, 0.5)
        local px, pz = cx.rpos.X, cx.rpos.Z
        local ox = math.floor(px / sp + 0.5) * sp
        local oz = math.floor(pz / sp + 0.5) * sp
        local scroll = (a == 3) and ((t * 3) % sp) or 0
        local recolor = o.col ~= color
        o.col = color
        for i = -5, 5 do
            local zi, xi = oz + i * sp + scroll, ox + i * sp + scroll
            local pz1, px1 = o.parts[i + 6], o.parts[i + 17]
            local dz, dx = math.abs(zi - pz), math.abs(xi - px)
            local lim = sp * 5.5
            local tz = 0.2 + 0.8 * math.clamp(dz / lim, 0, 1) ^ 2
            local tx = 0.2 + 0.8 * math.clamp(dx / lim, 0, 1) ^ 2
            if a == 2 then
                tz = math.clamp(tz + 0.4 * (0.5 + 0.5 * math.sin(dz * 0.35 - t * 5)), 0, 1)
                tx = math.clamp(tx + 0.4 * (0.5 + 0.5 * math.sin(dx * 0.35 - t * 5)), 0, 1)
            end
            pz1.Transparency, px1.Transparency = tz, tx
            pz1.Size, px1.Size = Vector3.new(sp * 11, 0.05, 0.14), Vector3.new(0.14, 0.05, sp * 11)
            mv(pz1, CFrame.new(px, o.gy, zi))
            mv(px1, CFrame.new(xi, o.gy, pz))
            if recolor then pz1.Color, px1.Color = color, color end
        end
    end)

    ----------------------------------------------------------------------
    -- 18. Evade trail: long neon ribbons streaming from the feet / body
    ----------------------------------------------------------------------
    def("EvadeTrail", function()
        local o = newObj()
        o.trails, o.emitters = {}, {}
        -- 0 = left foot, 1 = right foot, 2 = torso, 3 = head (used by Fan)
        for i = 1, 4 do
            local p = mk(BLOCK, Vector3.new(0.2, 0.2, 0.2), nil, o, 1)
            local tr = trailOn(p, 0.22, i == 3 and 1.6 or 1.1)
            o.trails[i] = tr
        end
        local base = o.vis
        function o.vis(on)
            base(on)
            for _, tr in ipairs(o.trails) do tr.Enabled = on end
        end
        return o
    end, function(o, C, t, color, cx)
        local a, k = C.Anim, C.Size
        local recolor = o.col ~= color
        o.col = color
        local cf = cx.root.CFrame
        local sway = math.sin(t * 9) * 0.5
        local targets
        if a == 1 then
            -- twin trails right under the feet, Evade-style
            targets = {
                cf * CFrame.new(-0.55, -2.6, 0.25),
                cf * CFrame.new(0.55, -2.6, 0.25),
            }
        elseif a == 2 then
            -- one thick comet from the torso
            targets = {cf * CFrame.new(0, 0.2, 0.9), cf * CFrame.new(0, -1.2, 0.9)}
        else
            -- fan: three ribbons spread behind
            targets = {
                cf * CFrame.new(-1.1 - sway * 0.4, -0.6, 0.7),
                cf * CFrame.new(0, 0.4, 0.9),
                cf * CFrame.new(1.1 + sway * 0.4, -0.6, 0.7),
            }
        end
        local fadeK = math.clamp(cx.spd / 12, 0.15, 1)
        for i, p in ipairs(o.parts) do
            local goal = targets[i] or targets[#targets]
            if i <= #targets then
                mv(p, goal)
                local tr = o.trails[i]
                if a == 2 then
                    tr.Lifetime = 1.9 * k
                else
                    tr.Lifetime = (0.7 + fadeK * 0.9) * k
                end
                if recolor then
                    tr.Color = ColorSequence.new({
                        ColorSequenceKeypoint.new(0, color:Lerp(WHITE, 0.35)),
                        ColorSequenceKeypoint.new(0.6, color),
                        ColorSequenceKeypoint.new(1, color:Lerp(BLACK, 0.5)),
                    })
                end
                tr.Transparency = NumberSequence.new({
                    NumberSequenceKeypoint.new(0, 0.05 + (1 - fadeK) * 0.5),
                    NumberSequenceKeypoint.new(0.7, 0.45),
                    NumberSequenceKeypoint.new(1, 1),
                })
            else
                mv(p, CFrame.new(cx.rpos + Vector3.new(0, -300, 0)))
                o.trails[i].Enabled = false
                if o.active then o.trails[i].Enabled = false end
            end
        end
        -- re-enable only the trails this animation uses
        for i = 1, #targets do o.trails[i].Enabled = true end
    end)

    ----------------------------------------------------------------------
    -- 19. Afterimages: fading body copies left behind while moving
    ----------------------------------------------------------------------
    def("AfterImage", function()
        local o = newObj()
        o.ghosts = {}
        for i = 1, 5 do
            local g = {
                head = mk(BALL, Vector3.new(1.1, 1.1, 1.1), nil, o, 1),
                torso = mk(BLOCK, Vector3.new(1.7, 1.9, 0.9), nil, o, 1),
                legs = mk(BLOCK, Vector3.new(1.5, 1.7, 0.8), nil, o, 1),
            }
            o.ghosts[i] = g
        end
        o.hist, o.acc = {}, 0
        return o
    end, function(o, C, t, color, cx, dt)
        local a = C.Anim
        local recolor = o.col ~= color
        o.col = color
        -- record the root pose at a fixed rate
        o.acc += dt * C.Speed
        local step = 0.055
        while o.acc >= step do
            o.acc -= step
            table.insert(o.hist, 1, cx.root.CFrame)
            if #o.hist > 40 then table.remove(o.hist) end
        end
        local active = (a == 3) and (cx.spd > 12) or (cx.spd > 2)
        for i, g in ipairs(o.ghosts) do
            local idx = i * 6 + 2
            local cf = o.hist[idx]
            if active and cf then
                local f = 1 - i / (#o.ghosts + 1)            -- 1 = newest, fading out
                local tr = 1 - f * 0.55                       -- older = more transparent
                if a == 2 then
                    local ang = t * 2 + i * 0.9
                    cf = cf * CFrame.new(math.cos(ang) * 0.6 * i, math.sin(t * 3 + i) * 0.3, math.sin(ang) * 0.6 * i)
                end
                mv(g.head, cf * CFrame.new(0, 1.55, 0))
                mv(g.torso, cf)
                mv(g.legs, cf * CFrame.new(0, -1.8, 0))
                g.head.Transparency, g.torso.Transparency, g.legs.Transparency = tr, tr, tr + 0.1
                if recolor then
                    local c = color:Lerp(WHITE, 0.25)
                    g.head.Color, g.torso.Color, g.legs.Color = c, color, color:Lerp(BLACK, 0.3)
                end
            else
                g.head.Transparency, g.torso.Transparency, g.legs.Transparency = 1, 1, 1
            end
        end
    end)

    ----------------------------------------------------------------------
    -- 20. Air ribbons: thin light ribbons twisting behind in the air
    ----------------------------------------------------------------------
    def("AirRibbons", function()
        local o = newObj()
        o.trails = {}
        for i = 1, 3 do
            local p = mk(BLOCK, Vector3.new(0.15, 0.15, 0.15), nil, o, 1)
            local tr = trailOn(p, 0.1, 1.4)
            tr.WidthScale = NumberSequence.new({
                NumberSequenceKeypoint.new(0, 0.4),
                NumberSequenceKeypoint.new(0.3, 1),
                NumberSequenceKeypoint.new(1, 0),
            })
            o.trails[i] = tr
        end
        local base = o.vis
        function o.vis(on)
            base(on)
            for _, tr in ipairs(o.trails) do tr.Enabled = on end
        end
        return o
    end, function(o, C, t, color, cx)
        local a, k = C.Anim, C.Size
        local recolor = o.col ~= color
        o.col = color
        local cf = cx.root.CFrame
        local spread = (a == 3) and 2.6 or 1.5
        for i, p in ipairs(o.parts) do
            local ph = i / 3 * TAU
            local ang = (a == 2) and (t * 5 + ph) or (t * 2.2 + ph)
            local y = math.sin(t * 3.1 + ph * 2) * 1.4
            local off = Vector3.new(math.cos(ang) * spread * k, y, math.sin(ang) * spread * k * 0.6 + 0.8)
            mv(p, cf * CFrame.new(off))
            local tr = o.trails[i]
            tr.Lifetime = 1.1 * k + 0.3 * math.sin(t + ph)
            if recolor then
                local c = (i == 2) and color:Lerp(WHITE, 0.5) or color
                tr.Color = ColorSequence.new(c, color:Lerp(BLACK, 0.4))
            end
        end
    end)

    ----------------------------------------------------------------------
    -- 21. Dust kick: soft dust puffs while running and on landing
    ----------------------------------------------------------------------
    def("DustKick", function()
        local o = newObj()
        o.puffs = {}
        for i = 1, 14 do
            local p = mk(BALL, Vector3.new(0.6, 0.6, 0.6), Enum.Material.SmoothPlastic, o, 1)
            o.puffs[i] = {p = p, age = 9, life = 1, from = Vector3.new(), vel = Vector3.new()}
        end
        o.next, o.stepAcc, o.prevVy = 1, 0, 0
        return o
    end, function(o, C, t, color, cx, dt)
        local a, k = C.Anim, C.Size
        local recolor = o.col ~= color
        o.col = color
        local function spawn(n, power)
            for _ = 1, n do
                local pf = o.puffs[o.next]
                o.next = o.next % #o.puffs + 1
                pf.age, pf.life = 0, 0.55 + math.random() * 0.4
                pf.from = cx.rpos + Vector3.new((math.random() - 0.5) * 1.4, -2.7, (math.random() - 0.5) * 1.4)
                local ang = math.random() * TAU
                pf.vel = Vector3.new(math.cos(ang) * power, 1.6 + math.random() * power, math.sin(ang) * power)
            end
        end
        local run = (a ~= 2) and cx.spd > 8
        local land = (a ~= 1) and (o.prevVy < -28 and cx.root.AssemblyLinearVelocity.Y > -6)
        o.prevVy = cx.root.AssemblyLinearVelocity.Y
        o.stepAcc += dt * C.Speed
        if run and o.stepAcc > 0.12 then
            o.stepAcc = 0
            spawn(2, 2.2)
        end
        if land then spawn(8, 4.5) end
        for _, pf in ipairs(o.puffs) do
            if pf.age < pf.life then
                pf.age += dt
                local u = math.clamp(pf.age / pf.life, 0, 1)
                local pos = pf.from + pf.vel * pf.age
                local s = (0.5 + u * 1.9) * k
                pf.p.Size = Vector3.new(s, s * 0.8, s)
                pf.p.Transparency = 0.55 + u * 0.45
                mv(pf.p, CFrame.new(pos))
                if recolor then pf.p.Color = color:Lerp(WHITE, 0.55) end
            elseif pf.p.Transparency < 1 then
                pf.p.Transparency = 1
            end
        end
    end)

    ----------------------------------------------------------------------
    -- v14 EPIC VFX: shockwave, meteors, light pillar, black hole, dragon, sigil
    ----------------------------------------------------------------------
    local EPIC_RAY = RaycastParams.new()
    EPIC_RAY.FilterType = Enum.RaycastFilterType.Exclude
    local METEOR_SKY = Vector3.new(58, 130, 36)

    -- camera punch (FOV) + shake, decays in the driver
    local function addKick(kick, shake)
        E.kick = math.max(E.kick or 0, kick or 0)
        E.shake = math.max(E.shake or 0, shake or 0)
    end

    local function groundAt(pos, cx, up, down)
        EPIC_RAY.FilterDescendantsInstances = {cx.char, E.folder}
        local hit = workspace:Raycast(pos + Vector3.new(0, up, 0), Vector3.new(0, -(up + down), 0), EPIC_RAY)
        return hit and hit.Position or nil
    end

    local function easeOut(u)
        u = math.clamp(u, 0, 1)
        return 1 - (1 - u) ^ 3
    end

    local function hotSeq(c)
        return ColorSequence.new({
            ColorSequenceKeypoint.new(0, c:Lerp(WHITE, 0.7)),
            ColorSequenceKeypoint.new(0.4, c),
            ColorSequenceKeypoint.new(1, c:Lerp(BLACK, 0.55)),
        })
    end

    local function sparkEmitter(parent, rate, life, spdA, spdB, size)
        local e = Instance.new("ParticleEmitter")
        e.Texture = SPARK_TEX
        e.Rate = rate
        e.Lifetime = NumberRange.new(life * 0.7, life)
        e.Speed = NumberRange.new(spdA, spdB)
        e.SpreadAngle = Vector2.new(15, 15)
        e.LightEmission = 1
        e.LightInfluence = 0
        e.Rotation = NumberRange.new(0, 360)
        e.RotSpeed = NumberRange.new(-120, 120)
        e.Size = NumberSequence.new({NumberSequenceKeypoint.new(0, size), NumberSequenceKeypoint.new(1, 0)})
        e.Transparency = NumberSequence.new({
            NumberSequenceKeypoint.new(0, 0),
            NumberSequenceKeypoint.new(0.75, 0.2),
            NumberSequenceKeypoint.new(1, 1),
        })
        e.Enabled = false
        e.Parent = parent
        return e
    end

    local function newLight(parent, range)
        local l = Instance.new("PointLight")
        l.Range = range
        l.Brightness = 0
        l.Shadows = false
        l.Enabled = false
        l.Parent = parent
        return l
    end

    -- extra on/off work on top of the default o.vis
    local function hookVis(o, fn)
        local base = o.vis
        function o.vis(on)
            base(on)
            fn(on)
        end
    end

    -- Hollow glowing ring lying flat on a thin part (SurfaceGui + UIStroke). both = visible from below too.
    local function newRing(o, pps, both)
        local p = mk(BLOCK, Vector3.new(1, 0.05, 1), Enum.Material.SmoothPlastic, o, 1)
        local r = {part = p, guis = {}, strokes = {}, mix = {}, on = false}
        local faces = both and {Enum.NormalId.Top, Enum.NormalId.Bottom} or {Enum.NormalId.Top}
        for _, face in ipairs(faces) do
            local g = Instance.new("SurfaceGui")
            g.Face = face
            g.SizingMode = Enum.SurfaceGuiSizingMode.PixelsPerStud
            g.PixelsPerStud = pps or 16
            g.LightInfluence = 0
            g.Brightness = 3
            g.ClipsDescendants = false
            g.Enabled = false
            g.Adornee = p
            g.Parent = p
            table.insert(r.guis, g)
            for _, spec in ipairs({{1, 5, 0}, {0.9, 2, 0.7}}) do
                local f = Instance.new("Frame")
                f.AnchorPoint = Vector2.new(0.5, 0.5)
                f.Position = UDim2.fromScale(0.5, 0.5)
                f.Size = UDim2.fromScale(spec[1], spec[1])
                f.BackgroundTransparency = 1
                f.BorderSizePixel = 0
                f.Parent = g
                local uc = Instance.new("UICorner")
                uc.CornerRadius = UDim.new(0.5, 0)
                uc.Parent = f
                local st = Instance.new("UIStroke")
                st.Thickness = spec[2]
                st.Transparency = 1
                st.Parent = f
                table.insert(r.strokes, st)
                table.insert(r.mix, spec[3])
            end
        end
        return r
    end

    local function hideRing(r)
        if r.on then
            r.on = false
            for _, g in ipairs(r.guis) do g.Enabled = false end
        end
    end

    -- tr: 0 = solid, 1 = invisible
    local function ringSet(r, cf, dia, tr, color)
        if tr >= 0.97 or dia < 0.3 then
            hideRing(r)
            return
        end
        if not r.on then
            r.on = true
            for _, g in ipairs(r.guis) do g.Enabled = true end
        end
        r.part.Size = Vector3.new(dia, 0.05, dia)
        mv(r.part, cf)
        local recolor = r.col ~= color
        r.col = color
        for i, st in ipairs(r.strokes) do
            st.Transparency = math.clamp(tr + r.mix[i] * 0.3, 0, 1)
            if recolor then st.Color = color:Lerp(WHITE, r.mix[i]) end
        end
    end

    ----------------------------------------------------------------------
    -- 22. Shockwave: giant ring + glowing ground cracks + flying rubble (landing / rhythm / sprint)
    ----------------------------------------------------------------------
    local function hideWave(wv)
        wv.done = true
        hideRing(wv.r1)
        hideRing(wv.r2)
        for _, cp in ipairs(wv.cracks) do cp.Transparency = 1 end
        for _, d in ipairs(wv.debris) do d.p.Transparency = 1 end
    end

    local function shockFire(o, k, cx, power)
        local g = groundAt(cx.rpos, cx, 3, 12)
        local wv = o.waves[o.next]
        o.next = o.next % #o.waves + 1
        wv.age, wv.life, wv.pw, wv.done = 0, 1.25, power, false
        wv.pos = (g or (cx.rpos - Vector3.new(0, 2.9, 0))) + Vector3.new(0, 0.08, 0)
        wv.seed = math.random() * TAU
        wv.col = nil
        for _, d in ipairs(wv.debris) do
            local ang = math.random() * TAU
            local out = (5 + math.random() * 11) * k * power
            d.v = Vector3.new(math.cos(ang) * out, (10 + math.random() * 13) * power, math.sin(ang) * out)
            d.spin = Vector3.new(math.random() * 8 - 4, math.random() * 8 - 4, math.random() * 8 - 4)
            local s = (0.35 + math.random() * 0.6) * k
            d.p.Size = Vector3.new(s, s, s)
        end
        addKick(5 * power, 0.55 * power)
    end

    def("Shockwave", function()
        local o = newObj()
        o.rings, o.waves = {}, {}
        for w = 1, 3 do
            local wv = {age = 99, life = 1.25, pos = Vector3.zero, pw = 1, seed = 0, done = true, cracks = {}, debris = {}}
            wv.r1, wv.r2 = newRing(o, 14), newRing(o, 14)
            table.insert(o.rings, wv.r1)
            table.insert(o.rings, wv.r2)
            for i = 1, 6 do
                wv.cracks[i] = mk(BLOCK, Vector3.new(0.2, 0.06, 1), nil, o, 1)
            end
            for i = 1, 7 do
                local neon = i % 2 == 0
                wv.debris[i] = {
                    p = mk(BLOCK, Vector3.new(0.6, 0.6, 0.6), neon and Enum.Material.Neon or Enum.Material.Slate, o, 1),
                    neon = neon, v = Vector3.zero, spin = Vector3.zero,
                }
            end
            o.waves[w] = wv
        end
        o.next, o.acc, o.sprint = 1, 0, false
        hookVis(o, function(on)
            if not on then
                for _, wv in ipairs(o.waves) do hideWave(wv) end
            end
        end)
        return o
    end, function(o, C, t, color, cx, dt)
        local a, k = C.Anim, C.Size
        if a == 1 then
            if cx.landed then shockFire(o, k, cx, cx.landP) end
        elseif a == 2 then
            o.acc += dt * C.Speed
            if o.acc >= 1.5 then
                o.acc = 0
                shockFire(o, k, cx, 1)
            end
        else
            local run = cx.spd > 15
            if run and not o.sprint then shockFire(o, k, cx, 1.15) end
            o.sprint = run
            o.acc += dt * C.Speed
            if run and o.acc >= 0.6 then
                o.acc = 0
                shockFire(o, k, cx, 0.6)
            end
        end
        for _, wv in ipairs(o.waves) do
            if not wv.done then
                wv.age += dt
                local u = math.clamp(wv.age / wv.life, 0, 1)
                local pw = wv.pw
                local recolor = wv.col ~= color
                wv.col = color
                -- two expanding rings, the second one slightly late and smaller
                local R1 = 36 * k * pw
                ringSet(wv.r1, CFrame.new(wv.pos), 2 + R1 * easeOut(u), u ^ 1.6 * 0.95, color)
                local u2 = math.clamp((wv.age - 0.14) / wv.life, 0, 1)
                ringSet(wv.r2, CFrame.new(wv.pos + Vector3.new(0, 0.03, 0)), 1 + R1 * 0.68 * easeOut(u2),
                    wv.age < 0.14 and 1 or (u2 ^ 1.3 * 0.95), color:Lerp(WHITE, 0.45))
                -- glowing cracks running out along the ground
                local rr = easeOut(u) * 18 * k * pw
                local n = #wv.cracks
                for i, cp in ipairs(wv.cracks) do
                    local ang = wv.seed + i / n * TAU + (i % 2) * 0.2
                    local dir = Vector3.new(math.cos(ang), 0, math.sin(ang))
                    local len = (2.6 + (i % 3) * 1.1) * k * pw * (1 - u * 0.5)
                    local c0 = wv.pos + dir * (rr * (0.55 + (i % 3) * 0.15) + len / 2) + Vector3.new(0, 0.1, 0)
                    cp.Size = Vector3.new(0.22 * k, 0.06, len)
                    cp.Transparency = 0.05 + u * u * 0.95
                    mv(cp, CFrame.lookAt(c0, c0 + dir))
                    if recolor then cp.Color = color:Lerp(WHITE, 0.3) end
                end
                -- rubble thrown into the air
                for _, d in ipairs(wv.debris) do
                    local pos = wv.pos + d.v * wv.age + Vector3.new(0, -27.5 * wv.age * wv.age, 0)
                    if pos.Y < wv.pos.Y + 0.2 then pos = Vector3.new(pos.X, wv.pos.Y + 0.2, pos.Z) end
                    d.p.Transparency = math.clamp((u - 0.55) / 0.45, 0, 1)
                    mv(d.p, CFrame.new(pos) * CFrame.Angles(d.spin.X * wv.age, d.spin.Y * wv.age, d.spin.Z * wv.age))
                    if recolor then d.p.Color = d.neon and color or color:Lerp(BLACK, 0.7) end
                end
                if wv.age >= wv.life then hideWave(wv) end
            end
        end
    end)

    ----------------------------------------------------------------------
    -- 23. Meteors: burning rocks fall from the sky and explode around you
    ----------------------------------------------------------------------
    def("Meteors", function()
        local o = newObj()
        o.m = {}
        for i = 1, 6 do
            local m = {
                core = mk(BALL, Vector3.new(1.4, 1.4, 1.4), nil, o, 1),
                glow = mk(BALL, Vector3.new(3, 3, 3), nil, o, 1),
                boom = mk(BALL, Vector3.new(1, 1, 1), nil, o, 1),
                ring = newRing(o, 14),
                phase = 0, age = 0, life = 1, arm = 0, pw = 1,
                start = Vector3.zero, tgt = Vector3.zero,
            }
            m.trail = trailOn(m.core, 0.7, 0.6)
            m.trail.Enabled = false
            m.sparks = sparkEmitter(m.boom, 0, 1.1, 14, 34, 0.55)
            m.sparks.SpreadAngle = Vector2.new(70, 70)
            m.sparks.Acceleration = Vector3.new(0, -45, 0)
            m.light = newLight(m.boom, 28)
            o.m[i] = m
        end
        o.acc = 0
        hookVis(o, function(on)
            if not on then
                for _, m in ipairs(o.m) do
                    m.phase = 0
                    m.trail.Enabled = false
                    m.light.Enabled = false
                    hideRing(m.ring)
                end
            end
        end)
        return o
    end, function(o, C, t, color, cx, dt)
        local a, k = C.Anim, C.Size
        local interval = (a == 2) and 0.28 or ((a == 3) and 1.6 or 0.75)
        local fallT = (a == 2) and 0.7 or ((a == 3) and 1.7 or 1.0)
        local big = (a == 3) and 1.9 or 1
        o.acc += dt * C.Speed
        if o.acc >= interval * (0.6 + math.random() * 0.8) then
            o.acc = 0
            for _, m in ipairs(o.m) do
                if m.phase == 0 then
                    local ang = math.random() * TAU
                    local rad = 10 + math.random() * 30
                    local base = cx.rpos + Vector3.new(math.cos(ang) * rad, 0, math.sin(ang) * rad)
                    local hit = groundAt(base, cx, 70, 160)
                    m.tgt = hit or Vector3.new(base.X, cx.rpos.Y - 3, base.Z)
                    m.start = m.tgt + METEOR_SKY
                    m.phase, m.age, m.arm = 1, 0, 2
                    m.life = fallT * (0.85 + math.random() * 0.3)
                    m.pw = big * (0.8 + math.random() * 0.5)
                    break
                end
            end
        end
        for _, m in ipairs(o.m) do
            if m.col ~= color then
                m.col = color
                m.core.Color = WHITE:Lerp(color, 0.25)
                m.glow.Color = color
                m.boom.Color = color:Lerp(WHITE, 0.35)
                m.trail.Color = hotSeq(color)
                m.sparks.Color = hotSeq(color)
                m.light.Color = color
            end
            if m.phase == 1 then
                -- jump to the sky with the trail off for two frames (no streak across the map)
                m.trail.Enabled = false
                m.core.Transparency, m.glow.Transparency = 1, 1
                mv(m.core, CFrame.new(m.start))
                mv(m.glow, CFrame.new(m.start))
                mv(m.boom, CFrame.new(m.tgt))
                m.arm -= 1
                if m.arm <= 0 then
                    m.phase, m.age = 2, 0
                    m.trail.Enabled = true
                end
            elseif m.phase == 2 then
                m.age += dt
                local u = math.clamp(m.age / m.life, 0, 1)
                local pos = m.start:Lerp(m.tgt, u ^ 1.25)
                local s = 1.5 * k * m.pw
                m.core.Size = Vector3.new(s, s, s)
                m.glow.Size = Vector3.new(s * 2.3, s * 2.3, s * 2.3)
                m.core.Transparency, m.glow.Transparency = 0, 0.65
                mv(m.core, CFrame.new(pos))
                mv(m.glow, CFrame.new(pos))
                if u >= 1 then
                    m.phase, m.age = 3, 0
                    m.core.Transparency, m.glow.Transparency = 1, 1
                    m.sparks:Emit(math.floor(22 * m.pw))
                    m.light.Enabled = true
                    local d = (m.tgt - cx.rpos).Magnitude
                    if d < 36 then addKick(2 * (1 - d / 36), 0.5 * (1 - d / 36) * m.pw) end
                end
            elseif m.phase == 3 then
                m.age += dt
                local u = math.clamp(m.age / 0.9, 0, 1)
                local s = (1.5 + 10 * easeOut(u)) * k * m.pw
                m.boom.Size = Vector3.new(s, s, s)
                m.boom.Transparency = 0.1 + 0.9 * u
                mv(m.boom, CFrame.new(m.tgt + Vector3.new(0, s * 0.25, 0)))
                ringSet(m.ring, CFrame.new(m.tgt + Vector3.new(0, 0.1, 0)), 2 + 22 * k * m.pw * easeOut(u), u ^ 1.4, color)
                m.light.Brightness = 6 * (1 - u) * m.pw
                if m.age >= 1.0 then
                    m.phase = 0
                    m.light.Enabled = false
                    m.boom.Transparency = 1
                    hideRing(m.ring)
                end
            end
        end
    end)

    ----------------------------------------------------------------------
    -- 24. Light pillar: a column of light from the sky, energy rings sucked into its base
    ----------------------------------------------------------------------
    local PILLAR_H = 260
    local function setCyl(p, base, d, tr)
        p.Size = Vector3.new(PILLAR_H, d, d)
        p.Transparency = tr
        mv(p, base * CFrame.new(0, PILLAR_H / 2, 0) * CFrame.Angles(0, 0, math.pi / 2))
    end
    local function hideCol(col)
        if col.on then
            col.on = false
            col.sparks.Enabled = false
            col.light.Enabled = false
            for _, r in ipairs(col.r) do hideRing(r) end
        end
        col.core.Transparency, col.mid.Transparency, col.shell.Transparency = 1, 1, 1
    end

    def("Pillar", function()
        local o = newObj()
        o.cols = {}
        for c = 1, 2 do
            local col = {
                core = mk(CYL, Vector3.new(PILLAR_H, 0.8, 0.8), nil, o, 1),
                mid = mk(CYL, Vector3.new(PILLAR_H, 2, 2), nil, o, 1),
                shell = mk(CYL, Vector3.new(PILLAR_H, 4, 4), nil, o, 1),
                base = mk(BLOCK, Vector3.new(5, 0.2, 5), Enum.Material.SmoothPlastic, o, 1),
                r = {newRing(o, 14), newRing(o, 14), newRing(o, 14)},
                on = false,
            }
            col.sparks = sparkEmitter(col.base, 38, 1.7, 10, 22, 0.55)
            col.sparks.SpreadAngle = Vector2.new(4, 4)
            col.sparks.Acceleration = Vector3.new(0, 6, 0)
            col.light = newLight(col.base, 24)
            o.cols[c] = col
        end
        o.acc = 1
        hookVis(o, function(on)
            if not on then
                for _, col in ipairs(o.cols) do hideCol(col) end
            end
        end)
        return o
    end, function(o, C, t, color, cx, dt)
        local a, k = C.Anim, C.Size
        o.acc += dt
        if o.acc > 0.2 or not o.gyT then
            o.acc = 0
            local gp = groundAt(cx.rpos, cx, 3, 14)
            o.gyT = gp and gp.Y or (cx.rpos.Y - 2.9)
            o.gy = o.gy or o.gyT
        end
        o.gy += (o.gyT - o.gy) * math.min(1, dt * 12)
        local gy = o.gy
        local n = (a == 1) and 1 or 2
        local pulse = 1 + 0.12 * math.sin(t * 5) + 0.05 * math.sin(t * 13)
        local w = (a == 3) and 0.55 or 1
        local recolor = o.col ~= color
        o.col = color
        for ci, col in ipairs(o.cols) do
            if ci > n then
                hideCol(col)
            else
                if not col.on then
                    col.on = true
                    col.sparks.Enabled = true
                    col.light.Enabled = true
                end
                local origin, yaw, tilt
                if a == 1 then
                    origin, yaw, tilt = Vector3.new(cx.rpos.X, gy, cx.rpos.Z), 0, 0
                elseif a == 2 then
                    local side = (ci == 1) and -1 or 1
                    local off = cx.root.CFrame.RightVector * (5.2 * k * side)
                    origin, yaw, tilt = Vector3.new(cx.rpos.X + off.X, gy, cx.rpos.Z + off.Z), 0, 0
                else
                    origin = Vector3.new(cx.rpos.X, gy, cx.rpos.Z)
                    yaw = t * 0.9 + (ci - 1) * math.pi
                    tilt = math.rad(24) + 0.08 * math.sin(t * 1.7)
                end
                local base = CFrame.new(origin) * CFrame.Angles(0, yaw, 0) * CFrame.Angles(tilt, 0, 0)
                local kk = k * pulse * w
                setCyl(col.core, base, 0.7 * kk, 0.04)
                setCyl(col.mid, base, 1.9 * kk, 0.38)
                setCyl(col.shell, base, 3.8 * kk, 0.78)
                col.base.Size = Vector3.new(5 * k, 0.2, 5 * k)
                mv(col.base, CFrame.new(origin + Vector3.new(0, 0.2, 0)))
                col.light.Brightness = 3 * pulse
                col.light.Range = 22 * k
                -- energy rings shrink into the base
                for ri, r in ipairs(col.r) do
                    local ph = (t * 0.55 + ri / 3) % 1
                    ringSet(r, CFrame.new(origin.X, gy + 0.1, origin.Z), 2 + 15 * k * (1 - ph),
                        1 - math.sin(ph * math.pi) ^ 0.7 * 0.92, color)
                end
                if recolor then
                    col.core.Color = WHITE:Lerp(color, 0.15)
                    col.mid.Color = color:Lerp(WHITE, 0.2)
                    col.shell.Color = color
                    col.sparks.Color = hotSeq(color)
                    col.light.Color = color
                end
            end
        end
    end)

    ----------------------------------------------------------------------
    -- 25. Black hole: dark core, tilted glowing disk, matter spiralling in, particles pulled inward
    ----------------------------------------------------------------------
    def("BlackHole", function()
        local o = newObj()
        o.core = mk(BALL, Vector3.new(3, 3, 3), Enum.Material.SmoothPlastic, o, 0)
        o.core.Color = Color3.fromRGB(4, 3, 8)
        o.rim = mk(BALL, Vector3.new(3.6, 3.6, 3.6), nil, o, 0.72)
        o.disk = {newRing(o, 12, true), newRing(o, 12, true), newRing(o, 12, true)}
        o.spots = {}
        for i = 1, 7 do
            local p = mk(BALL, Vector3.new(0.5, 0.5, 0.5), nil, o, 1)
            local tr = trailOn(p, 0.3, 0.55)
            o.spots[i] = {p = p, tr = tr, cool = 3, last = 0}
        end
        o.anchor = mk(BLOCK, Vector3.new(12, 12, 12), Enum.Material.SmoothPlastic, o, 1)
        o.pull = sparkEmitter(o.anchor, 0, 1.0, 6, 8, 0.4)
        o.pull.SpreadAngle = Vector2.new(0, 0)
        o.okShape = pcall(function()
            o.pull.Shape = Enum.ParticleEmitterShape.Sphere
            o.pull.ShapeInOut = Enum.ParticleEmitterShapeInOut.Inward
            o.pull.ShapeStyle = Enum.ParticleEmitterShapeStyle.Surface
        end)
        o.light = newLight(o.anchor, 26)
        hookVis(o, function(on)
            o.pull.Enabled = on and o.okShape
            o.pull.Rate = o.okShape and 36 or 0
            o.light.Enabled = on
            for _, s in ipairs(o.spots) do
                s.tr.Enabled = false
                s.cool = 3
            end
            if not on then
                for _, r in ipairs(o.disk) do hideRing(r) end
            end
        end)
        return o
    end, function(o, C, t, color, cx, dt)
        local a, k = C.Anim, C.Size
        local cf0, axis
        if a == 1 then
            cf0 = CFrame.new(cx.rpos + Vector3.new(0, 7.5 * k + math.sin(t * 1.3) * 0.5, 0))
            axis = CFrame.new(cf0.Position) * CFrame.Angles(0, t * 0.35, 0) * CFrame.Angles(math.rad(24), 0, 0)
        elseif a == 2 then
            cf0 = cx.root.CFrame * CFrame.new(0, 2.2, 6.5 * k)
            axis = cf0 * CFrame.Angles(math.rad(78), 0, t * 0.35)
        else
            local ang = t * 0.55
            cf0 = CFrame.new(cx.rpos + Vector3.new(math.cos(ang) * 11 * k, 3.5 + math.sin(t) * 0.8, math.sin(ang) * 11 * k))
            axis = CFrame.new(cf0.Position) * CFrame.Angles(0, t * 0.35, 0) * CFrame.Angles(math.rad(34), 0, 0)
        end
        local center = cf0.Position
        local recolor = o.col ~= color
        o.col = color
        local cs = 2.6 * k
        o.core.Size = Vector3.new(cs, cs, cs)
        mv(o.core, CFrame.new(center))
        local rs = 3.5 * k * (1 + 0.05 * math.sin(t * 4))
        o.rim.Size = Vector3.new(rs, rs, rs)
        mv(o.rim, CFrame.new(center))
        for i, r in ipairs(o.disk) do
            local wob = axis * CFrame.Angles(0.12 * math.sin(t * 0.9 + i), 0.12 * math.cos(t * 0.7 + i * 2), 0)
            ringSet(r, wob, (5.2 + i * 2.6) * k, 0.12 + (i - 1) * 0.14 + 0.08 * math.sin(t * 3 + i), color)
        end
        -- matter falling into the hole along the disk
        local ns = #o.spots
        for i, s in ipairs(o.spots) do
            local ph = (t * 0.22 + i / ns) % 1
            if ph < s.last - 0.5 then
                s.tr.Enabled = false
                s.cool = 3
            end
            s.last = ph
            if s.cool > 0 then
                s.cool -= 1
                if s.cool == 0 and o.active then s.tr.Enabled = true end
            end
            local r = (9.5 - 7.4 * ph ^ 1.5) * k
            local th = i * 0.9 + ph * 9 + t * 0.5
            local sz = (0.55 - 0.3 * ph) * k
            s.p.Size = Vector3.new(sz, sz, sz)
            s.p.Transparency = 0.05 + ph ^ 4 * 0.95
            mv(s.p, axis * CFrame.new(math.cos(th) * r, 0, math.sin(th) * r))
            if recolor then
                s.p.Color = color:Lerp(WHITE, 0.4)
                s.tr.Color = hotSeq(color)
            end
        end
        o.anchor.Size = Vector3.new(12 * k, 12 * k, 12 * k)
        mv(o.anchor, CFrame.new(center))
        o.light.Brightness = 2.5 + math.sin(t * 3)
        if recolor then
            o.rim.Color = color
            o.pull.Color = hotSeq(color)
            o.light.Color = color
        end
    end)

    ----------------------------------------------------------------------
    -- 26. Energy dragon: a glowing serpent coils around you, follows you or draws a figure eight
    ----------------------------------------------------------------------
    def("Dragon", function()
        local o = newObj()
        o.n = 30
        o.seg, o.pos = {}, {}
        for i = 1, o.n do
            o.seg[i] = mk(BALL, Vector3.new(1, 1, 1), nil, o, 1)
            o.pos[i] = Vector3.zero
        end
        o.hornL = mk(BLOCK, Vector3.new(0.18, 0.18, 1.2), nil, o, 1)
        o.hornR = mk(BLOCK, Vector3.new(0.18, 0.18, 1.2), nil, o, 1)
        o.eyeL = mk(BALL, Vector3.new(0.3, 0.3, 0.3), nil, o, 1)
        o.eyeR = mk(BALL, Vector3.new(0.3, 0.3, 0.3), nil, o, 1)
        o.eyeL.Color, o.eyeR.Color = WHITE, WHITE
        o.tr = trailOn(o.seg[1], 0.5, 0.7)
        o.fire = sparkEmitter(o.seg[1], 24, 0.7, 2, 7, 0.5)
        o.fire.SpreadAngle = Vector2.new(45, 45)
        o.init, o.cool = false, 3
        hookVis(o, function(on)
            o.init = false
            o.tr.Enabled = false
            o.cool = 3
            o.fire.Enabled = on
        end)
        return o
    end, function(o, C, t, color, cx, dt)
        local a, k = C.Anim, C.Size
        local N = o.n
        local rp = cx.rpos
        local target
        if a == 1 then
            local ang = t * 1.7
            target = rp + Vector3.new(math.cos(ang) * 3.4 * k, 0.3 + math.sin(t * 1.1) * 2.2 * k, math.sin(ang) * 3.4 * k)
        elseif a == 2 then
            target = (cx.root.CFrame * CFrame.new(2.6 * k + math.sin(t * 1.3) * 1.2, 2.8 + math.sin(t * 2.1) * 0.9,
                3.6 * k + math.cos(t * 0.9) * 1.2)).Position
        else
            local th = t * 0.8
            local den = 1 + math.sin(th) ^ 2
            target = rp + Vector3.new(7 * k * math.cos(th) / den, 1.4 + math.sin(th * 2) * 1.5 * k,
                7 * k * math.sin(th) * math.cos(th) / den)
        end
        if not o.init or (o.pos[1] - target).Magnitude > 60 then
            o.init = true
            for i = 1, N do o.pos[i] = target + Vector3.new(i * 0.6, 0, 0) end
            o.tr.Enabled = false
            o.cool = 3
        end
        if o.cool > 0 then
            o.cool -= 1
            if o.cool == 0 then o.tr.Enabled = true end
        end
        -- head chases the path, every segment keeps a fixed distance to the one in front of it
        o.pos[1] = o.pos[1]:Lerp(target, math.min(1, dt * (a == 2 and 7 or 20)))
        local sp = 0.78 * k
        for i = 2, N do
            local u = (i - 1) / (N - 1)
            local d = o.pos[i] - o.pos[i - 1]
            local m = d.Magnitude
            if m < 1e-3 then d, m = Vector3.zAxis, 1 end
            o.pos[i] = o.pos[i - 1] + d / m * (sp * (1 - 0.35 * u))
        end
        local recolor = o.col ~= color
        o.col = color
        for i = 2, N do
            local u = (i - 1) / (N - 1)
            local s = o.seg[i]
            local size = k * (1.25 - 1.0 * u ^ 0.85) + 0.18
            s.Size = Vector3.new(size, size, size)
            s.Transparency = (i % 2 == 0) and 0.05 or 0.3
            mv(s, CFrame.new(o.pos[i]))
            if recolor then s.Color = color:Lerp(BLACK, 0.5 * u):Lerp(WHITE, 0.25 * (1 - u)) end
        end
        -- head, horns and eyes
        local fwd = o.pos[1] - o.pos[2]
        if fwd.Magnitude < 1e-3 then fwd = Vector3.zAxis end
        local hcf = CFrame.lookAt(o.pos[1], o.pos[1] + fwd.Unit)
        local head = o.seg[1]
        local hs = 1.9 * k
        head.Size = Vector3.new(hs, hs, hs)
        head.Transparency = 0
        mv(head, hcf)
        o.hornL.Transparency, o.hornR.Transparency = 0.1, 0.1
        o.eyeL.Transparency, o.eyeR.Transparency = 0, 0
        mv(o.hornL, hcf * CFrame.new(-0.45 * k, 0.65 * k, 0.55 * k) * CFrame.Angles(math.rad(-30), math.rad(15), 0))
        mv(o.hornR, hcf * CFrame.new(0.45 * k, 0.65 * k, 0.55 * k) * CFrame.Angles(math.rad(-30), math.rad(-15), 0))
        mv(o.eyeL, hcf * CFrame.new(-0.42 * k, 0.25 * k, -0.75 * k))
        mv(o.eyeR, hcf * CFrame.new(0.42 * k, 0.25 * k, -0.75 * k))
        if recolor then
            head.Color = WHITE:Lerp(color, 0.3)
            o.hornL.Color, o.hornR.Color = color:Lerp(WHITE, 0.6), color:Lerp(WHITE, 0.6)
            o.tr.Color = hotSeq(color)
            o.fire.Color = hotSeq(color)
        end
    end)

    ----------------------------------------------------------------------
    -- 27. Sigil: a big magic circle on the ground (hexagram / pentagram / rising halos)
    ----------------------------------------------------------------------
    local function sigilXZ(R, ang, yaw)
        local x, z = math.cos(ang) * R, math.sin(ang) * R
        local cy, sy = math.cos(yaw), math.sin(yaw)
        return x * cy - z * sy, x * sy + z * cy
    end
    local function sigilLine(p, c0, ax, az, bx, bz, w, tr)
        local A, B = Vector3.new(ax, 0, az), Vector3.new(bx, 0, bz)
        local d = B - A
        local mid = c0 + (A + B) / 2
        p.Size = Vector3.new(w, 0.05, math.max(d.Magnitude, 0.01))
        p.Transparency = tr
        mv(p, CFrame.lookAt(mid, mid + d))
    end

    def("Sigil", function()
        local o = newObj()
        o.rings = {newRing(o, 18, true), newRing(o, 18, true), newRing(o, 18, true), newRing(o, 18, true)}
        o.lines, o.orbs = {}, {}
        for i = 1, 10 do o.lines[i] = mk(BLOCK, Vector3.new(0.16, 0.05, 1), nil, o, 1) end
        for i = 1, 6 do o.orbs[i] = mk(BALL, Vector3.new(0.5, 0.5, 0.5), nil, o, 1) end
        o.anchor = mk(BLOCK, Vector3.new(7, 0.2, 7), Enum.Material.SmoothPlastic, o, 1)
        o.sparks = sparkEmitter(o.anchor, 22, 1.5, 3, 7, 0.45)
        o.sparks.Acceleration = Vector3.new(0, 2, 0)
        o.light = newLight(o.anchor, 16)
        o.acc = 1
        hookVis(o, function(on)
            o.sparks.Enabled = on
            o.light.Enabled = on
            if not on then
                for _, r in ipairs(o.rings) do hideRing(r) end
            end
        end)
        return o
    end, function(o, C, t, color, cx, dt)
        local a, k = C.Anim, C.Size
        o.acc += dt
        if o.acc > 0.12 or not o.gyT then
            o.acc = 0
            local gp = groundAt(cx.rpos, cx, 3, 14)
            o.gyT = gp and gp.Y or (cx.rpos.Y - 2.9)
            o.gy = o.gy or o.gyT
        end
        o.gy += (o.gyT - o.gy) * math.min(1, dt * 14)
        local c0 = Vector3.new(cx.rpos.X, o.gy + 0.07, cx.rpos.Z)
        local pulse = 0.5 + 0.5 * math.sin(t * 3)
        local R = 4.2 * k
        local recolor = o.col ~= color
        o.col = color
        -- rings
        local base = CFrame.new(c0)
        if a == 3 then
            for i = 1, 3 do
                local ph = (t * 0.45 + i / 3) % 1
                ringSet(o.rings[i], CFrame.new(c0 + Vector3.new(0, ph * 7.5, 0)), R * 2.1 * (1 - 0.55 * ph),
                    1 - math.sin(ph * math.pi) ^ 0.6 * 0.9, color)
            end
            ringSet(o.rings[4], base, R * 2.15, 0.08 + 0.2 * pulse, color)
        else
            ringSet(o.rings[1], base, R * 2.15, 0.06 + 0.2 * pulse, color)
            ringSet(o.rings[2], base, R * 1.72, 0.2, color)
            ringSet(o.rings[3], base, R * 0.85, 0.12 + 0.2 * (1 - pulse), color)
            hideRing(o.rings[4])
        end
        -- star lines + vertex orbs
        local lt = 0.05 + 0.3 * pulse
        local used, orbs = 0, 0
        if a == 2 then
            local yaw = t * 0.42
            for j = 0, 4 do
                local ax, az = sigilXZ(R, math.pi / 2 + j * TAU / 5, yaw)
                local bx, bz = sigilXZ(R, math.pi / 2 + ((j + 2) % 5) * TAU / 5, yaw)
                used += 1
                sigilLine(o.lines[used], c0, ax, az, bx, bz, 0.18 * k, lt)
                orbs += 1
                o.orbs[orbs].Transparency = 0.1
                o.orbs[orbs].Size = Vector3.new(0.55 * k, 0.55 * k, 0.55 * k)
                mv(o.orbs[orbs], CFrame.new(c0 + Vector3.new(ax, 0.2, az)))
            end
            local yaw2 = -t * 0.9
            for j = 0, 4 do
                local ax, az = sigilXZ(R * 0.48, math.pi / 2 + j * TAU / 5, yaw2)
                local bx, bz = sigilXZ(R * 0.48, math.pi / 2 + (j + 1) * TAU / 5, yaw2)
                used += 1
                sigilLine(o.lines[used], c0, ax, az, bx, bz, 0.14 * k, lt)
            end
        else
            local yaw = t * (a == 3 and 0.25 or 0.6)
            local rad = (a == 3) and R * 0.9 or R
            for tri = 0, 1 do
                for j = 0, 2 do
                    local a0 = math.pi / 2 + tri * math.pi / 3 + j * TAU / 3
                    local ax, az = sigilXZ(rad, a0, yaw)
                    local bx, bz = sigilXZ(rad, a0 + TAU / 3, yaw)
                    used += 1
                    sigilLine(o.lines[used], c0, ax, az, bx, bz, 0.18 * k, lt)
                    orbs += 1
                    o.orbs[orbs].Transparency = 0.1
                    o.orbs[orbs].Size = Vector3.new(0.55 * k, 0.55 * k, 0.55 * k)
                    mv(o.orbs[orbs], CFrame.new(c0 + Vector3.new(ax, 0.2, az)))
                end
            end
            if a == 1 then
                local yaw2 = -t * 1.0
                for j = 0, 2 do
                    local ax, az = sigilXZ(R * 0.5, math.pi / 2 + j * TAU / 3, yaw2)
                    local bx, bz = sigilXZ(R * 0.5, math.pi / 2 + (j + 1) * TAU / 3, yaw2)
                    used += 1
                    sigilLine(o.lines[used], c0, ax, az, bx, bz, 0.14 * k, lt)
                end
            end
        end
        for i = used + 1, #o.lines do o.lines[i].Transparency = 1 end
        for i = orbs + 1, #o.orbs do o.orbs[i].Transparency = 1 end
        o.anchor.Size = Vector3.new(R * 1.4, 0.2, R * 1.4)
        mv(o.anchor, CFrame.new(c0))
        o.light.Brightness = 1.5 + pulse
        o.light.Range = 16 * k
        if recolor then
            for _, p in ipairs(o.lines) do p.Color = color:Lerp(WHITE, 0.25) end
            for _, p in ipairs(o.orbs) do p.Color = color:Lerp(WHITE, 0.55) end
            o.sparks.Color = hotSeq(color)
            o.light.Color = color
        end
    end)

    ----------------------------------------------------------------------
    -- Screen effects: speed lines (14), chromatic edges (15), glitch bars (16), neon grade (17)
    ----------------------------------------------------------------------
    local SL = {items = {}, s = 0, acc = 0, frame = nil}
    do
        local f = Instance.new("Frame")
        f.Name = "SpeedLines"
        f.Size = UDim2.fromScale(1, 1)
        f.BackgroundTransparency = 1
        f.Active = false
        f.Visible = false
        f.ZIndex = 0
        f.Parent = overlay
        SL.frame = f
        for i = 1, 44 do
            local pivot = Instance.new("Frame")
            pivot.Size = UDim2.fromOffset(0, 0)
            pivot.Position = UDim2.fromScale(0.5, 0.5)
            pivot.BackgroundTransparency = 1
            pivot.Rotation = i / 44 * 360
            pivot.ZIndex = 0
            pivot.Parent = f
            local line = Instance.new("Frame")
            line.BorderSizePixel = 0
            line.BackgroundColor3 = WHITE
            line.ZIndex = 0
            line.Parent = pivot
            local g = Instance.new("UIGradient")
            g.Transparency = NumberSequence.new({NumberSequenceKeypoint.new(0, 1), NumberSequenceKeypoint.new(1, 0.1)})
            g.Parent = line
            SL.items[i] = {pivot = pivot, line = line}
        end
    end
    local function speedLines(on, C, t, color, dt, vp)
        local target = 0
        if on then
            if C.Anim == 1 then
                target = math.clamp((ex.spd - 14) / 28, 0, 1)
            elseif C.Anim == 2 then
                target = 0.7
            else
                target = 0.35 + 0.5 * math.abs(math.sin(t * 3))
            end
        end
        SL.s += (target - SL.s) * math.min(1, dt * 6)
        local s = SL.s
        SL.frame.Visible = s > 0.02
        RX.kickS = on and (C.Anim ~= 3 and s * 7 or 0) or 0
        if s <= 0.02 then return end
        SL.acc += dt
        if SL.acc < 0.05 then return end
        SL.acc = 0
        local D = vp.Magnitude / 2
        local col = WHITE:Lerp(color, 0.35)
        for _, it in ipairs(SL.items) do
            if math.random() < 0.4 or not it.init then
                it.init = true
                local r0 = D * (0.2 + math.random() * 0.35)
                local len = D * (0.2 + math.random() * 0.4) * (0.35 + 0.65 * s) * (C and C.Size or 1)
                local th = 1 + math.random() * 2.5
                it.pivot.Rotation = math.random() * 360
                it.line.Position = UDim2.fromOffset(r0, -th / 2)
                it.line.Size = UDim2.fromOffset(len, th)
            end
            it.line.BackgroundColor3 = col
            it.line.BackgroundTransparency = 1 - 0.75 * s * (0.5 + 0.5 * math.random())
        end
    end

    local function chromaStep(on, C, t, dt)
        local amp = 0
        if on then
            if C.Anim == 1 then
                amp = 0.55
            elseif C.Anim == 2 then
                amp = 0.15 + 0.5 * math.abs(math.sin(t * 2))
            else
                amp = math.clamp(ex.spd / 45, 0, 1) * 0.8 + math.clamp(ex.turn / 6, 0, 0.6)
            end
        end
        amp = math.max(amp, R.chroma or 0, E.impactChroma or 0)
        chromaEdges.show(amp, C and (0.6 + C.Size * 0.4) or 1)
    end

    local gradeCC, gradeBloom, gradeK = nil, nil, 0
    local GRADES = {
        {tint = Color3.fromRGB(255, 232, 255), sat = 0.55, con = 0.28, bri = -0.03, bi = 1.2, bs = 36, bt = 0.75},
        {tint = Color3.fromRGB(205, 240, 255), sat = 0.35, con = 0.22, bri = -0.02, bi = 1.0, bs = 30, bt = 0.8},
        {tint = Color3.fromRGB(255, 165, 155), sat = -0.3, con = 0.35, bri = -0.05, bi = 1.1, bs = 34, bt = 0.8},
    }
    local function gradeStep(on, C, dt)
        gradeK += ((on and 1 or 0) - gradeK) * math.min(1, dt * 3)
        if gradeK < 0.01 and not on then
            if gradeCC then
                gradeCC:Destroy()
                gradeBloom:Destroy()
                gradeCC, gradeBloom = nil, nil
            end
            return
        end
        if not gradeCC then
            for _, n in ipairs({"RMEXGrade", "RMEXGradeBloom"}) do
                local old = Lighting:FindFirstChild(n)
                if old then old:Destroy() end
            end
            gradeCC = Instance.new("ColorCorrectionEffect")
            gradeCC.Name = "RMEXGrade"
            gradeCC.Parent = Lighting
            gradeBloom = Instance.new("BloomEffect")
            gradeBloom.Name = "RMEXGradeBloom"
            gradeBloom.Parent = Lighting
        end
        local g = GRADES[C and C.Anim or 1] or GRADES[1]
        local k = gradeK * math.clamp((C and C.Intensity or 45) / 45, 0.2, 1.6)
        gradeCC.TintColor = WHITE:Lerp(g.tint, math.min(k, 1))
        gradeCC.Saturation = math.clamp(g.sat * k, -1, 1)
        gradeCC.Contrast = math.clamp(g.con * k, -1, 1)
        gradeCC.Brightness = g.bri * k
        gradeBloom.Intensity = g.bi * math.min(k, 1.3)
        gradeBloom.Size = g.bs
        gradeBloom.Threshold = 1 - (1 - g.bt) * math.min(k, 1)
    end

    local gb = {nextAt = 0}
    local function glitchStep(on, C, t, dt)
        if not on then return end
        if t < gb.nextAt then return end
        if C.Anim == 1 then
            gb.nextAt = t + 2.5 + math.random() * 2.5
            bars.burst(0.18, 0.6)
        elseif C.Anim == 2 then
            gb.nextAt = t + 0.7 + math.random() * 0.9
            bars.burst(0.2, 0.7)
        elseif ex.spd > 10 or ex.turn > 3 then
            gb.nextAt = t + 0.45
            bars.burst(0.15, 0.5)
        end
    end

    ----------------------------------------------------------------------
    -- Screen impact (v14): expanding shock rings + white flash + RGB split + camera punch
    -- Jump = on takeoff, Landing = on hard landing, Beat = steady heartbeat
    ----------------------------------------------------------------------
    local IM = {rings = {}, nextR = 1, flash = nil, flashA = 0, chroma = 0, beat = 0}
    do
        local fl = Instance.new("Frame")
        fl.Name = "ImpactFlash"
        fl.Size = UDim2.fromScale(1, 1)
        fl.BackgroundColor3 = WHITE
        fl.BackgroundTransparency = 1
        fl.BorderSizePixel = 0
        fl.Active = false
        fl.Visible = false
        fl.ZIndex = 0
        fl.Parent = overlay
        IM.flash = fl
        for i = 1, 3 do
            local f = Instance.new("Frame")
            f.Name = "ImpactRing"
            f.AnchorPoint = Vector2.new(0.5, 0.5)
            f.Position = UDim2.fromScale(0.5, 0.5)
            f.Size = UDim2.fromOffset(10, 10)
            f.BackgroundTransparency = 1
            f.BorderSizePixel = 0
            f.Active = false
            f.Visible = false
            f.ZIndex = 0
            f.Parent = overlay
            local uc = Instance.new("UICorner")
            uc.CornerRadius = UDim.new(0.5, 0)
            uc.Parent = f
            local st = Instance.new("UIStroke")
            st.Thickness = 8
            st.Color = WHITE
            st.Transparency = 1
            st.Parent = f
            IM.rings[i] = {f = f, st = st, age = 9, life = 0.8}
        end
    end
    local function impactBurst(power, color)
        local r = IM.rings[IM.nextR]
        IM.nextR = IM.nextR % #IM.rings + 1
        r.age, r.life, r.col = 0, 0.7 + 0.2 * power, color
        r.st.Color = (color or WHITE):Lerp(WHITE, 0.5)
        r.f.Visible = true
        IM.flashA = math.max(IM.flashA, 0.22 * power)
        IM.chroma = math.max(IM.chroma, 0.8 * power)
        addKick(7 * power, 0.5 * power)
    end
    local function impactStep(on, C, t, color, dt, vp)
        if on and C then
            if C.Anim == 1 then
                if ex.jumped then impactBurst(0.7, color) end
            elseif C.Anim == 2 then
                if ex.landed then impactBurst(ex.landP or 1, color) end
            else
                IM.beat += dt * C.Speed
                if IM.beat >= 1.2 then
                    IM.beat = 0
                    impactBurst(0.5, color)
                end
            end
        end
        local diag = vp.Magnitude
        for _, r in ipairs(IM.rings) do
            if r.f.Visible then
                r.age += dt
                local u = r.age / r.life
                if u >= 1 then
                    r.f.Visible = false
                else
                    local d = 40 + diag * 0.85 * easeOut(u)
                    r.f.Size = UDim2.fromOffset(d, d)
                    r.st.Transparency = u ^ 1.2
                end
            end
        end
        IM.flashA *= math.exp(-dt * 9)
        IM.chroma *= math.exp(-dt * 5)
        local fl = IM.flash
        fl.Visible = IM.flashA > 0.02
        if fl.Visible then
            fl.BackgroundColor3 = color:Lerp(WHITE, 0.7)
            fl.BackgroundTransparency = 1 - IM.flashA
        end
        E.impactChroma = IM.chroma
    end

    ----------------------------------------------------------------------
    -- Driver (called once per frame from the main loop)
    ----------------------------------------------------------------------
    local prev = {esp = false, aim = false, vis = false}
    local lastLook
    RX.extUpdate = function(dt)
        local cam = getCam()
        if not cam then return end
        local vp = cam.ViewportSize
        -- camera turn speed (used by a few reactive effects)
        local look = cam.CFrame.LookVector
        ex.turn = lastLook and math.acos(math.clamp(look:Dot(lastLook), -1, 1)) / math.max(dt, 0.001) or 0
        lastLook = look
        local root, char = fx.root, fx.character
        local alive = root and root.Parent and char
        if alive then
            local v = root.AssemblyLinearVelocity
            ex.spd = Vector3.new(v.X, 0, v.Z).Magnitude
            ex.rpos, ex.root, ex.char = root.Position, root, char
            -- takeoff / hard landing flags shared by the v14 effects
            local pvy = ex.pvy or 0
            ex.landed = pvy < -30 and v.Y > -6
            ex.landP = math.clamp(-pvy / 55, 0.5, 1.6)
            ex.jumped = pvy < 12 and v.Y > 32
            ex.pvy = v.Y
        else
            ex.spd = 0
            ex.landed, ex.jumped, ex.pvy = false, false, 0
        end
        local master = visual.Master

        -- trigger detection (rising edges)
        local espAny = settings.Boxes or settings.Outline or settings.Names or settings.Distance or settings.Health
            or settings.Tracers or settings.Radar or settings.Arrows or settings.HeadDot or settings.LookLine
        local aimOn = RX.aim and RX.aim.On
        local visAny = false
        for _, item in ipairs(personalToggles) do
            if not item.meta and item.field ~= "Master" and visual[item.field] then
                visAny = true
                break
            end
        end
        if aimOn and not prev.aim then
            detect(ALERT, "det_aim")
        elseif espAny and not prev.esp then
            detect(GREEN, "det_esp")
        end
        if visAny and master and not prev.vis and visual.Ritual and os.clock() - R.last > 6 then
            RX.ritualPlay()
        end
        prev.esp, prev.aim, prev.vis = espAny and true or false, aimOn and true or false, (visAny and master) and true or false

        detectStep(dt)
        ritualStep(dt, cam)
        bars.update(dt)

        -- screen effects
        local on = function(n) return master and visual[n] == true end
        local C, t, color
        if on("SpeedLines") then C, t, color = efx("SpeedLines", dt) end
        speedLines(on("SpeedLines"), C, t or 0, color or WHITE, dt, vp)
        C, t, color = nil, nil, nil
        if on("Chroma") then C, t = efx("Chroma", dt) end
        chromaStep(on("Chroma"), C, t or 0, dt)
        C, t = nil, nil
        if on("GlitchBars") then C, t = efx("GlitchBars", dt) end
        glitchStep(on("GlitchBars"), C, t or 0, dt)
        C = nil
        if on("Grade") then C = efx("Grade", dt) end
        gradeStep(on("Grade"), C, dt)
        C, t, color = nil, nil, nil
        if on("Impact") then C, t, color = efx("Impact", dt) end
        local okI, errI = pcall(impactStep, on("Impact"), C, t or 0, color or WHITE, dt, vp)
        if not okI and not IM.warned then
            IM.warned = true
            warn("[RMEX v14] Impact: " .. tostring(errI))
        end
        -- camera punch / shake requested by the v14 effects
        E.kick = (E.kick or 0) * math.exp(-dt * 7)
        E.shake = (E.shake or 0) * math.exp(-dt * 6)
        if E.shake > 0.02 then
            local s = E.shake * 0.01
            cam.CFrame = cam.CFrame * CFrame.Angles((math.random() - 0.5) * s, (math.random() - 0.5) * s, (math.random() - 0.5) * s * 1.5)
        end
        RX.fovKick = (R.kick or 0) + (RX.kickS or 0) + E.kick

        -- world effects
        if not alive then
            for _, o in pairs(E.obj) do
                if o.active then
                    o.active = false
                    o.vis(false)
                end
            end
            return
        end
        ensureFolder()
        for _, name in ipairs(ORDER) do
            local d = FXS[name]
            local o = E.obj[name]
            if master and visual[name] then
                if not o and not d.broken then
                    local okB, res = pcall(d.build)
                    if okB then
                        o = res
                        E.obj[name] = o
                    else
                        d.broken = true
                        warn("[RMEX v14] " .. name .. " build: " .. tostring(res))
                    end
                end
                if not o then continue end
                local C2, t2, c2 = efx(name, dt)
                if not o.active then
                    o.active = true
                    o.vis(true)
                end
                local okS, errS = pcall(d.step, o, C2, t2, c2, ex, dt)
                if not okS and not d.warned then
                    d.warned = true
                    warn("[RMEX v14] " .. name .. ": " .. tostring(errS))
                end
            elseif o and o.active then
                o.active = false
                o.vis(false)
            end
        end
        flush()
    end
end
__block3()

-- ============================================================================
-- FLY (UNIVERSAL tab): toggle opens a movable window with FLY / speed - + / OFF
-- ============================================================================
local function __block4()
    local T = {
        en = {ufly = "Fly", ufly_d = "Opens a movable window: fly on/off, speed + / -"},
        ru = {ufly = "Полёт (Fly)", ufly_d = "Открывает окно: полёт вкл/выкл, скорость + / -"},
    }
    for l, t in pairs(T) do
        for k, v in pairs(t) do STRINGS[l][k] = v end
    end

    local Fly = {On = false, Speed = 50, Win = false}
    RX.fly = Fly
    local lv, att, al
    local controls

    local win = Instance.new("Frame")
    win.Name = "RMEXFlyWin"
    win.Size = UDim2.fromOffset(210, 152)
    win.Position = UDim2.fromScale(0.62, 0.3)
    win.BackgroundColor3 = Color3.fromRGB(18, 18, 24)
    win.BackgroundTransparency = 0.12
    win.BorderSizePixel = 0
    win.Active = true
    win.Visible = false
    win.ZIndex = 40
    win.Parent = gui
    corner(win, 12)
    local wStroke = Instance.new("UIStroke")
    wStroke.Thickness = 1.5
    wStroke.Parent = win

    local title = Instance.new("TextButton")
    title.Size = UDim2.new(1, 0, 0, 30)
    title.BackgroundTransparency = 1
    title.AutoButtonColor = false
    title.Text = "FLY   (drag)"
    title.Font = Enum.Font.GothamBold
    title.TextSize = 12
    title.ZIndex = 41
    title.Parent = win
    makeDraggable(title, win)

    local function btn(text, x, y, w, h, cb)
        local b = Instance.new("TextButton")
        b.Position = UDim2.fromOffset(x, y)
        b.Size = UDim2.fromOffset(w, h)
        b.BackgroundColor3 = Color3.fromRGB(34, 34, 44)
        b.BorderSizePixel = 0
        b.AutoButtonColor = false
        b.Text = text
        b.TextColor3 = Color3.new(1, 1, 1)
        b.Font = Enum.Font.GothamBold
        b.TextSize = 14
        b.ZIndex = 41
        b.Parent = win
        corner(b, 8)
        addPress(b, 0.94)
        b.Activated:Connect(cb)
        return b
    end

    local flyBtn, spdLbl
    local function refresh()
        flyBtn.Text = Fly.On and "FLY: ON" or "FLY: OFF"
        flyBtn.BackgroundColor3 = Fly.On and P.accent or Color3.fromRGB(34, 34, 44)
        flyBtn.TextColor3 = Fly.On and P.onAccent or Color3.new(1, 1, 1)
        spdLbl.Text = "SPEED " .. Fly.Speed
    end

    local function stopFly()
        Fly.On = false
        if lv then lv:Destroy() lv = nil end
        if al then al:Destroy() al = nil end
        if att then att:Destroy() att = nil end
        local ch = localPlayer.Character
        local hum = ch and ch:FindFirstChildOfClass("Humanoid")
        if hum then hum.PlatformStand = false end
    end

    local function startFly()
        local ch = localPlayer.Character
        local hum = ch and ch:FindFirstChildOfClass("Humanoid")
        local root = ch and ch:FindFirstChild("HumanoidRootPart")
        if not (hum and root) then return end
        stopFly()
        att = Instance.new("Attachment")
        att.Name = "RMEX_FlyAtt"
        att.Parent = root
        lv = Instance.new("LinearVelocity")
        lv.Name = "RMEX_FlyLV"
        lv.Attachment0 = att
        lv.MaxForce = math.huge
        lv.RelativeTo = Enum.ActuatorRelativeTo.World
        lv.VectorVelocity = Vector3.zero
        lv.Parent = root
        al = Instance.new("AlignOrientation")
        al.Name = "RMEX_FlyAlign"
        al.Mode = Enum.OrientationAlignmentMode.OneAttachment
        al.Attachment0 = att
        al.RigidityEnabled = true
        al.Parent = root
        hum.PlatformStand = true
        Fly.On = true
    end

    flyBtn = btn("FLY: OFF", 10, 38, 190, 34, function()
        if Fly.On then stopFly() else startFly() end
        refresh()
    end)
    btn("-", 10, 80, 44, 34, function() Fly.Speed = math.max(10, Fly.Speed - 10) refresh() end)
    spdLbl = btn("SPEED 50", 58, 80, 94, 34, function() end)
    spdLbl.BackgroundTransparency = 1
    btn("+", 156, 80, 44, 34, function() Fly.Speed = math.min(300, Fly.Speed + 10) refresh() end)
    btn("OFF", 10, 120, 190, 26, function()
        stopFly()
        Fly.Win = false
        win.Visible = false
        refresh()
    end)
    bindTheme(function(p)
        wStroke.Color = p.accent
        title.TextColor3 = p.accent
        refresh()
    end)

    local function getMove(hum)
        if controls == nil then
            controls = false
            pcall(function()
                local pm = localPlayer:WaitForChild("PlayerScripts"):WaitForChild("PlayerModule", 3)
                controls = require(pm):GetControls()
            end)
        end
        if controls then
            local ok, v = pcall(function() return controls:GetMoveVector() end)
            if ok and v then return v end
        end
        return workspace.CurrentCamera.CFrame:VectorToObjectSpace(hum.MoveDirection)
    end

    RunService.Heartbeat:Connect(function()
        if not Fly.On then return end
        local ch = localPlayer.Character
        local hum = ch and ch:FindFirstChildOfClass("Humanoid")
        local cam = workspace.CurrentCamera
        if not (lv and lv.Parent and hum and cam) or hum.Health <= 0 then
            stopFly() refresh() return
        end
        local mv = getMove(hum)
        local v = cam.CFrame:VectorToWorldSpace(Vector3.new(mv.X, 0, mv.Z)) * Fly.Speed
        if UserInputService:IsKeyDown(Enum.KeyCode.Space) then v += Vector3.yAxis * Fly.Speed * 0.7 end
        if UserInputService:IsKeyDown(Enum.KeyCode.LeftControl) then v -= Vector3.yAxis * Fly.Speed * 0.7 end
        lv.VectorVelocity = v
        local look = cam.CFrame.LookVector
        local flat = Vector3.new(look.X, 0, look.Z)
        if flat.Magnitude > 0.01 then al.CFrame = CFrame.lookAt(Vector3.zero, flat) end
    end)

    localPlayer.CharacterAdded:Connect(function()
        lv, att, al = nil, nil, nil
        Fly.On = false
        refresh()
    end)

    makeToggleRow(universalPage, {key = "ufly", desc = "ufly_d",
        get = function() return Fly.Win end,
        set = function(v)
            Fly.Win = v
            win.Visible = v
            if not v then stopFly() end
            refresh()
        end})
end
__block4()

-- ============================================================================
-- MAIN LOOP
-- ============================================================================

RunService.RenderStepped:Connect(function(dt)
    local cam = getCam()
    if not cam then return end
    local vp = cam.ViewportSize

    if visual.Rainbow then
        rainbowHue = (rainbowHue + dt * visual.RainbowSpeed / 100) % 1
        previewFrame.BackgroundColor3 = getEffectColor()
    end

    -- Tracers (stretched with the overlay settings)
    local sx, sy = esp.StretchX / 100, esp.StretchY / 100
    local cx0, cy0 = vp.X * 0.5, vp.Y * 0.5
    local startPoint = Vector2.new(cx0, esp.Origin == "top" and 0 or (esp.Origin == "center" and cy0 or vp.Y))
    for player, line in pairs(tracers) do
        local char = player.Character
        local root = char and char:FindFirstChild("HumanoidRootPart")
        if not settings.Tracers or not root then
            line.Visible = false
        else
            local pt = cam:WorldToViewportPoint(root.Position)
            local ex, ey = pt.X, pt.Y
            if pt.Z <= 0 then
                ex = vp.X - ex
                ey = vp.Y - ey
            end
            ex = (ex - cx0) * sx + cx0
            ey = (ey - cy0) * sy + cy0
            ex = math.clamp(ex, 2, vp.X - 2)
            ey = math.clamp(ey, 2, vp.Y - 2)
            local delta = Vector2.new(ex, ey) - startPoint
            line.Position = UDim2.fromOffset((startPoint.X + ex) / 2, (startPoint.Y + ey) / 2)
            line.Size = UDim2.fromOffset(math.max(delta.Magnitude, 1), 2)
            line.Rotation = math.deg(math.atan2(delta.Y, delta.X))
            line.BackgroundColor3 = P.accent
            line.Visible = true
            local dot = line:FindFirstChild("Dot")
            if dot then
                dot.BackgroundColor3 = P.text
                dot.UIStroke.Color = P.accent
            end
        end
    end

    -- ESP
    local myChar = localPlayer.Character
    local myRoot = myChar and myChar:FindFirstChild("HumanoidRootPart")
    for player, data in pairs(tracked) do
        if not data.character.Parent then
            removeESP(player)
        else
            updateESPBox(data, dt, vp)
            updateESPInfo(player, data, myRoot, dt)
        end
    end

    -- Universal: speed / jump / gravity
    local uni = RX.uni
    local hum = myChar and myChar:FindFirstChildOfClass("Humanoid")
    if hum then
        if uni.Speed then
            if not uni.oS then uni.oS = hum.WalkSpeed end
            hum.WalkSpeed = uni.SpeedV
        elseif uni.oS then
            hum.WalkSpeed = uni.oS
            uni.oS = nil
        end
        if uni.Jump then
            if not uni.oJ then uni.oJ = hum.UseJumpPower and hum.JumpPower or hum.JumpHeight end
            if hum.UseJumpPower then
                hum.JumpPower = uni.JumpV
            else
                hum.JumpHeight = uni.JumpV * uni.JumpV / (2 * workspace.Gravity)
            end
        elseif uni.oJ then
            if hum.UseJumpPower then hum.JumpPower = uni.oJ else hum.JumpHeight = uni.oJ end
            uni.oJ = nil
        end
    end
    if uni.Grav then
        if not uni.oG then uni.oG = workspace.Gravity end
        workspace.Gravity = uni.GravV
    elseif uni.oG then
        workspace.Gravity = uni.oG
        uni.oG = nil
    end

    -- Always visible (fullbright)
    local fb = RX.fb
    if screenFX.Bright then
        if not fb then
            fb = {B = Lighting.Brightness, A = Lighting.Ambient, O = Lighting.OutdoorAmbient,
                S = Lighting.GlobalShadows, F = Lighting.FogEnd, E = Lighting.ExposureCompensation}
            local atm = Lighting:FindFirstChildOfClass("Atmosphere")
            if atm then fb.atm = atm; fb.D = atm.Density end
            RX.fb = fb
        end
        local k = RX.bright.Level / 100
        local g = 0.3 + 0.7 * k
        Lighting.Ambient = Color3.new(g, g, g)
        Lighting.OutdoorAmbient = Color3.new(g, g, g)
        Lighting.Brightness = 1 + 2 * k
        Lighting.GlobalShadows = false
        Lighting.FogEnd = 1e6
        Lighting.ExposureCompensation = math.max(fb.E, 0.7 * k)
        if fb.atm and fb.atm.Parent then fb.atm.Density = fb.D * (1 - k) end
    elseif fb then
        Lighting.Brightness = fb.B
        Lighting.Ambient = fb.A
        Lighting.OutdoorAmbient = fb.O
        Lighting.GlobalShadows = fb.S
        Lighting.FogEnd = fb.F
        Lighting.ExposureCompensation = fb.E
        if fb.atm and fb.atm.Parent then fb.atm.Density = fb.D end
        RX.fb = nil
    end

    RX.perf(dt)
    RX.espExtras(cam, vp)

    -- World tint
    local tc = RX.tintCC
    if screenFX.Tint then
        if not tc or not tc.Parent then
            local old = Lighting:FindFirstChild("RMEXTint")
            if old then old:Destroy() end
            tc = Instance.new("ColorCorrectionEffect")
            tc.Name = "RMEXTint"
            tc.Parent = Lighting
            RX.tintCC = tc
        end
        local k = RX.tint.Strength / 100
        tc.TintColor = Color3.new(1, 1, 1):Lerp(RX.tint.Color, k)
        tc.Saturation = RX.tint.Mono and -1 or 0.25 * k
        tc.Contrast = 0.12 * k + (RX.tint.Mono and 0.2 or 0)
    elseif tc then
        tc:Destroy()
        RX.tintCC = nil
    end

    -- Motion blur (camera turn speed)
    local cam = workspace.CurrentCamera
    local bl = RX.blur
    if screenFX.Blur and cam then
        if not bl then
            local old = Lighting:FindFirstChild("RMEXMotionBlur")
            if old then old:Destroy() end
            bl = Instance.new("BlurEffect")
            bl.Name = "RMEXMotionBlur"
            bl.Size = 0
            bl.Parent = Lighting
            RX.blur = bl
        end
        local look = cam.CFrame.LookVector
        local ang = RX.lastLook and math.acos(math.clamp(look:Dot(RX.lastLook), -1, 1)) or 0
        RX.lastLook = look
        local target = math.min(math.max(0, ang / math.max(dt, 0.001) - 0.6) * 3.5 * (RX.blurK / 50), 26)
        bl.Size = bl.Size + (target - bl.Size) * math.min(1, dt * 10)
    elseif bl then
        bl:Destroy()
        RX.blur = nil
        RX.lastLook = nil
    end

    updateEffects(dt)
    if RX.extUpdate then
        local ok, err = pcall(RX.extUpdate, dt)
        if not ok and RX.extErr ~= err then
            RX.extErr = err
            warn("[RMEX v12] " .. tostring(err))
        end
    end
end)

-- ============================================================================
-- HOOKS
-- ============================================================================

for _, player in ipairs(Players:GetPlayers()) do
    setupPlayer(player)
end

Players.PlayerAdded:Connect(setupPlayer)

Players.PlayerRemoving:Connect(function(player)
    removeESP(player)
    if tracers[player] then
        tracers[player]:Destroy()
        tracers[player] = nil
    end
    if playerConns[player] then
        for _, c in ipairs(playerConns[player]) do c:Disconnect() end
        playerConns[player] = nil
    end
end)

localPlayer.CharacterAdded:Connect(function(character)
    task.spawn(buildEffects, character)
end)
localPlayer.CharacterRemoving:Connect(function()
    clearEffects()
end)
if localPlayer.Character then
    task.spawn(buildEffects, localPlayer.Character)
end

-- ============================================================================
-- INTRO SPLASH: fullscreen "RMEX VISUAL" animation on load, then fades away
-- ============================================================================
do
    local intro = Instance.new("ScreenGui")
    intro.Name = "RMEXIntro"
    intro.ResetOnSpawn = false
    intro.IgnoreGuiInset = true
    intro.DisplayOrder = 999
    intro.Parent = playerGui

    local dim = Instance.new("Frame")
    dim.Name = "Dim"
    dim.Size = UDim2.fromScale(1, 1)
    dim.BackgroundColor3 = Color3.fromRGB(7, 7, 12)
    dim.BackgroundTransparency = 1
    dim.BorderSizePixel = 0
    dim.Parent = intro

    -- vignette-style dark gradient on the intro screen
    local dimG = Instance.new("UIGradient")
    dimG.Rotation = 90
    dimG.Color = ColorSequence.new({
        ColorSequenceKeypoint.new(0, Color3.fromRGB(10, 10, 18)),
        ColorSequenceKeypoint.new(0.5, Color3.fromRGB(5, 5, 9)),
        ColorSequenceKeypoint.new(1, Color3.fromRGB(12, 10, 20)),
    })
    dimG.Parent = dim

    local TITLE = "RMEX VISUAL"
    local holder = Instance.new("Frame")
    holder.AnchorPoint = Vector2.new(0.5, 0.5)
    holder.Position = UDim2.fromScale(0.5, 0.44)
    holder.Size = UDim2.fromOffset(0, 90)
    holder.BackgroundTransparency = 1
    holder.Parent = dim
    local layout = Instance.new("UIListLayout")
    layout.FillDirection = Enum.FillDirection.Horizontal
    layout.HorizontalAlignment = Enum.HorizontalAlignment.Center
    layout.VerticalAlignment = Enum.VerticalAlignment.Center
    layout.Padding = UDim.new(0, 4)
    layout.SortOrder = Enum.SortOrder.LayoutOrder
    layout.Parent = holder

    local letters = {}
    local accentNow = accent
    for i = 1, #TITLE do
        local ch = TITLE:sub(i, i)
        local l = Instance.new("TextLabel")
        l.LayoutOrder = i
        l.BackgroundTransparency = 1
        l.Size = UDim2.fromOffset(ch == " " and 26 or 0, 90)
        l.AutomaticSize = ch == " " and Enum.AutomaticSize.None or Enum.AutomaticSize.X
        l.Font = Enum.Font.GothamBlack
        l.Text = ch
        l.TextSize = 12
        l.TextTransparency = 1
        l.TextColor3 = Color3.new(1, 1, 1)
        l.TextStrokeTransparency = 1
        l.Parent = holder
        local stroke = Instance.new("UIStroke")
        stroke.Thickness = 2
        stroke.Color = accentNow
        stroke.Transparency = 1
        stroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Contour
        stroke.Parent = l
        letters[i] = {label = l, stroke = stroke}
    end

    -- underline that draws itself in
    local line = Instance.new("Frame")
    line.AnchorPoint = Vector2.new(0.5, 0)
    line.Position = UDim2.new(0.5, 0, 0.44, 58)
    line.Size = UDim2.fromOffset(0, 3)
    line.BorderSizePixel = 0
    line.BackgroundColor3 = accentNow
    line.BackgroundTransparency = 1
    line.Parent = dim
    local lineC = Instance.new("UICorner")
    lineC.CornerRadius = UDim.new(1, 0)
    lineC.Parent = line

    -- subtitle
    local sub = Instance.new("TextLabel")
    sub.AnchorPoint = Vector2.new(0.5, 0)
    sub.Position = UDim2.new(0.5, 0, 0.44, 74)
    sub.Size = UDim2.fromOffset(400, 20)
    sub.BackgroundTransparency = 1
    sub.Font = Enum.Font.Code
    sub.TextSize = 14
    sub.Text = "v14 · epic VFX loaded"
    sub.TextColor3 = accentNow
    sub.TextTransparency = 1
    sub.Parent = dim

    -- shine band that sweeps across the title
    local shine = Instance.new("Frame")
    shine.AnchorPoint = Vector2.new(0.5, 0.5)
    shine.Position = UDim2.fromScale(-0.2, 0.44)
    shine.Size = UDim2.new(0.18, 0, 0, 110)
    shine.BackgroundColor3 = Color3.new(1, 1, 1)
    shine.BackgroundTransparency = 1
    shine.BorderSizePixel = 0
    shine.Rotation = 18
    shine.Parent = dim
    local shineG = Instance.new("UIGradient")
    shineG.Transparency = NumberSequence.new({
        NumberSequenceKeypoint.new(0, 1),
        NumberSequenceKeypoint.new(0.5, 0.55),
        NumberSequenceKeypoint.new(1, 1),
    })
    shineG.Parent = shine

    task.spawn(function()
        local ti = TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
        -- screen fades in
        TweenService:Create(dim, TweenInfo.new(0.35), {BackgroundTransparency = 0.12}):Play()
        task.wait(0.3)
        RX.beep(true)
        -- letters pop in one by one
        local pop = TweenInfo.new(0.45, Enum.EasingStyle.Back, Enum.EasingDirection.Out)
        for i, it in ipairs(letters) do
            if TITLE:sub(i, i) ~= " " then
                TweenService:Create(it.label, pop, {TextTransparency = 0, TextSize = 66}):Play()
                TweenService:Create(it.stroke, pop, {Transparency = 0.25}):Play()
                task.wait(0.07)
            end
        end
        -- underline + subtitle
        TweenService:Create(line, ti, {Size = UDim2.fromOffset(340, 3), BackgroundTransparency = 0.15}):Play()
        TweenService:Create(sub, ti, {TextTransparency = 0.2}):Play()
        task.wait(0.25)
        -- shine sweep
        TweenService:Create(shine, TweenInfo.new(0.7, Enum.EasingStyle.Quad, Enum.EasingDirection.InOut),
            {Position = UDim2.fromScale(1.2, 0.44), BackgroundTransparency = 0.55}):Play()
        task.wait(0.85)
        -- fade everything out
        local out = TweenInfo.new(0.65, Enum.EasingStyle.Quad, Enum.EasingDirection.In)
        TweenService:Create(dim, out, {BackgroundTransparency = 1}):Play()
        TweenService:Create(line, out, {BackgroundTransparency = 1}):Play()
        TweenService:Create(sub, out, {TextTransparency = 1}):Play()
        TweenService:Create(shine, out, {BackgroundTransparency = 1}):Play()
        for _, it in ipairs(letters) do
            TweenService:Create(it.label, out, {TextTransparency = 1, TextSize = 84}):Play()
            TweenService:Create(it.stroke, out, {Transparency = 1}):Play()
        end
        task.wait(0.75)
        intro:Destroy()
    end)
end

-- ============================================================================
-- START
-- ============================================================================

refreshTexts()
selectTab(1, true)
applySettings()
applyScreenFX()
