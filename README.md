#   GÖREV YÖNETİM UYGULAMASI

import os

gorevler = []

def gorevleri_yukle():
    global gorevler
    try:
        if os.path.exists("gorevler.txt"):
            with open("gorevler.txt", "r", encoding="utf-8") as dosya:
                gorevler = [satir.strip() for satir in dosya.readlines()]
        else:
            gorevler = []
    except Exception as e:
        print("Dosya okunurken hata oluştu:", e)
        gorevler = []

def gorevleri_kaydet():
    try:
        with open("gorevler.txt", "w", encoding="utf-8") as dosya:
            for gorev in gorevler:
                dosya.write(gorev + "\n")
    except Exception as e:
        print("Dosya yazılırken hata oluştu:", e)


def gorevleri_listele():
    if not gorevler:
        print("\nGörev listesi boş.\n")
        return

    print("\n--- GÖREV LİSTESİ ---")
    for i, gorev in enumerate(gorevler, start=1):
        print(f"{i}. {gorev}")
    print()

def gorev_ekle():
    yeni_gorev = input("Eklemek istediğiniz görevi yazın: ").strip()

    if yeni_gorev == "":
        print("Boş görev eklenemez!")
        return

    gorevler.append(yeni_gorev)
    gorevleri_kaydet()
    print("✔ Görev başarıyla eklendi!\n")


def gorev_sil():
    gorevleri_listele()
    if not gorevler:
        return

    try:
        numara = int(input("Silmek istediğiniz görev numarası: "))
        if 1 <= numara <= len(gorevler):
            silinen = gorevler.pop(numara - 1)
            gorevleri_kaydet()
            print(f"✔ '{silinen}' görevi silindi!\n")
        else:
            print("Geçersiz görev numarası!\n")
    except ValueError:
        print("Lütfen sadece sayı girin!\n")

def gorev_duzenle():
    gorevleri_listele()
    if not gorevler:
        return

    try:
        numara = int(input("Düzenlemek istediğiniz görev numarası: "))
        if 1 <= numara <= len(gorevler):
            yeni_metin = input("Yeni görev metnini yazın: ").strip()

            if yeni_metin == "":
                print("Boş görev yazılamaz!")
                return

            gorevler[numara - 1] = yeni_metin
            gorevleri_kaydet()
            print("✔ Görev başarıyla güncellendi!\n")
        else:
            print("Geçersiz görev numarası!\n")
    except ValueError:
        print("Lütfen sadece sayı girin!\n")


def menu():
    print("""
--- GÖREV YÖNETİM UYGULAMASI ---

1) Görevleri Listele
2) Yeni Görev Ekle
3) Görev Düzenle
4) Görev Sil
5) Çıkış
""")


gorevleri_yukle()

while True:
    menu()
    secim = input("Bir seçenek seçin: ")

    if secim == "1":
        gorevleri_listele()
    elif secim == "2":
        gorev_ekle()
    elif secim == "3":
        gorev_duzenle()
    elif secim == "4":
        gorev_sil()
    elif secim == "5":
        print("Programdan çıkılıyor... 👋")
        break
    else:
        print("Geçersiz seçim! Lütfen yeniden deneyin.\n")
