# Recap Pertemuan 3,4,5

- Text
    - [x]  Add text mesh pro
    - [x]  property text mesh pro yg umum digunakan
    - [x]  Manipulasi TextMeshProUGUI
        - Script
            
            ```jsx
            // Latihan2MengubahWarnaTeksTextMeshPro.cs
            
            using TMPro;
            using UnityEngine;
            
            /// <summary>
            /// Latihan 2: Mengubah warna sebagian teks menggunakan TextMeshPro.
            /// Script ini digunakan untuk menampilkan HP dengan warna berbeda
            /// berdasarkan jumlah HP saat ini.
            /// </summary>
            public class Latihan2MengubahWarnaTeksTextMeshPro : MonoBehaviour
            {
                [Header("UI References")]
                [SerializeField] private TextMeshProUGUI _statusText;
            
                [Header("HP Settings")]
                [SerializeField] private int _maxHealthPoint = 100;
                [SerializeField] private int _damageAmount = 25;
            
                private int healthPoint;
            
                /// <summary>
                /// Fungsi Start dipanggil satu kali saat game object pertama kali aktif.
                /// Di sini kita menyiapkan nilai awal HP.
                /// </summary>
                private void Start()
                {
                    // Saat game dimulai, HP dibuat penuh.
                    healthPoint = _maxHealthPoint;
            
                    // Menampilkan teks HP pertama kali.
                    UpdateHealthText();
                }
            
                /// <summary>
                /// Fungsi Update dipanggil setiap frame.
                /// Di sini kita mengecek apakah tombol Space ditekan.
                /// </summary>
                private void Update()
                {
                    // GetKeyDown berarti input hanya terbaca satu kali saat tombol baru ditekan.
                    if (Input.GetKeyDown(KeyCode.Space))
                    {
                        // Mengurangi HP sesuai jumlah damage.
                        healthPoint = healthPoint - _damageAmount;
            
                        // Jika HP sudah kurang dari 0, HP dikembalikan penuh.
                        if (healthPoint < 0)
                        {
                            healthPoint = _maxHealthPoint;
                        }
            
                        // Memperbarui tampilan teks HP setelah nilainya berubah.
                        UpdateHealthText();
                    }
                }
            
                /// <summary>
                /// Fungsi ini digunakan untuk memperbarui teks HP.
                /// Warna angka HP akan berubah berdasarkan nilai HP saat ini.
                /// </summary>
                private void UpdateHealthText()
                {
                    // Jika HP lebih dari 50, angka HP berwarna hijau.
                    if (healthPoint > 50)
                    {
                        _statusText.text = "HP: <color=green>" + healthPoint + "</color>";
                    }
                    // Jika HP lebih dari 25, angka HP berwarna kuning.
                    else if (healthPoint > 25)
                    {
                        _statusText.text = "HP: <color=yellow>" + healthPoint + "</color>";
                    }
                    // Jika HP 25 atau kurang, angka HP berwarna merah.
                    else
                    {
                        _statusText.text = "HP: <color=red>" + healthPoint + "</color>";
                    }
                }
            
                /// <summary>
                /// Fungsi ini bisa dipanggil dari Button melalui OnClick di Inspector.
                /// Ketika Button diklik, teks akan diganti menjadi pesan sederhana.
                /// </summary>
                public void ChangeText()
                {
                    _statusText.text = "Text is changed by Button";
                }
            }
            ```
            
