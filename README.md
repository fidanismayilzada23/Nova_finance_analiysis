# 🛍️ Nova Finance Analytics

> Çirkli e‑ticaret datasının təmizlənməsi, müştəri davranışlarının təhlili və interaktiv Power BI dashboard hazırlanması.

---

## 📌 Layihə haqqında

| Xüsusiyyət | Məlumat |
|-----------|---------|
| **Məqsəd** | Data təmizləmə, müştəri/xərc/fraud analizi, Power BI dashboard |
| **Texnologiyalar** | Python, SQL, Power BI, Excel |
| **Data həcmi** | 5600+ sətir, 20+ sütun |

---

## 📁 Repo strukturu
```
📦 Finans-E-ticaret-Analitika-Layihəsi
┣ 📂 data_set
┃ ┣ 📜 Finance_Ecommerce_Dirty_Dataset_csv.csv # Orijinal çirkli data
┃ ┗ 📜 nova_finance_temiz_data.csv # Təmizlənmiş data
┣ 📂 notebooks
┃ ┗ 📜 bitirme_projesi.py # Python kodu (Colab)
┣ 📂 powerbi
┃ ┣ 📜 Nova finance.pbix # Power BI dashboard
┃ ┣ 📜 Powerbi proje.pdf
┃ ┗ 📜 Daxlar.txt
┣ 📂 excel
┃ ┗ 📜 Novafinancepivottabel.xlsx # Excel pivot analiz
┣ 📂 presentation
┃ ┗ 📜 powerbi proje.pdf # Təqdimat
┣ 📜 README.md
```

---

## 🔧 1. Data təmizləmə və hazırlıq (Python)

**Görülən işlər:**

| Addım | Əməliyyat |
|-------|-----------|
| 1 | Gizli boşluqların silinməsi |
| 2 | Null dəyərlərin sayının müəyyən edilməsi |
| 3 | Tarix sütununun düzənlənməsi |
| 4 | TransactionID səhvlərinin düzəldilməsi, dublikatların silinməsi |
| 5 | TransactionType, Currency, IsFraud standartlaşdırılması (mapping ilə) |
| 6 | Merchant mail, telefon, postal code, kategoriya və subkategoriyada yazım xətalarının düzəldilməsi |
| 7 | Amount və Balance sütunlarında xüsusi simvolların təmizlənməsi, numeric-ə çevrilməsi |
| 8 | ExchangeRate ilə **Amount_Base** (USD bazalı məbləğ) yaradılması |
| 9 | Outlier analizi və Log transformasiyası |

**Nəticə:** 5671 sətir, 22 sütun – təmiz, analizə hazır data.

📓 `notebooks/bitirme_projesi.py`

---

## 📊 2. İlkin analiz və hipotez testləri (Python)

### Statistik testlər:

| Hipotez | Test | Nəticə |
|---------|------|--------|
| Kateqoriya ilə məbləğ arasında fərq var | ANOVA | ❌ Təsir yoxdur (p=0.97) |
| Həftə sonu / içi xərcləmə fərqlidir | Mann-Whitney U | ❌ Fərq yoxdur (p=0.0878; U p=0.15) |
| Ölkə ilə məbləğ arasında fərq var | ANOVA | ❌ Təsir yoxdur (p=0.69) |

### Əsas tapıntılar:

| Tapıntı | Ətraflı |
|---------|---------|
| **Amount Base paylanması** | Sağa çarpıqlıq var – bəzi müştərilərin yüksək ödənişləri statistik nəticəyə təsir edir. Müştərilərin 75%-i aşağı ödənişlər edir. |
| **Ödəniş növləri** | Credit 32%, Debit 51%, Refund 16%. Median məbləğlər bir-birinə yaxındır. |
| **Həftə sonu / içi** | Həftə içi 4091, həftə sonu 1580 əməliyyat. Orta məbləğ dəyişmir. |
| **Ölkələr** | Hansı ölkədə olmasından asılı olmayaraq müştərilər eyni orta məbləğdə ödəniş edir. |

📓 `notebooks/bitirme_projesi.py`

---

## 🗄️ 3. SQL analizi

### Əsas sorğu nəticələri:

