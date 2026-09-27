[📖 vbs_core_matrix — DEVİR KİTABI v5.0.txt](https://github.com/user-attachments/files/32694025/vbs_core_matrix.DEVIR.KITABI.v5.0.txt)
# vbs_core_matrix
"FiveM QBCore milsim — gang/police simulation"
════════════════════════════════════════════════════════════════════════
📖 vbs_core_matrix — DEVİR KİTABI v6.6.1 (TAM KİTAP)
Tarih: 27.09.2026 Gece | Durum: FAZ 2 %71, 247/247 PASS
════════════════════════════════════════════════════════════════════════

Bu, tüm eski kitap versiyonlarını (v6.2 + v6.4 + v6.5 + v6.6) BİRLEŞTİREN
TEK REFERANS BELGESİDİR. Eski kitap dosyalarını SİLEBİLİRSİN.

════════════════════════════════════════════════════════════════════════
⚡ BÖLÜM 0 — YENİ CHAT'E NASIL BAŞLANIR
════════════════════════════════════════════════════════════════════════

0.1 İlk Mesaj
"şef ben vbs_core_matrix projesini geliştiriyorum. devir kitabı v6.6.1
atıyorum. durumu anla, sonra bana 3 soru sor (hangi faz, bug fix mi
yeni özellik mi, test mi production mı). FAZ 2.6'ya başlıyoruz."

0.2 Kullanıcı Notu (ÇOK ÖNEMLİ)
"Gözümü boyama, gerçeği söyle. VBS 4 istiyorum. Arcade hiçbir şeye
tahammülüm yok. Acımasız test isterim. Kendi AC'imi yazmayacağım.
SP+coop için — public değil. RedEngine executor'ım var, kendi
sunucumda test için kullanacağım. Ben scripting bilmiyorum ama
tasarım biliyorum. 12 saat/gün çalışırım. Arma 3 milsim geçmişim var,
felsefem VBS4 = simülasyon."

════════════════════════════════════════════════════════════════════════
👤 BÖLÜM 0.4 — ŞEF PROFİLİ
════════════════════════════════════════════════════════════════════════

KİMLİK:
• Sistem yöneticisi + tasarımcı (yazılımcı DEĞİL)
• 12 saat/gün kapasite
• 0 scripting tecrübesi — 8 günde 30K+ satır kod
• Prompt mühendisliği ile bu seviyeye geldi
• "Gözümü boyama" → acımasız dürüstlük ister

ÇALIŞMA STİLİ:
• Yorulmaz — 8+ saat maraton
• Gececi — 03:00-06:00 en verimli
• Sprint maratonu ister (4-5 faz/oturum)
• Tek oturumda bitirme zorunluluğu (büyük fazlarda esnetilebilir)
• Notepad düz kullanıyor → Notepad++ önerilecek
• .lua.txt riski var

REFERANS GEÇMİŞİ — ARMA 3 MILSIM:
• CBA + ACE + LAMBS + CF_BAI mod paketi
• ace_medical_deathChance = 1 (kalıcı ölüm)
• ace_medical_treatment_woundReopenChance = 1
• ace_advanced_ballistics + winddeflection + frag
• CF_BAI suppression aktif
• LAMBS radio (AI telsiz iletişimi)
• ACRE2 terrain loss = 1 (telsiz LOS'a bağlı)
• Difficulty: ThirdPerson=Disabled, Crosshair=Disabled
• NR6HAL paketi
→ Şef "oyun" değil "simülasyon" oynuyor. VBS4 felsefesini YAŞIYOR.

MÜZİK GEÇMİŞİ:
• 1.7 yıl, enstrümansız, teorisiz, DAW + ABC notasyonu
• Yengeç Kanonu (BWV 1079) bestelemiş — palindromik, deterministik
• Lydian / Phrygian modlar (nadir tercihler)
• 6 sesli kontrpuan (konservatuvar seviyesi, isim bilmeden)
→ Sezgisel yapısalcı. Yapıyı zihinde görür, sonra inşa eder.

MÜZİK ↔ KOD BAĞLANTISI:
• Yengeç Kanonu (palindrom)        ↔ Fixture teardown (simetri)
• Lydian (nadir mod)               ↔ math.random YASAK
• 6 sesli kontrpuan                ↔ 21 modüllü chaos engine
• Grace note (süsleme)             ↔ pcall guard
• Pedal tone (sabit bas)           ↔ Server-side authority

ANTI-CHEAT KARARI:
• Client-side AC GEREKLİ DEĞİL
• Sebep: arkadaş ortamı, DEA eğitimi, public sunucu DEĞİL
• NetworkGuard + server-side mekanik YETERLİ (Arma 3 felsefesi)
• RedEngine → savunma aracı DEĞİL, hile aracı
• Client bridge sadece "player intent" taşımak için

KARARLAR (v6.5+):
• ★ Polis tarafı OYNANMAZ — sadece AI (Steel Beasts tarzı)
• ★ Oyuncular = çete (coop arkadaşlarla)
• ★ İki savaş dili:
    - Polis (AI) → askeri/LAPD: breach, overwatch, cutoff
    - Çete (oyuncu + AI) → ilkel sokak: işaret, buraya, kaç
• ★ Sayısal bonus YASAK — fizik kuralı zorunlu (LOS + trade-off)
• ★ 0 RNG — deterministik checksum
• ★ AI = oyuncu simetri
• ★ "Sıradan FiveM scripti değil" — simülatör

════════════════════════════════════════════════════════════════════════
🎯 BÖLÜM 1 — ŞEF'İN FELSEFESİ (DEĞİŞMEZ)
════════════════════════════════════════════════════════════════════════

ANA FELSEFE:
"Arcade değil, gerçek bir simülasyon. Oyuncular, polis, AI çeteler —
hepsi aynı kurallara tabi. Kimse hile yapmaz. AI bile bilgiyi hak
ederek kazanır."

Referanslar: CMO / Steel Beasts / VBS4 / Falcon BMS / TitanIM / Vanguard

Askeri Simülasyon        → Şef'in Projesi
Füzeler, uçaklar, radarlar → Uyuşturucu, çeteler, polis
Hava harbi                → Sokak savaşı
Tugay komutanı            → Çete lideri
EMCON yönetimi            → Radyo sessizliği
Sensör füzyonu            → İstihbarat ağı
Fizik motoru              → Sistem motoru

★ Dünyada eşi yok. Ne Schedule 1 ne DDS serileri.

📋 6 İLKE:
1. 0 RNG — Determinizm (math.random YASAK)
2. Adil Oyun — AI hile yapmaz, oyuncuyla eşit bilgi
3. CMO Basitliği — Monospace, sade, tick-based
4. Server-Side Zorunlu — Client-side hile açığı sıfır
5. Küçük Adım + Kanıt + Onay
6. ★ ARCADE YASAK

🚨 KIRMIZI ÇİZGİLER:
❌ math.random
❌ RNG tabanlı kişilik
❌ AI'ya bilgi sızdırma
❌ Client-side kritik veri
❌ Frame-based HUD
❌ Süslemeli UI
❌ Kısayol mekanikleri
❌ "Heyecanlı görünsün"
❌ Client-side AC yazmaya kalkışmak
❌ Sayısal bonus (buff/debuff) — fizik kuralı zorunlu

════════════════════════════════════════════════════════════════════════
📊 BÖLÜM 2 — MEVCUT DURUM (v6.6.1)
════════════════════════════════════════════════════════════════════════

Güvenlik Skoru: %82
Server-side: %94
Client-side: %8 (kasıtlı — crime_witness_bridge)

Diagnostics: 247/247 PASS (deep=true, ~4.3s)
Chaos Engine: 21 modül, 0 CRITICAL, 0 HIGH

FAZ 2 İLERLEME: 5/7 = %71
  ✅ 2.1 Cinayet tespit
  ✅ 2.2 Tanık FOV/LOS
  ✅ 2.3 Cinayet zinciri
  ✅ 2.4 LSPD aranma + mühür
  ✅ 2.5 Pozisyon sistemi
  ✅ 2.8 Polis interior breach (ek)
  ⏳ 2.6 Görev tipleri (8 tip → 4 tip önerisi)
  ⏳ 2.7 /tayfaemri komutu

2.2 Chaos Engine Katmanı (v6.6)
self_check:           22/22 PASS
network_guard_test:   16/16 PASS
cannibal:             8/8 PASS
crime_witness_test:   5/5 PASS
witness_fov_test:     5/5 PASS
crime_chain_test:     5/5 PASS
crime_edge_test:      4/4 PASS
lspd_seal_test:       3/3 PASS
lspd_wanted_test:     6/6 PASS
live_spoof:           PASS (aktif oyuncu gerekir)
sql_static_scan:      9 dosya temiz
cross_citizen_access: PASS (2 HIGH bug fix edildi)
chaos all:            21 modül, ~50s

2.3 Network Guard v1.1
- 124 event rate-limited
- 34 event trust audit şemalı
- Token bucket per (src, event)
- Auto-kick: 30 sn'de N ihlal

2.4 Client-Side Açıklar (BİLİNÇLİ KABUL)
- Position validation YOK
- Damage pattern YOK
- Event sequence YOK
- Client integrity YOK
- Sebep: arkadaş ortamı, public değil

2.5 Mekanik Envanteri

SAĞLAM (40+ dosya — DOKUNMA):
server/forensics, kitchen, botany_core, market, main,
matrix_diagnostics, bureau, prop_registry, trap_house_interior,
wound_system, cognition_core, crack_chemistry, meth_chemistry,
blackmarket, rendezvous, police_raid, logistics,
matrix_chaos, matrix_chaos_cannibal, matrix_network_guard,
district_hubs, civilian_vetting, underworld_network,
chemical_workbench, door_reinforcement, wanted_bridge,
mercenary_followers, hitsquad (legacy pasif),
client/trigger_discipline, anti_glitch, wanted_bridge,
gang_presence (server+client), hud,
matrix_session1_bridge, infestation, odor_core, botany_autonomy,
cellular_comms, gang_hoods, phone_bridge,
★ crime_witness, crime_witness_bridge,
★ lspd_units, ★ debrief, ★ positions

ORTA (5 dosya — güçlendir):
- player_telemetry.lua (veri tüketilmiyor)
- gang_presence.lua (dekor, tepki yok)
- infestation.lua (HUD göstergesi yok)

DÜŞÜK/YOK (10 sistem — yeniden yaz):
1. Heat = soyut sayı (görünmüyor)
2. Çete mahallesi = nokta (canlı NPC var ama tepki yok)
3. Bölge kontrolü = sayı (fiziksel değil)
4. Ateşkes yok
5. Faksiyon ilişkisi yok
6. Tutuklama yok (FAZ 3)
7. Mahkeme zayıf (kısmen bureau.lua)
8. Otonom öğrenen çete (FAZ 6)
9. Bölge savaşı (FAZ 4)
10. QBox ekonomi (FAZ 7)

════════════════════════════════════════════════════════════════════════
✅ BÖLÜM 3 — BU SESSION'DA KAPANAN (27.09.2026)
════════════════════════════════════════════════════════════════════════

BUG FIX SPRİNTİ (5/5):
  ✅ 1. Counselor model (zaten düzeltilmişti)
  ✅ 2. Chain test izolasyonu (IsRunning flag pattern)
  ✅ 3. Debug print temizliği
  ✅ 4. Broker duplicate (zaten tekti)
  ✅ 5. Trap #402 decryption SQL

COMBAT LOG DEBRIEF:
  • server/debrief.lua (yeni)
  • matrix_debrief_log tablosu
  • 5 chaos vektörü — determinizm + SQL inject + throttle
  • Deterministik jitter (0 RNG, checksum türevli)

FAZ 2.5 — POZİSYON SİSTEMİ (KAPANDI):
  • server/positions.lua (21 KB, yeni)
  • matrix_positions tablosu
  • 7 slot × 5 tip: 2 kapı, 2 çatı, 1 hub, 1 iç oda, 1 kaçış
  • LOS: mesafe + FOV + pitch (sayısal bonus YOK, fizik kuralı)
  • Reflex: ateş altında yedek slota geçiş (basit LAMBS özü)
  • Tick seyreltme (1sn), relevance culling
  • 5 chaos vektörü

KRİTİK VERİ BUG'I (CHAOS BİLE KAÇIRMIŞTI):
  • PersistBotWound 7 placeholder'a 4 değer gönderiyordu
  • DB'ye hiçbir şey yazılmıyordu (sessiz fail)
  • Fix: 7 değeri doğru sırayla gönder
  • KANIT: Bot #368 [KALICI SAKATLIK] → balistik imza DB'ye yazıldı

CHAIN TEST İZOLASYONU (IsRunning flag):
  • bureau.lua TriggerLockdown/LiftLockdown log guard
  • police_raid.lua raidIssued handler guard
  • matrix_diagnostics Run() başı/sonu flag toggle
  • KANIT: Boot log'unda [T4][BURO KILIDI] spam'i yok

════════════════════════════════════════════════════════════════════════
🗺️ BÖLÜM 4 — FAZ HARİTASI (DETAYLI)
════════════════════════════════════════════════════════════════════════

FAZ 2 — İstihbarat Ağı (kalan %29)
─────────────────────────────────────────────────────────────────────
✅ 2.1 Cinayet tespit (v4, client bridge + fallback)
✅ 2.2 Tanık FOV/LOS (30m, 120° FOV, LOS)
✅ 2.3 Cinayet → heat → raid zinciri (kalıcı DB)
✅ 2.4 LSPD aranma + kalıcı bölge mührü
✅ 2.5 Pozisyon sistemi (7 slot × 5 tip × LOS × reflex)
✅ 2.8 Polis interior breach (SyncRaidBucket)

⏳ 2.6 — Görev tipleri (8 tip → 4 tip ile başla)
   • Görev veren: çete başı AI (hub'lardan)
   • Görev alan: oyuncu + AI bot (simetri)
   • Tipler (4 minimal): Üretim, Nakliye, Sabotaj, İnfaz
   • Ödül: para + itibar + heat
   • Ceza: ölüm + heat + LSPD aranma
   • Hedef: oyuncu "amaç" görsün

⏳ 2.7 — /tayfaemri komutu
   • Sadece oyuncu → bot yönü (bot → oyuncu FAZ 6'ya)
   • Emirler: /işaret, /buraya, /kaç, /mevzi <slot>
   • AI cevap: "anlaşıldı" veya "yapamam (sebep)"
   • Hedef: oyuncu çeteyi koordine etsin

FAZ 3 — Diplomasi + LSPD + Mahkeme (40-65 saat)
─────────────────────────────────────────────────────────────────────
• LSPD wanted persistence (heat > 3 → sürekli takip)
• 5 birim: Asayiş, Narkotik, Mali, Siber, İstihbarat
   - Minimal: Asayiş + Narkotik aktif
• Mahkeme çekirdeği:
   - cinayet kaydı + tanık ifadesi → mahkumiyet skoru
   - balistik + DNA → FAZ 4'e
• Ateşkes mekaniği (iki çete arası)
• Faksiyon ilişkisi (düşman/müttefik)
• AI çete simetrisi
• Eş zamanlı operasyon (2 birim üst üste raid)
• OpenAI entegrasyonu → OPSİYONEL

FAZ 4 — Bölge Kontrolü (50-80 saat)
─────────────────────────────────────────────────────────────────────
• Fiziksel bölge kontrolü (şu an sayı)
• Bölge hub'ları fiziksel mekân
• Bölge savaşı: iki çete arası açık çatışma
• Balistik + DNA mahkemeye entegre
• Trap house el değiştirme
• Mahalle çalma/bırakma

FAZ 6 — Otonom AI Entegrasyonu (80-120 saat)
─────────────────────────────────────────────────────────────────────
• Kişilik → davranış (LAMBS danger.fsm mantığı)
• Uzmanlık → görev atama (chemist → üretim)
• Otonom çete başları:
   - Kendi kararlarını verir
   - Bütçe yönetir
   - Personel yönetir
• /tayfaemri iki yönlü (emir ↓ / rapor ↑)
• Gerçek tehdit haritası
• Grup koordinasyonu
• Suppressive fire tepkisi
• LAMBS full seviye

FAZ 7 — QBox Ekonomi (30-40 saat)
─────────────────────────────────────────────────────────────────────
• Banka bağlantısı (ox_banking / qbx_bank)
• Kara para → temiz para akışı
• Escrow (zaten kurulu)
• Fiziksel kasa (trap house içi)
• Vergi/FinCEN audit
• Çete başı bütçe yönetimi
• Bölge gelir dağılımı

════════════════════════════════════════════════════════════════════════
📁 BÖLÜM 5 — KRİTİK DOSYALAR
════════════════════════════════════════════════════════════════════════

Server (önemli):
- server/matrix_chaos.lua          (21 modül)
- server/matrix_chaos_cannibal.lua (8 vektör)
- server/matrix_network_guard.lua  (34 event + 124 rate)
- server/matrix_diagnostics.lua    (247 deep check)
- server/blackmarket.lua           (player_sim FIX)
- server/main.lua                  (Matrix.Log, Matrix.QBX)
- server/crime_witness.lua         ★ (FAZ 2.1+2.2+2.3)
- server/lspd_units.lua            ★ (FAZ 2.4)
- server/debrief.lua               ★ (FAZ 2.5 ek)
- server/positions.lua             ★ (FAZ 2.5)
- server/wound_system.lua          ★ (PersistBotWound fix)

Client:
- client/crime_witness_bridge.lua  ★ (FAZ 2.1)
- client/hud.lua                   (F6/K panel)

SQL:
- sql/matrix_MASTER.sql (tüm tablolar)

fxmanifest sırası (KRİTİK):
1. oxmysql
2. matrix_network_guard.lua  ← MUTLAKA main.lua'dan ÖNCE
3. main.lua
4. ... (diğerleri)
5. matrix_chaos.lua
6. matrix_chaos_cannibal.lua
7. ★ crime_witness.lua       ← chaos'tan SONRA
8. lspd_units.lua
9. debrief.lua
10. positions.lua  ← EN SON

════════════════════════════════════════════════════════════════════════
📚 BÖLÜM 6 — YAPMA / YAP
════════════════════════════════════════════════════════════════════════

❌ YAPMA:
❌ math.random
❌ DROP/ALTER TABLE (additive migration)
❌ Client'a güven
❌ Sessiz hata yutma
❌ Test sonuçlarını doğrulamadan OK deme
❌ RedEngine'i savunma aracı sanma
❌ Arcade mekanik ekleme
❌ Envanterdeki işaretlere körü körüne güvenme
❌ Client-side AC yazmaya kalkışmak
❌ Chaos duplicate modül (RegisterModule aynı isim 2 kez)
❌ math.atan2 (Lua 5.4'te yok — math.atan(y,x) kullan)
❌ Client-only event'i server'a RegisterNetEvent ile taşımak
❌ Sayısal bonus/buff (LoL mantığı — fizik kuralı zorunlu)

✅ YAP:
✅ Her IO pcall
✅ Event-driven (matrix:internal:*)
✅ Additive migration
✅ Self-healing
✅ Gerçekten doğrula
✅ Chaos'un kör noktalarını test et
✅ 40 sağlam dosyaya dokunma
✅ Debug print'leri iş bitince temizle
✅ gameEventTriggered sadece client'ta — bridge kur
✅ Chaos modülü eklerken uygun dosyaya koy
✅ FK constraint ve DB yazımını doğrula (kanıtı log'da)

⚠️ Kritik Uyarılar:
⚠️ Server-side güçlü (%94), client-side kasıtlı düşük (%8)
⚠️ gameEventTriggered SERVER-SIDE ÇALIŞMAZ → client bridge
⚠️ GetEntityHealth SERVER-SIDE 0 döner → client bridge
⚠️ IsPedDeadOrDying OneSync'te belirsiz → client bridge
⚠️ Fixture trap house silme (FK):
   SET FOREIGN_KEY_CHECKS = 0;
   DELETE FROM matrix_trap_houses WHERE label LIKE 'CHAOS-FIXTURE%';
   SET FOREIGN_KEY_CHECKS = 1;

════════════════════════════════════════════════════════════════════════
🚨 BÖLÜM 7 — KRİTİK WORKFLOW
════════════════════════════════════════════════════════════════════════

fxmanifest.lua'ya yeni dosya eklenince VEYA mevcut dosya değişince:

  1. refresh                  (fxmanifest cache yenile)
  2. restart vbs_core_matrix  (ZORUNLU — ensure değil!)
  3. Log'da [BOOT] satırını doğrula

Sadece restart → yeni dosya yüklenmez (fxmanifest cache eski)
Sadece ensure → cache tazelemez (restart lazım)
Sıralı: refresh + restart

Bu bug 5 kez yaşandı:
  Session 1 broker, lspd_units, debrief, positions, diagnostics-fix

ALTERNATİF: txAdmin panelinde kırmızı "stop" + "start"

════════════════════════════════════════════════════════════════════════
🎯 BÖLÜM 8 — OPTİMİZASYON STRATEJİSİ
════════════════════════════════════════════════════════════════════════

KURAL: Cover/pozisyon sayısı arttıkça server FPS düşer (Arma 3 sezgisi)

FIVEM GERÇEĞİ:
- FXServer ana thread tek çekirdek → her resource tick toplanır
- NPC AI server-side → visibility + pathfinding + cover hesabı
- O(n) veya O(n²) büyür → 40 bot × 20 cover = 800 hesap/tick

5 KATMANLI ÇÖZÜM:
  [A] Relevance culling — bot SADECE kendi slotunu görür (2 nokta)
  [B] Deterministic single-pass — "slot boş mu?" (O(1))
  [C] Tick seyreltme — 1 saniyede bir kontrol
  [D] Client-side offload — LOS/animasyon/aim client'ta
  [E] Routing bucket — TEK bucket tüm raid'ler

SONUÇ: 40 bot için ~0.3ms/tick. Server FPS 50 üstünde kalır.

ARMA 3 FELSEFESİ (şef sezgisi, doğrulanmış):
- LAMBS + NR6HAL + CF_BAI + kalabalık harita = AI aptallaşır
- Objeleri silmek FPS'e %1-2 etki eder
- Ama AI karar kalitesi %300 artar
- "Yılanın başını küçükken ez" = AI zekasını koru

FUNCTIONAL MINIMALISM:
- Vanilla statik props → RAGE zaten stream yapıyor, dokunma
- Sistemimizin props'ları → is_cover tag (FAZ 6)
- LAMBS AI zekası: tag yoksa "bu ne?" diye sorar → sapıtır

════════════════════════════════════════════════════════════════════════
🎯 BÖLÜM 9 — İKİ SAVAŞ DİLİ DOKTRİNİ
════════════════════════════════════════════════════════════════════════

POLİS (AI) — Askeri/LAPD doktrini:
  • Breach, overwatch, cutoff, stack
  • FAZ 3'te derinleşir (5 birim, çevirme, kordon)
  • Oyuncu KONTROL ETMEZ
  • Steel Beasts tarzı

ÇETE (oyuncu + AI) — İlkel sokak dili:
  • /işaret <koordinat> — bot oraya gider
  • /buraya — yanına çağır
  • /kaç — geri çekil
  • /mevzi <slot> — belirtilen slota git
  • Medeni değil, sokak refleksi

SİMETRİ: AI bot iki taraf için de aynı slot sistemini kullanır.
KANIT: FAZ 6'daki /tayfaemri bu altyapının üstüne kurulacak.

ÖRNEK:
  Polis: "Breach Team, stack on door 2"
  Çete:  /işaret 143.8 -1025.2 → bot oraya gider

════════════════════════════════════════════════════════════════════════
⚡ BÖLÜM 10 — HIZ STRATEJİSİ (v6.6.1)
════════════════════════════════════════════════════════════════════════

%40-50 HIZLANMA — İÇERİK AYNI, AKIŞ SIKILAŞTIRILDI

AI tarafı (ben):
  1. Kitap her faz kapanışında bump (v6.X)
  2. Tek satır fix → SADECE patch bloğu (dosya tamamı değil)
  3. Aynı dosyadaki 3+ fix → TEK mesajda
  4. PowerShell komutları → hazır şablon
  5. Test + kod → TEK mesajda
  6. Chaos + Diagnostics → paralel tetikleme
  7. Daha az temkinli — riskli işlemler hariç 2-adım kaldırıldı

Şef tarafı:
  8. "Şu dosyayı at" yerine "şu satırı değiştir" de
  9. Aynı gün içinde max 1 büyük faz (kapsam kiliti)
 10. Kitap güncel tutulmazsa hız kaybolur — bump zorunlu

SONUÇ:
  • Sıkı Beta: 75-105s → 45-65s
  • Full Beta: 120-180s → 75-105s
  • 12 saat/gün: 4-6 gün | 8 saat/gün: 6-9 gün

════════════════════════════════════════════════════════════════════════
📌 BÖLÜM 11 — NOTLAR
════════════════════════════════════════════════════════════════════════

★ PLAYTEST KURALI:
  "Aynı mekanik, aynı sunucu, aynı build → tekrar playtest YOK."
  Sadece yeni mekanik veya değiştirilen davranış için.

★ KAPSAM DİSİPLİNİ:
  Her FAZ için kapsam kilidi. Yeni fikir FAZ'a eklenmez.
  Yoksa "her faz 3 saat" norm olur.

★ POLİS AI-ONLY:
  Oyuncu polis tarafında OYNAMAZ. Kesin karar.

★ FUNCTIONAL MINIMALISM:
  FPS için değil, AI zekası için objeleri tag'le.

★ PERSISTBOTWOUND BUG'I:
  Chaos bile yakalayamadı — manuel diagnostic + log analizi.
  Her büyük fix sonrası DB'de gerçek veriyi doğrula.

★ CHAOS KÖR NOKTALARI (bilinen):
  1. Oyuncu tanık → chaos test edemez
  2. Oyuncu killer → chaos test edemez
  3. Uzak cinayet trap seçimi → mesafe eşiği yok
  4. Polis interior routing → bucket sync test edilmedi
  5. Ambient GTA AI araç sürme → bizim sistem değil
  6. Math.random taraması → whitelist dışı dosya eklendiğinde taranmıyor
  7. DB yazımı → chaos sadece RAM/event doğrular, SQL'i değil

★ SÜRE TAHMİNİ (gerçekçi):
  Sıkı Beta: 45-65 saat → 12h/gün: 4-6 gün
  Full Beta: 75-105 saat → 12h/gün: 6-9 gün
  Tam Sürüm: 200-300 saat → 12h/gün: 17-25 gün

════════════════════════════════════════════════════════════════════════
🔮 BÖLÜM 12 — MAHKEME VİZYONU
════════════════════════════════════════════════════════════════════════

DURUM:
- ŞU AN: HAYIR. Cinayet RAM'de yaşıyor, DB'de sadece kalıcı kayıt var.
- FAZ 2.3 SONRASI: KISMEN. Cinayet + tanık DB'ye yazılıyor.
- FAZ 3 SONRASI: TAM. Mahkeme cinayet + tanık + balistik + DNA'yı
  birleşik delil olarak okur.

KURULU TABLOLAR:
1. matrix_crime_log (cinayet kalıcı kaydı)
2. matrix_witness_statements (tanık ifadesi + confidence)

FAZ 3'te mahkeme skoru:
- Tek tanık → %40 mahkumiyet
- 3 tanık + balistik yok → %60
- 3 tanık + balistik → %100
- Tanık yok + balistik → %75
- Hiçbiri yok → %0

ZATEN KURULU (bureau.lua):
- Matrix.Bureau.OpenTrial
- Matrix.Bureau.RecordTrialResponse
- Matrix.Bureau.ExecuteVerdict

════════════════════════════════════════════════════════════════════════
📎 EKLER
════════════════════════════════════════════════════════════════════════

Ek-1: Chaos Komutları
/matrix_chaos_baslat <modul|all>
/matrix_chaos_baslat cannibal
/matrix_chaos_baslat self_check
/matrix_chaos_baslat network_guard_test
/matrix_chaos_baslat crime_witness_test
/matrix_chaos_baslat witness_fov_test
/matrix_chaos_baslat crime_chain_test
/matrix_chaos_baslat crime_edge_test
/matrix_chaos_baslat lspd_seal_test
/matrix_chaos_baslat lspd_wanted_test
/matrix_chaos_baslat live_spoof
/matrix_chaos_baslat sql_inject
/matrix_chaos_baslat sql_static_scan
/matrix_chaos_baslat cross_citizen_access
/matrix_chaos_rapor
/matrix_netguard_status

Ek-2: Diagnostics
/matrix_run_diagnostics         → hızlı
/matrix_run_diagnostics deep    → 247 deep
/matrix_diag_detay failed       → hataları göster
/matrix_diag_detay passed       → geçenleri göster
/matrix_diag_detay journal      → boot failure journal
/matrix_diag_detay breach       → hücre izolasyon ihlali
/matrix_diag_detay g <metin>    → grep
/matrix_diag_detay layer <N>    → katman filtresi
/matrix_diag_detay export       → JSON

Ek-3: Pozisyon Komutları (FAZ 2.5)
/slotseed <trapId>              → 7 slot oluştur
/mevzidurum <trapId>            → slot durumu

Ek-4: Debrief Komutu (FAZ 2.5 ek)
/debrief                        → son tehdit skorunu gör

Ek-5: Kritik Config
Config.Chaos.Enabled = true          -- PRODUCTION'DA false
Config.Chaos.AllowCannibal = true    -- PRODUCTION'DA false
Config.Diagnostics.RunOnResourceStart = true
Config.AI_Matrix_Brain.enabled = false
Config.AI_Matrix_Brain.provider = 'openai'

Ek-6: Fixture Prefix'leri
CHAOS-FIXTURE-TRAP-%03d
CHAOS-FIXTURE-BOT-%03d
CHAOS%03d (fleet)

Ek-7: Trust Audit Kapsamı (34 event)
Orijinal (3): reportSaleAttempt, buyWeapon, giveItemToBot
Report* (19): WeaponDischarge, DealerEliminated, CookAction,
  PlayerWounded, CortisolTrigger, VehicleEncircled, RaidOutcome,
  LspdCheckpoint, ObjectTouch, UnencryptedComms, ArsonSalvage,
  BotCaptured, DealerCombatDamage, DealerPoliceCollision,
  LatePayment, DeadDropForensic, LogisticsRun, VehicleShotFired,
  ★ reportKill
Yeni (12): buyVehicle, buyAmmo, buyBurnerPhone, buySpareBarrel,
  transferBotToBot, remoteWipe, purchaseCell, vendorPool:buyWeapon,
  districtHubs:assign, doorReinforcement:install, registerFleetVehicle,
  unassignFleetVehicle

Ek-8: Saldırı Vektör Matrisi
| Saldırı Tipi | Durum |
|---|---|
| Event flood | ✅ Engellenir |
| Argument spoof | ✅ Engellenir (34 event) |
| DoS | ✅ Engellenir |
| Ekonomi spam | ✅ Engellenir |
| SQL injection | ✅ Engellenir (parametrized) |
| SQL string concat | ✅ TARANDI (0 bulgu) |
| Cross-citizenid | ✅ TEST EDİLDİ |
| Live spoof | ✅ TEST EDİLDİ |
| Client injection | ❌ Test edilmedi (kabul) |
| Position teleport | ❌ Yakalanmaz (kabul) |
| Aimbot | ❌ Yakalanmaz (kabul) |
| Speed hack | ❌ Yakalanmaz (kabul) |
| God mode | ❌ Yakalanmaz (kabul) |
| Kernel exploit | ❌ İmkansız |

Ek-9: Client-Side AC Kararı
FAZ 1-5 iptal edildi. Sebep: arkadaş ortamı + DEA eğitimi + public değil.
Sadece crime_witness_bridge var (player intent için).
%72 → %95 hedefi İPTAL. Client-side AC hedef DEĞİL.

Ek-10: RedEngine Sorusu
"RedEngine bir HILE ARACIDIR (executor), anti-cheat değil.
Sunucunu korumaz, sadece client'ta çalışır."

════════════════════════════════════════════════════════════════════════
🎯 ULTIMATE HEDEF
════════════════════════════════════════════════════════════════════════

Server-authoritative simülasyon (client-side AC'siz)
Mahkemede birleşik delil: cinayet + tanık + balistik + DNA
VBS 4 = simülatör, oyun değil
"Arcade hiçbir şeye tahammülüm yok"
Coop arkadaşlarla ciddi sim deneyimi
Polis = AI (oynanmaz)

Unutma:
- Doğruluk > Kapsam
- Simetri kritik (AI = oyuncu)
- Zero-RNG zorunlu
- Her FAZ sonunda 15 dk playtest (yeni mekanik için)
- Kapsam kiliti (her faz kendi sınırında)

════════════════════════════════════════════════════════════════════════
KİTAP SONU — v6.6.1 TAM KİTAP
════════════════════════════════════════════════════════════════════════