- Button
    - [x]  Add button
    - [x]  Property button yg biasa digunakan
    - [x]  **Latihan 2: Ganti Teks Saat Button Diklik**
        - Script
            
            ```jsx
            // LatihanMengubahTeksDenganButton.cs
            
            using TMPro;
            using UnityEngine;
            using UnityEngine.UI;
            
            /// <summary>
            /// Latihan: Mengubah teks menggunakan Button.
            /// Script ini digunakan untuk mengganti isi TextMeshPro ketika sebuah Button diklik.
            /// </summary>
            public class LatihanMengubahTeksDenganButton : MonoBehaviour
            {
                [Header("UI References")]
                [SerializeField] private TextMeshProUGUI _messageText;
                [SerializeField] private Button _changeTextButton;
            
                /// <summary>
                /// Fungsi Start akan dipanggil satu kali saat game object pertama kali aktif.
                /// Di sini kita menyiapkan teks awal dan menghubungkan Button dengan fungsi ChangeText.
                /// </summary>
                private void Start()
                {
                    // Mengatur teks awal sebelum button diklik.
                    _messageText.text = "Belum diklik";
            
                    // Menambahkan fungsi ChangeText ke event onClick milik Button.
                    // Artinya, ketika button diklik, fungsi ChangeText akan dijalankan.
                    _changeTextButton.onClick.AddListener(ChangeText);
                }
            
                /// <summary>
                /// Fungsi ini dipanggil ketika button diklik.
                /// Fungsi ini akan mengganti isi teks pada komponen TextMeshProUGUI.
                /// </summary>
                private void ChangeText()
                {
                    // Mengubah teks setelah button diklik.
                    _messageText.text = "Button sudah diklik!";
                }
            
                /// <summary>
                /// Fungsi OnDestroy dipanggil ketika game object dihancurkan.
                /// Kita menghapus listener agar tidak ada event yang tertinggal.
                /// </summary>
                private void OnDestroy()
                {
                    _changeTextButton.onClick.RemoveListener(ChangeText);
                }
            }
            ```
            
    - [x]  **Latihan 3: Simulasi Menembak & Reload**
        - Script
            
            ```jsx
            // Latihan3MenembakDanReloadAmmo.cs
            
            using TMPro;
            using UnityEngine;
            using UnityEngine.UI;
            
            /// <summary>
            /// Latihan 3: Menembak dan reload ammo menggunakan Button.
            /// Script ini digunakan untuk mengurangi ammo saat tombol Shoot ditekan,
            /// dan mengisi ulang ammo saat tombol Reload ditekan.
            /// </summary>
            public class Latihan3MenembakDanReloadAmmo : MonoBehaviour
            {
                [Header("Ammo Settings")]
                public int MaxAmmo = 10;
                public int CurrentAmmo;
            
                [Header("UI References")]
                public TextMeshProUGUI TextAmmo;
                public Button ButtonShoot;
                public Button ButtonReload;
            
                /// <summary>
                /// Fungsi Start dipanggil satu kali saat game object pertama kali aktif.
                /// Di sini kita menyiapkan ammo awal dan menghubungkan button dengan fungsi.
                /// </summary>
                private void Start()
                {
                    // Saat game dimulai, ammo langsung dibuat penuh.
                    CurrentAmmo = MaxAmmo;
            
                    // Menampilkan jumlah ammo ke UI.
                    UpdateAmmoText();
            
                    // Menghubungkan tombol Shoot dengan fungsi Shoot.
                    // Jadi saat ButtonShoot diklik, fungsi Shoot akan dijalankan.
                    ButtonShoot.onClick.AddListener(Shoot);
            
                    // Menghubungkan tombol Reload dengan fungsi Reload.
                    ButtonReload.onClick.AddListener(Reload);
            
                    // Mengecek kondisi tombol di awal game.
                    UpdateButtonState();
                }
            
                /// <summary>
                /// Fungsi ini dipanggil ketika tombol Shoot ditekan.
                /// Fungsi ini akan mengurangi ammo sebanyak 1.
                /// </summary>
                public void Shoot()
                {
                    // Jika ammo sudah habis, fungsi langsung berhenti.
                    // Ini untuk mencegah CurrentAmmo menjadi angka negatif.
                    if (CurrentAmmo <= 0)
                    {
                        return;
                    }
            
                    // Mengurangi ammo sebanyak 1.
                    CurrentAmmo = CurrentAmmo - 1;
            
                    // Memperbarui teks ammo di UI.
                    UpdateAmmoText();
            
                    // Memperbarui kondisi tombol setelah menembak.
                    UpdateButtonState();
                }
            
                /// <summary>
                /// Fungsi ini dipanggil ketika tombol Reload ditekan.
                /// Fungsi ini akan mengisi ammo kembali sampai penuh.
                /// </summary>
                public void Reload()
                {
                    // Mengisi kembali ammo sampai jumlah maksimum.
                    CurrentAmmo = MaxAmmo;
            
                    // Memperbarui teks ammo di UI.
                    UpdateAmmoText();
            
                    // Memperbarui kondisi tombol setelah reload.
                    UpdateButtonState();
                }
            
                /// <summary>
                /// Fungsi ini digunakan untuk memperbarui teks ammo.
                /// Contoh hasil teks: 10/10, 9/10, 0/10.
                /// </summary>
                private void UpdateAmmoText()
                {
                    TextAmmo.text = CurrentAmmo + "/" + MaxAmmo;
                }
            
                /// <summary>
                /// Fungsi ini digunakan untuk mengatur apakah tombol bisa diklik atau tidak.
                /// </summary>
                private void UpdateButtonState()
                {
                    // Tombol Shoot hanya bisa diklik jika ammo masih lebih dari 0.
                    ButtonShoot.interactable = CurrentAmmo > 0;
            
                    // Tombol Reload hanya bisa diklik jika ammo belum penuh.
                    ButtonReload.interactable = CurrentAmmo < MaxAmmo;
                }
            
                /// <summary>
                /// Fungsi OnDestroy dipanggil ketika game object dihancurkan.
                /// Listener dihapus agar event tidak tertinggal.
                /// </summary>
                private void OnDestroy()
                {
                    ButtonShoot.onClick.RemoveListener(Shoot);
                    ButtonReload.onClick.RemoveListener(Reload);
                }
            }
            ```
            