| Sorğu | Nəticə |
|-------|--------|
| **İşlem tipinə görə həcm** | Debit 51%, Credit 33%, Refund 16% |
| **Ən aktiv şəhərlər** | Hyderabad, Gurugram, Chennai, Mumbai, Pune, Delhi, Kolkata, Bengaluru, Jaipur |
| **Ən çox istifadə edilən marketlər** | Swiggy, Electroworld, Localmart, Shopeasy, Zomato, Bigbasket, Amazon, Flipkart, Autozone, Reliance |
| **Həftə içi / sonu xərcləmə** | Həftə içi 4091, həftə sonu 1580 əməliyyat |

📄 `sql/analysis_queries.sql`

---

## 📈 4. Power BI dashboard

**Dashboard səhifələri:**

| Səhifə | Məzmun |
|--------|--------|
| **Giriş** | KPI kartları (Ortalama işlem, unikal müştəri, ümumi həcm, gəlir), tarix filtri, səhifə naviqasiyası |
| **Ümumi Analiz** | Ölkələr üzrə işlem həcmi, ödəniş növü bölgüsü, marketlər, müştəri segmenti |
| **Kateqoriya Analizi** | Kateqoriyalar üzrə pul axını (Waterfall), işlem sayı, gəlir, geri qaytarma |
| **Ölkə Analizi** | Müştəri sayı, saxtakarlıq sayı/zərəri, şəhərlər üzrə gəlir, işlem yoğunluğu |
| **Dolandırıcılıq Analizi** | Kateqoriyalar üzrə saxtakarlıq sayı |

**Əsas KPI‑lar:**

| KPI | Dəyər |
|-----|-------|
| Ortalama İşlem Tutarı | 26 milyard |
| Unikal Müştəri Sayı | 4 244 |
| Ümumi Əməliyyat Həcmi | 14 milyard |
| Ümumi Gəlir | 4.58 milyon |

📊 `powerbi/Nova finance.pbix`

---

## 🧠 5. Əsas tapıntılar və biznes tövsiyələri

| # | Tapıntı | Biznes Tövsiyəsi |
|---|---------|------------------|
| 1 | VIP müştərilər (5.4%) ümumi gəlirin böyük hissəsini yaradır | VIP sadiqlik proqramı, fərdi menecer xidməti, VIP tədbirlər və hədiyyələr |
| 2 | **Electronics** ən çox gəlir gətirən kateqoriyadır | Təhlükəsizlik tədbirlərinin artırılması, məhsul çeşidinin genişləndirilməsi, məqsədli reklam kampaniyaları, endirim strateqiyası |
| 3 | ABŞ-də saxtakarlıq həm say, həm də zərər baxımından liderdir | Risk skorlama sistemi (yüksək riskli əməliyyatların avtomatik bloklanması), ABŞ bazarı üçün xüsusi limitlər, erkən aşkarlama komandaları, yüksək riskli ştatların monitorinqi |
| 4 | **Swiggy, Electroworld, Localmart** ən çox istifadə edilən marketlərdir | Strateji tərəfdaşlıq, müştəri sadiqliyinin artırılması |
| 5 | Həftə sonu xərcləri həftə içi ilə eyni orta məbləğdədir | Həftə sonu kampaniyaları, xüsusi təkliflər, mobil bildirişlər, sosial media kampaniyaları |
| 6 | **Hyderabad** və **Gurugram** ən çox gəlir gətirən şəhərlərdir | Bu şəhərlərdə satış ofislərinin gücləndirilməsi, lokal marketinq kampaniyaları |
| 7 | Son 6 ayda əməliyyat həcmində artım var | Artıma səbəb olan amillərin araşdırılması (mövsüm, kampaniya, yeni istifadəçilər) və uğurlu strategiyaların təkrarlanması |

📄 `presentation/powerbi proje.pdf`

---

## 📊 6. Excel analizi

- Pivot tablolar ilə əlavə analizlər aparılmışdır
- Kateqoriya, ölkə, market və zaman bazlı xülasə cədvəlləri hazırlanmışdır

📊 `excel/Novafinancepivottabel.xlsx`

## 👤 Author
**Fidan Ismayilzada**  
Data Analyst  
🔗 LinkedIn: https://linkedin.com/in/fidan-ismayilzada-529104193
