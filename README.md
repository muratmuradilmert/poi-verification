# POI Verification

A single-page, in-browser tool for batch geocoding, reverse geocoding and location validation of points of interest from an Excel file. Built for Turkish addresses; the interface is available in **Turkish and English**.

[Türkçe açıklama aşağıda ↓](#türkçe)

## Features

- **Address → Coordinates**: finds latitude/longitude from the address (and optionally the business name).
- **Coordinates → Address**: fills in the address, province and district from coordinates.
- **Validate Location**: checks existing coordinates against the address and flags rows farther than a threshold (default 500 m). Mismatches can then be fixed in one click.
- Progressive address cleanup for Turkish addresses (neighbourhood, street, door number, building) with province/district/neighbourhood consistency checks.
- Optional **Places API (New)** business-name search (paid; off by default).
- **Google Maps** or **Yandex Geocoder** as the provider.
- Map view (OpenStreetMap / Esri satellite), filters, search, row selection, Excel export.
- Turkish / English interface and light / dark theme.

## Getting started

No build step and no server needed. Either:

- open `index.html` in a browser, or
- use the hosted version on GitHub Pages (if enabled for this repository).

When opened directly from disk (`file://`), the map defaults to Esri imagery, because OpenStreetMap does not serve tiles to pages without a Referer header. Served over HTTP(S), for example from GitHub Pages, OpenStreetMap works normally.

Then:

1. Pick a provider and enter your API key in **API Settings**.
2. Click **Upload Excel** (or drag and drop the file onto the table). Use **Download Template** for the expected columns.
3. Choose a tab, optionally select rows, and click **Start**.
4. Click **Export to Excel** to save the results.

### Excel columns

| Column (TR / EN) | Notes |
|---|---|
| ID | Optional; the row number is used when empty |
| İsim / Name | Business or point name |
| İl / Province | |
| İlçe / District | |
| Adres / Address | |
| Enlem / Latitude | Decimal; a comma is accepted as the decimal separator |
| Boylam / Longitude | |
| Durum / Status | Filled in by the tool |
| Not / Note | Filled in by the tool |

Headers are matched case- and accent-insensitively and some aliases are accepted (`lat`, `lng`, `city`, `district`, `açık adres`…). Any other columns are kept and written back on export.

## API keys

The tool runs entirely in your browser and calls the provider directly with **your own key**. Usage is billed to your account.

**Google Maps Platform**: enable *Maps JavaScript API* and *Geocoding API*; enable *Places API (New)* only if you turn on business-name search. In the Google Cloud Console, [restrict the key](https://developers.google.com/maps/api-security-best-practices) to the HTTP referrers you use (for example your GitHub Pages address). A browser key is always visible to whoever uses the page, and the referrer restriction is what protects it.

**Yandex**: a [Geocoder API](https://yandex.com/maps-api/products/geocoder-api) key.

## Privacy

- API keys are never part of this repository. They are kept in memory, or in your browser's `localStorage` if **Remember keys in this browser** is checked. Uncheck it to remove them.
- Your Excel data stays in the browser. Only the addresses/coordinates being looked up are sent to the selected provider. When the map is open, map tiles are loaded from OpenStreetMap or Esri.

## Third-party services and libraries

- [SheetJS](https://sheetjs.com/) (Excel), [Leaflet](https://leafletjs.com/) (map), [Lucide](https://lucide.dev/) (icons), loaded from public CDNs.
- Map tiles: © [OpenStreetMap](https://www.openstreetmap.org/copyright) contributors; satellite imagery © Esri and its data providers. Please respect the [OSM tile usage policy](https://operations.osmfoundation.org/policies/tiles/) and Esri's terms for heavy use.

## License

[MIT](LICENSE)

---

## Türkçe

Excel dosyasındaki noktalar için toplu **adres → koordinat**, **koordinat → adres** ve **konum doğrulama** yapan, tamamen tarayıcıda çalışan tek sayfalık bir araç. Türkiye adresleri için geliştirildi. Arayüz Türkçe ve İngilizce kullanılabilir.

### Özellikler

- **Adres → Koordinat**: Adresten (isteğe bağlı olarak işletme adından) enlem ve boylam bulur.
- **Koordinat → Adres**: Koordinattan adres, il ve ilçe bilgisini doldurur.
- **Konum Doğrulama**: Mevcut koordinatı adresle karşılaştırır ve eşiği (varsayılan 500 m) aşan satırları işaretler. Uyumsuz satırlar tek tıkla düzeltilebilir.
- Türkçe adresler için kademeli temizleme (mahalle, cadde/sokak, kapı no, bina) ve il/ilçe/mahalle tutarlılık kontrolü.
- İsteğe bağlı **Places API (New)** ile işletme adı araması (ücretli, varsayılan olarak kapalı).
- Servis sağlayıcı olarak **Google Maps** veya **Yandex Geocoder**.
- Harita görünümü (OpenStreetMap / Esri uydu), filtreler, arama, satır seçimi ve Excel'e aktarma.
- Türkçe/İngilizce arayüz, açık/koyu tema.

### Kullanım

Kurulum gerekmez: `index.html` dosyasını tarayıcıda açın ya da GitHub Pages adresini kullanın. Dosya doğrudan diskten (`file://`) açıldığında OpenStreetMap karo vermediği için harita varsayılan olarak Esri uydu görüntüsüyle açılır. GitHub Pages gibi bir sunucudan açıldığında OpenStreetMap normal çalışır.

1. **API Ayarları** bölümünde servis sağlayıcıyı seçip API anahtarınızı girin.
2. **Excel Yükle** ile dosyanızı açın ya da tabloya sürükleyip bırakın. Sütun yapısı için **Şablon İndir**'i kullanabilirsiniz.
3. Sekmeyi seçin, isterseniz satır seçin ve **Başlat**'a basın.
4. Sonuçları **Excel'e Aktar** ile kaydedin.

### API anahtarı ve gizlilik

- Araç, sağlayıcıya doğrudan **sizin anahtarınızla** istek gönderir ve kullanım ücreti sizin hesabınıza yansır.
- Google için *Maps JavaScript API* ve *Geocoding API*'yi açın. İşletme adı aramasını kullanacaksanız *Places API (New)*'yu da açın. Anahtarı Google Cloud Console'da kullandığınız web adresine (HTTP referrer) kısıtlayın: tarayıcıda çalışan bir anahtar sayfayı kullanan herkese görünür ve onu koruyan bu kısıtlamadır.
- Anahtarlar bu depoda yer almaz. Yalnızca bellekte, **Anahtarları bu tarayıcıda hatırla** seçiliyse de tarayıcınızın `localStorage` alanında tutulur.
- Excel verileriniz tarayıcıda kalır. Seçili sağlayıcıya yalnızca aranan adres veya koordinat gönderilir.

### Lisans

[MIT](LICENSE)