- Image
    - [x]  Add Image
    - [x]  Property Image yg biasa digunakan
    - [x]  **Latihan 4 mengganti Sprite pada komponen Image**
        - Script
            
            ```jsx
            // Latihan4MenggantiSpritePadaKomponenImage.cs
            
            using TMPro;
            using UnityEngine;
            using UnityEngine.UI;
            
            /// <summary>
            /// Latihan 4: Mengganti Sprite pada komponen Image.
            /// Script ini digunakan untuk membuat tampilan gambar yang bisa berpindah halaman
            /// menggunakan tombol Previous dan Next.
            /// </summary>
            public class Latihan4MenggantiSpritePadaKomponenImage : MonoBehaviour
            {
                [Header("UI References")]
                public Image Gambar;
                public Button ButtonPrev, ButtonNext;
                public TextMeshProUGUI TeksHalaman;
            
                [Header("Page Settings")]
                public int MaxPage = 3;
            
                [Header("Image Data")]
                public Sprite[] KumpulanGambar;
            
                private int currentPage;
            
                private void Start()
                {
                    Initialize();
                }
            
                /// <summary>
                /// Menyiapkan kondisi awal saat game dimulai.
                /// Halaman dimulai dari halaman 1.
                /// </summary>
                private void Initialize()
                {
                    currentPage = 1;
            
                    // Menampilkan teks halaman, contoh: 1/3.
                    TeksHalaman.text = currentPage + "/" + MaxPage;
            
                    // Array dimulai dari index 0.
                    // Karena currentPage dimulai dari 1, maka perlu dikurangi 1.
                    Gambar.sprite = KumpulanGambar[currentPage - 1];
            
                    // Menambahkan fungsi yang akan dipanggil ketika tombol diklik.
                    ButtonNext.onClick.AddListener(OnNextButtonPressed);
                    ButtonPrev.onClick.AddListener(OnPrevButtonPressed);
            
                    // Saat masih di halaman pertama, tombol Prev tidak perlu ditampilkan.
                    ButtonPrev.gameObject.SetActive(false);
                }
            
                /// <summary>
                /// Dipanggil ketika tombol Next ditekan.
                /// Fungsi ini akan memindahkan gambar ke halaman berikutnya.
                /// </summary>
                public void OnNextButtonPressed()
                {
                    // Menambah nomor halaman sebanyak 1.
                    currentPage = currentPage + 1;
            
                    // Memperbarui teks halaman setelah currentPage berubah.
                    TeksHalaman.text = currentPage + "/" + MaxPage;
            
                    // Mengganti sprite Image sesuai halaman saat ini.
                    // Contoh: halaman 2 menggunakan KumpulanGambar[1].
                    Gambar.sprite = KumpulanGambar[currentPage - 1];
            
                    // Jika sudah sampai halaman terakhir,
                    // tombol Next disembunyikan agar halaman tidak lewat dari MaxPage.
                    if (currentPage == MaxPage)
                    {
                        ButtonNext.gameObject.SetActive(false);
                    }
            
                    // Jika bukan halaman pertama,
                    // tombol Prev ditampilkan agar player bisa kembali ke halaman sebelumnya.
                    if (currentPage != 1)
                    {
                        ButtonPrev.gameObject.SetActive(true);
                    }
                }
            
                /// <summary>
                /// Dipanggil ketika tombol Previous ditekan.
                /// Fungsi ini akan memindahkan gambar ke halaman sebelumnya.
                /// </summary>
                public void OnPrevButtonPressed()
                {
                    // Mengurangi nomor halaman sebanyak 1.
                    currentPage = currentPage - 1;
            
                    // Memperbarui teks halaman setelah currentPage berubah.
                    TeksHalaman.text = currentPage + "/" + MaxPage;
            
                    // Mengganti sprite Image sesuai halaman saat ini.
                    Gambar.sprite = KumpulanGambar[currentPage - 1];
            
                    // Jika sudah kembali ke halaman pertama,
                    // tombol Prev disembunyikan agar halaman tidak menjadi 0.
                    if (currentPage == 1)
                    {
                        ButtonPrev.gameObject.SetActive(false);
                    }
            
                    // Jika belum berada di halaman terakhir,
                    // tombol Next ditampilkan kembali.
                    if (currentPage != MaxPage)
                    {
                        ButtonNext.gameObject.SetActive(true);
                    }
                }
            }
            ```
            
    - [x]  **Latihan 5:  mengganti Color pada komponen Image**
        - Menggunakan Update
            
            ```jsx
            // Latihan5EfekDamageHealMenggunakanUpdate.cs
            
            using TMPro;
            using UnityEngine;
            using UnityEngine.UI;
            
            /// <summary>
            /// Latihan 5: Efek damage dan heal menggunakan komponen Image.
            /// Script ini digunakan untuk mengubah warna layar saat player terkena damage atau mendapatkan heal.
            /// Efek transparansi gambar akan dikurangi perlahan menggunakan fungsi Update.
            /// </summary>
            public class Latihan5EfekDamageHealMenggunakanUpdate : MonoBehaviour
            {
                [Header("UI References")]
                [SerializeField] private TextMeshProUGUI _hpText;
                [SerializeField] private TextMeshProUGUI _statusText;
                [SerializeField] private Button _damageButton;
                [SerializeField] private Button _healButton;
                [SerializeField] private Image _effectImage;
            
                [Header("HP Settings")]
                [SerializeField] private int _maxHp = 100;
                [SerializeField] private int _damageAmount = 10;
                [SerializeField] private int _healAmount = 10;
            
                [Header("Effect Settings")]
                [SerializeField, Range(0f, 1f)] private float _damageAlpha = 0.6f;
                [SerializeField, Range(0f, 1f)] private float _healAlpha = 0.4f;
                [SerializeField, Range(0f, 1f)] private float _lowHpAlpha = 0.2f;
                [SerializeField] private float _fadeSpeed = 2.5f;
            
                private int currentHp;
                private Color currentEffectColor;
                private float currentAlpha;
                private float targetAlpha;
            
                /// <summary>
                /// Fungsi Awake dipanggil sebelum Start.
                /// Di sini kita menyiapkan nilai awal HP dan efek gambar.
                /// </summary>
                private void Awake()
                {
                    // Jika Max HP kurang dari 1, kita paksa menjadi 1 agar HP tidak bernilai 0 dari awal.
                    if (_maxHp < 1)
                    {
                        _maxHp = 1;
                    }
            
                    // Saat game dimulai, HP dibuat penuh.
                    currentHp = _maxHp;
            
                    // Warna awal efek dibuat merah, tetapi alpha-nya 0 sehingga tidak terlihat.
                    currentEffectColor = Color.red;
                    currentAlpha = 0f;
                    targetAlpha = 0f;
                }
            
                /// <summary>
                /// Fungsi Start dipanggil satu kali saat game object aktif.
                /// Di sini kita menghubungkan button dengan fungsi damage dan heal.
                /// </summary>
                private void Start()
                {
                    // Ketika tombol damage diklik, fungsi TakeDamage akan dijalankan.
                    _damageButton.onClick.AddListener(TakeDamage);
            
                    // Ketika tombol heal diklik, fungsi Heal akan dijalankan.
                    _healButton.onClick.AddListener(Heal);
            
                    // Menampilkan status awal.
                    UpdateStatusText("HP penuh. Siap bermain.");
            
                    // Memperbarui tampilan UI di awal game.
                    UpdateUI();
                    UpdateEffectImageColor();
                }
            
                /// <summary>
                /// Fungsi Update dipanggil setiap frame.
                /// Di sini alpha pada gambar efek akan bergerak perlahan menuju targetAlpha.
                /// </summary>
                private void Update()
                {
                    // Jika alpha sekarang lebih besar dari target,
                    // maka alpha dikurangi sedikit demi sedikit.
                    if (currentAlpha > targetAlpha)
                    {
                        currentAlpha -= _fadeSpeed * Time.deltaTime;
            
                        // Jika pengurangan alpha terlalu jauh melewati target,
                        // langsung samakan dengan target.
                        if (currentAlpha < targetAlpha)
                        {
                            currentAlpha = targetAlpha;
                        }
            
                        UpdateEffectImageColor();
                    }
                    // Jika alpha sekarang lebih kecil dari target,
                    // maka alpha ditambah sedikit demi sedikit.
                    else if (currentAlpha < targetAlpha)
                    {
                        currentAlpha += _fadeSpeed * Time.deltaTime;
            
                        // Jika penambahan alpha terlalu jauh melewati target,
                        // langsung samakan dengan target.
                        if (currentAlpha > targetAlpha)
                        {
                            currentAlpha = targetAlpha;
                        }
            
                        UpdateEffectImageColor();
                    }
                }
            
                /// <summary>
                /// Fungsi OnDestroy dipanggil ketika game object dihancurkan.
                /// Listener dihapus agar event button tidak tertinggal.
                /// </summary>
                private void OnDestroy()
                {
                    _damageButton.onClick.RemoveListener(TakeDamage);
                    _healButton.onClick.RemoveListener(Heal);
                }
            
                /// <summary>
                /// Fungsi ini dipanggil ketika tombol Damage ditekan.
                /// HP akan berkurang, lalu layar diberi efek warna merah.
                /// </summary>
                private void TakeDamage()
                {
                    // Mengurangi HP sesuai jumlah damage.
                    currentHp -= _damageAmount;
            
                    // Memastikan HP tidak lebih kecil dari 0 dan tidak lebih besar dari Max HP.
                    currentHp = ClampHpValue(currentHp);
            
                    // Mengatur warna efek menjadi merah.
                    currentEffectColor = Color.red;
            
                    // Alpha langsung dibuat cukup besar agar efek merah terlihat.
                    currentAlpha = _damageAlpha;
            
                    // Target alpha menentukan efek akan menghilang total atau tersisa sedikit saat HP rendah.
                    targetAlpha = GetLowHpAlpha();
            
                    if (currentHp <= 0)
                    {
                        UpdateStatusText("Player kalah.");
                    }
                    else if (IsHpLow())
                    {
                        UpdateStatusText("HP rendah!");
                    }
                    else
                    {
                        UpdateStatusText("Player terkena damage.");
                    }
            
                    UpdateUI();
                    UpdateEffectImageColor();
                }
            
                /// <summary>
                /// Fungsi ini dipanggil ketika tombol Heal ditekan.
                /// HP akan bertambah, lalu layar diberi efek warna hijau.
                /// </summary>
                private void Heal()
                {
                    // Menambah HP sesuai jumlah heal.
                    currentHp += _healAmount;
            
                    // Memastikan HP tidak lebih kecil dari 0 dan tidak lebih besar dari Max HP.
                    currentHp = ClampHpValue(currentHp);
            
                    // Mengatur warna efek menjadi hijau.
                    currentEffectColor = Color.green;
            
                    // Alpha langsung dibuat cukup besar agar efek hijau terlihat.
                    currentAlpha = _healAlpha;
            
                    // Target alpha menentukan efek akan menghilang total atau tersisa sedikit saat HP rendah.
                    targetAlpha = GetLowHpAlpha();
            
                    if (currentHp >= _maxHp)
                    {
                        UpdateStatusText("HP penuh kembali.");
                    }
                    else
                    {
                        UpdateStatusText("Player mendapatkan heal.");
                    }
            
                    UpdateUI();
                    UpdateEffectImageColor();
                }
            
                /// <summary>
                /// Fungsi ini digunakan untuk menjaga nilai HP agar tetap berada di antara 0 dan Max HP.
                /// </summary>
                private int ClampHpValue(int hpValue)
                {
                    if (hpValue < 0)
                    {
                        return 0;
                    }
            
                    if (hpValue > _maxHp)
                    {
                        return _maxHp;
                    }
            
                    return hpValue;
                }
            
                /// <summary>
                /// Fungsi ini digunakan untuk memperbarui seluruh tampilan UI.
                /// </summary>
                private void UpdateUI()
                {
                    UpdateHpText();
                    UpdateButtonStates();
                }
            
                /// <summary>
                /// Fungsi ini digunakan untuk memperbarui teks HP.
                /// Warna teks HP akan berubah berdasarkan jumlah HP saat ini.
                /// </summary>
                private void UpdateHpText()
                {
                    string hpColor = "white";
            
                    // Jika HP berada di 25% atau kurang, teks HP menjadi merah.
                    if (currentHp <= _maxHp * 0.25f)
                    {
                        hpColor = "red";
                    }
                    // Jika HP berada di 50% atau kurang, teks HP menjadi kuning.
                    else if (currentHp <= _maxHp * 0.5f)
                    {
                        hpColor = "yellow";
                    }
            
                    _hpText.text = "HP: <color=" + hpColor + ">" + currentHp + "</color>/" + _maxHp;
                }
            
                /// <summary>
                /// Fungsi ini digunakan untuk mengatur apakah tombol bisa diklik atau tidak.
                /// </summary>
                private void UpdateButtonStates()
                {
                    // Tombol damage hanya bisa diklik jika HP masih lebih dari 0.
                    _damageButton.interactable = currentHp > 0;
            
                    // Tombol heal hanya bisa diklik jika HP belum penuh.
                    _healButton.interactable = currentHp < _maxHp;
                }
            
                /// <summary>
                /// Fungsi ini digunakan untuk memperbarui warna dan transparansi Image efek.
                /// </summary>
                private void UpdateEffectImageColor()
                {
                    Color color = currentEffectColor;
            
                    // Alpha menentukan transparansi.
                    // 0 berarti tidak terlihat, 1 berarti terlihat penuh.
                    color.a = currentAlpha;
            
                    _effectImage.color = color;
                }
            
                /// <summary>
                /// Fungsi ini digunakan untuk mengganti teks status.
                /// </summary>
                private void UpdateStatusText(string message)
                {
                    _statusText.text = message;
                }
            
                /// <summary>
                /// Fungsi ini mengecek apakah HP sedang rendah.
                /// Di script ini, HP dianggap rendah jika berada di 25% atau kurang.
                /// </summary>
                private bool IsHpLow()
                {
                    return currentHp <= _maxHp * 0.25f;
                }
            
                /// <summary>
                /// Fungsi ini menentukan alpha tujuan setelah efek damage atau heal muncul.
                /// Jika HP rendah, efek akan tetap terlihat sedikit.
                /// Jika HP tidak rendah, efek akan hilang sampai alpha 0.
                /// </summary>
                private float GetLowHpAlpha()
                {
                    if (IsHpLow())
                    {
                        return _lowHpAlpha;
                    }
            
                    return 0f;
                }
            }
            ```
            
        - Menggunakan Coroutine
            
            ```jsx
            // Latihan5EfekDamageHealMenggunakanCoroutine.cs
            
            using System.Collections;
            using TMPro;
            using UnityEngine;
            using UnityEngine.UI;
            
            /// <summary>
            /// Latihan 5: Efek damage dan heal menggunakan Coroutine.
            /// Script ini digunakan untuk mengubah warna layar saat player terkena damage atau mendapatkan heal.
            /// Efek transparansi gambar akan dikurangi perlahan menggunakan Coroutine dan while.
            /// </summary>
            public class Latihan5EfekDamageHealMenggunakanCoroutine : MonoBehaviour
            {
                [Header("UI References")]
                [SerializeField] private TextMeshProUGUI _hpText;
                [SerializeField] private TextMeshProUGUI _statusText;
                [SerializeField] private Button _damageButton;
                [SerializeField] private Button _healButton;
                [SerializeField] private Image _effectImage;
            
                [Header("HP Settings")]
                [SerializeField] private int _maxHp = 100;
                [SerializeField] private int _damageAmount = 10;
                [SerializeField] private int _healAmount = 10;
            
                [Header("Effect Settings")]
                [SerializeField, Range(0f, 1f)] private float _damageAlpha = 0.6f;
                [SerializeField, Range(0f, 1f)] private float _healAlpha = 0.4f;
                [SerializeField, Range(0f, 1f)] private float _lowHpAlpha = 0.2f;
                [SerializeField] private float _fadeSpeed = 2.5f;
            
                private int currentHp;
                private Color currentEffectColor;
                private float currentAlpha;
                private float targetAlpha;
                private Coroutine fadeCoroutine;
            
                /// <summary>
                /// Fungsi Awake dipanggil sebelum Start.
                /// Di sini kita menyiapkan nilai awal HP dan efek gambar.
                /// </summary>
                private void Awake()
                {
                    // Jika Max HP kurang dari 1, kita paksa menjadi 1 agar HP tidak bernilai 0 dari awal.
                    if (_maxHp < 1)
                    {
                        _maxHp = 1;
                    }
            
                    // Saat game dimulai, HP dibuat penuh.
                    currentHp = _maxHp;
            
                    // Warna awal efek dibuat merah, tetapi alpha-nya 0 sehingga tidak terlihat.
                    currentEffectColor = Color.red;
                    currentAlpha = 0f;
                    targetAlpha = 0f;
                }
            
                /// <summary>
                /// Fungsi Start dipanggil satu kali saat game object aktif.
                /// Di sini kita menghubungkan button dengan fungsi damage dan heal.
                /// </summary>
                private void Start()
                {
                    // Ketika tombol damage diklik, fungsi TakeDamage akan dijalankan.
                    _damageButton.onClick.AddListener(TakeDamage);
            
                    // Ketika tombol heal diklik, fungsi Heal akan dijalankan.
                    _healButton.onClick.AddListener(Heal);
            
                    // Menampilkan status awal.
                    UpdateStatusText("HP penuh. Siap bermain.");
            
                    // Memperbarui tampilan UI di awal game.
                    UpdateUI();
                    UpdateEffectImageColor();
                }
            
                /// <summary>
                /// Fungsi OnDestroy dipanggil ketika game object dihancurkan.
                /// Listener dihapus agar event button tidak tertinggal.
                /// </summary>
                private void OnDestroy()
                {
                    _damageButton.onClick.RemoveListener(TakeDamage);
                    _healButton.onClick.RemoveListener(Heal);
                }
            
                /// <summary>
                /// Fungsi ini dipanggil ketika tombol Damage ditekan.
                /// HP akan berkurang, lalu layar diberi efek warna merah.
                /// </summary>
                private void TakeDamage()
                {
                    // Mengurangi HP sesuai jumlah damage.
                    currentHp -= _damageAmount;
            
                    // Memastikan HP tidak lebih kecil dari 0 dan tidak lebih besar dari Max HP.
                    currentHp = ClampHpValue(currentHp);
            
                    // Mengatur warna efek menjadi merah.
                    currentEffectColor = Color.red;
            
                    // Alpha langsung dibuat cukup besar agar efek merah terlihat.
                    currentAlpha = _damageAlpha;
            
                    // Target alpha menentukan efek akan menghilang total atau tersisa sedikit saat HP rendah.
                    targetAlpha = GetLowHpAlpha();
            
                    if (currentHp <= 0)
                    {
                        UpdateStatusText("Player kalah.");
                    }
                    else if (IsHpLow())
                    {
                        UpdateStatusText("HP rendah!");
                    }
                    else
                    {
                        UpdateStatusText("Player terkena damage.");
                    }
            
                    UpdateUI();
                    UpdateEffectImageColor();
                    StartFadeEffect();
                }
            
                /// <summary>
                /// Fungsi ini dipanggil ketika tombol Heal ditekan.
                /// HP akan bertambah, lalu layar diberi efek warna hijau.
                /// </summary>
                private void Heal()
                {
                    // Menambah HP sesuai jumlah heal.
                    currentHp += _healAmount;
            
                    // Memastikan HP tidak lebih kecil dari 0 dan tidak lebih besar dari Max HP.
                    currentHp = ClampHpValue(currentHp);
            
                    // Mengatur warna efek menjadi hijau.
                    currentEffectColor = Color.green;
            
                    // Alpha langsung dibuat cukup besar agar efek hijau terlihat.
                    currentAlpha = _healAlpha;
            
                    // Target alpha menentukan efek akan menghilang total atau tersisa sedikit saat HP rendah.
                    targetAlpha = GetLowHpAlpha();
            
                    if (currentHp >= _maxHp)
                    {
                        UpdateStatusText("HP penuh kembali.");
                    }
                    else
                    {
                        UpdateStatusText("Player mendapatkan heal.");
                    }
            
                    UpdateUI();
                    UpdateEffectImageColor();
                    StartFadeEffect();
                }
            
                /// <summary>
                /// Fungsi ini digunakan untuk menjaga nilai HP agar tetap berada di antara 0 dan Max HP.
                /// </summary>
                private int ClampHpValue(int hpValue)
                {
                    if (hpValue < 0)
                    {
                        return 0;
                    }
            
                    if (hpValue > _maxHp)
                    {
                        return _maxHp;
                    }
            
                    return hpValue;
                }
            
                /// <summary>
                /// Fungsi ini digunakan untuk memulai Coroutine fade.
                /// Jika Coroutine sebelumnya masih berjalan, Coroutine lama akan dihentikan dulu.
                /// </summary>
                private void StartFadeEffect()
                {
                    if (fadeCoroutine != null)
                    {
                        StopCoroutine(fadeCoroutine);
                    }
            
                    fadeCoroutine = StartCoroutine(FadeEffectRoutine());
                }
            
                /// <summary>
                /// Coroutine ini digunakan untuk mengubah alpha secara perlahan sampai mencapai targetAlpha.
                /// Perulangan while akan berjalan selama currentAlpha belum sama dengan targetAlpha.
                /// </summary>
                private IEnumerator FadeEffectRoutine()
                {
                    while (currentAlpha != targetAlpha)
                    {
                        // Jika alpha sekarang lebih besar dari target,
                        // maka alpha dikurangi sedikit demi sedikit.
                        if (currentAlpha > targetAlpha)
                        {
                            currentAlpha -= _fadeSpeed * Time.deltaTime;
            
                            // Jika pengurangan alpha terlalu jauh melewati target,
                            // langsung samakan dengan target.
                            if (currentAlpha < targetAlpha)
                            {
                                currentAlpha = targetAlpha;
                            }
                        }
                        // Jika alpha sekarang lebih kecil dari target,
                        // maka alpha ditambah sedikit demi sedikit.
                        else if (currentAlpha < targetAlpha)
                        {
                            currentAlpha += _fadeSpeed * Time.deltaTime;
            
                            // Jika penambahan alpha terlalu jauh melewati target,
                            // langsung samakan dengan target.
                            if (currentAlpha > targetAlpha)
                            {
                                currentAlpha = targetAlpha;
                            }
                        }
            
                        UpdateEffectImageColor();
            
                        // Menunggu 1 frame sebelum lanjut ke pengulangan berikutnya.
                        yield return null;
                    }
            
                    // Jika fade sudah selesai, penanda Coroutine dikosongkan kembali.
                    fadeCoroutine = null;
                }
            
                /// <summary>
                /// Fungsi ini digunakan untuk memperbarui seluruh tampilan UI.
                /// </summary>
                private void UpdateUI()
                {
                    UpdateHpText();
                    UpdateButtonStates();
                }
            
                /// <summary>
                /// Fungsi ini digunakan untuk memperbarui teks HP.
                /// Warna teks HP akan berubah berdasarkan jumlah HP saat ini.
                /// </summary>
                private void UpdateHpText()
                {
                    string hpColor = "white";
            
                    // Jika HP berada di 25% atau kurang, teks HP menjadi merah.
                    if (currentHp <= _maxHp * 0.25f)
                    {
                        hpColor = "red";
                    }
                    // Jika HP berada di 50% atau kurang, teks HP menjadi kuning.
                    else if (currentHp <= _maxHp * 0.5f)
                    {
                        hpColor = "yellow";
                    }
            
                    _hpText.text = "HP: <color=" + hpColor + ">" + currentHp + "</color>/" + _maxHp;
                }
            
                /// <summary>
                /// Fungsi ini digunakan untuk mengatur apakah tombol bisa diklik atau tidak.
                /// </summary>
                private void UpdateButtonStates()
                {
                    // Tombol damage hanya bisa diklik jika HP masih lebih dari 0.
                    _damageButton.interactable = currentHp > 0;
            
                    // Tombol heal hanya bisa diklik jika HP belum penuh.
                    _healButton.interactable = currentHp < _maxHp;
                }
            
                /// <summary>
                /// Fungsi ini digunakan untuk memperbarui warna dan transparansi Image efek.
                /// </summary>
                private void UpdateEffectImageColor()
                {
                    Color color = currentEffectColor;
            
                    // Alpha menentukan transparansi.
                    // 0 berarti tidak terlihat, 1 berarti terlihat penuh.
                    color.a = currentAlpha;
            
                    _effectImage.color = color;
                }
            
                /// <summary>
                /// Fungsi ini digunakan untuk mengganti teks status.
                /// </summary>
                private void UpdateStatusText(string message)
                {
                    _statusText.text = message;
                }
            
                /// <summary>
                /// Fungsi ini mengecek apakah HP sedang rendah.
                /// Di script ini, HP dianggap rendah jika berada di 25% atau kurang.
                /// </summary>
                private bool IsHpLow()
                {
                    return currentHp <= _maxHp * 0.25f;
                }
            
                /// <summary>
                /// Fungsi ini menentukan alpha tujuan setelah efek damage atau heal muncul.
                /// Jika HP rendah, efek akan tetap terlihat sedikit.
                /// Jika HP tidak rendah, efek akan hilang sampai alpha 0.
                /// </summary>
                private float GetLowHpAlpha()
                {
                    if (IsHpLow())
                    {
                        return _lowHpAlpha;
                    }
            
                    return 0f;
                }
            }
            ```
            
    - Latihan 6: **Fill Amount: Reload Progress**
        - Script