# asya-7
# ASYA ÜLKELERİ E-KİTAP OLUŞTURUCU
# Kodu kopyala -> https://replit.com/ sitesine yapıştır -> Çalıştır butonuna bas

from fpdf import FPDF
import requests

# PDF AYARLARI
pdf = FPDF(orientation='P', unit='mm', format='A4')
pdf.set_auto_page_break(auto=True, margin=15)
pdf.add_font('DejaVu', '', 'DejaVuSansCondensed.ttf', uni=True)
pdf.set_font('DejaVu', '', 14)

# KAPAK SAYFASI
pdf.add_page()
pdf.image("https://i.ibb.co/0nXqL9J/asia-map.jpg", x=10, y=20, w=180)  # Asya haritası
pdf.set_y(100)
pdf.cell(0, 10, "ASYA ÜLKELERİ REHBERİ", 0, 1, 'C')
pdf.cell(0, 10, "Hazırlayan: Ali Ekber HÖKELEK", 0, 1, 'C')
pdf.cell(0, 10, "Fatoş Büyükkuşoğlu İlkokulu - 4/C", 0, 1, 'C')

# ÜLKE BİLGİLERİ (Örnek 3 ülke)
ülkeler = [
    {
        "ad": "IRAK",
        "başkent": "Bağdat",
        "nüfus": "43 Milyon",
        "yemek": "Masgouf",
        "resim": "https://i.ibb.co/0JbY9Wz/irak.jpg"
    },
    {
        "ad": "JAPONYA",
        "başkent": "Tokyo",
        "nüfus": "125 Milyon",
        "yemek": "Suşi",
        "resim": "https://i.ibb.co/0JbY9Wz/japonya.jpg"
    }
]

# HER ÜLKE İÇİN SAYFA OLUŞTUR
for ülke in ülkeler:
    pdf.add_page()
    pdf.cell(0, 10, ülke["ad"], 0, 1, 'C')
    pdf.image(ülke["resim"], x=50, y=40, w=100)
    pdf.set_y(120)
    pdf.cell(0, 10, f"Başkent: {ülke['başkent']}", 0, 1)
    pdf.cell(0, 10, f"Nüfus: {ülke['nüfus']}", 0, 1)
    pdf.cell(0, 10, f"Ünlü Yemek: {ülke['yemek']}", 0, 1)

# DOSYAYI KAYDET
pdf.output("Asya_Ulkeleri_Rehberi.pdf")
print("PDF OLUŞTURULDU! Sağ üstteki 'Download' butonuna basarak indirin.")
