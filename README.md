# asya-7
# ASYA ÜLKELERİ E-KİTAP 

from fpdf import FPDF
import csv

class AsiaEbook:
    def __init__(self):
        self.pdf = FPDF()
        self.pdf.set_auto_page_break(auto=True, margin=15)
        self.pdf.add_font('DejaVu', '', 'DejaVuSansCondensed.ttf', uni=True)
        
    def create_cover(self):
        self.pdf.add_page()
        self.pdf.set_font('DejaVu', '', 24)
        self.pdf.cell(0, 40, "ASYA ÜLKELERİ REHBERİ", 0, 1, 'C')
        self.pdf.image("asia_map.png", x=50, y=60, w=100)
        self.pdf.set_font('DejaVu', '', 16)
        self.pdf.cell(0, 40, "Hazırlayan: Ali Ekber HÖKELEK", 0, 1, 'C')
        self.pdf.cell(0, 10, "Fatoş Büyükkuşoğlu İlkokulu - 4/C", 0, 1, 'C')

    def add_country(self, country_data):
        self.pdf.add_page()
        self.pdf.set_font('DejaVu', '', 18)
        self.pdf.cell(0, 10, country_data['name'], 0, 1, 'C')
        self.pdf.image(f"flags/{country_data['code']}.png", x=80, y=40, w=50)
        self.pdf.set_font('DejaVu', '', 14)
        self.pdf.cell(0, 30, f"Başkent: {country_data['capital']}", 0, 1)
        self.pdf.cell(0, 10, f"Nüfus: {country_data['population']}", 0, 1)
        self.pdf.cell(0, 10, f"Para Birimi: {country_data['currency']}", 0, 1)
        self.pdf.multi_cell(0, 10, f"Ünlü Yemekler: {country_data['food']}")

    def generate(self):
        self.create_cover()
        
        # CSV dosyasından ülke verilerini oku (Örnek veri)
        countries = [
            {'name':'IRAK', 'code':'iq', 'capital':'Bağdat', 
             'population':'43 Milyon', 'currency':'Irak Dinarı',
             'food':'Masgouf'},
            {'name':'JAPONYA', 'code':'jp', 'capital':'Tokyo',
             'population':'125 Milyon', 'currency':'Japon Yeni',
             'food':'Suşi, Ramen'}
        ]
        
        for country in countries:
            self.add_country(country)
            
        self.pdf.output("asia_countries.pdf")
        print("E-kitap oluşturuldu: asia_countries.pdf")

if __name__ == "__main__":
    ebook = AsiaEbook()
    ebook.generate()
