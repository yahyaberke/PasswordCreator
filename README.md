# PasswordCreator
This project allows user to slide each letter of a word as many times as user decides and generates a new word as a password.  
#include <stdio.h>
#include <string.h>
#include <ctype.h>
#include <iostream>

// Tablo boyutu
#define TABLO_BOYUTU 30

// Şifreleme tablosu
const char sifreleme_tablosu[TABLO_BOYUTU] = { 'A', 'B', 'C', 'Ç', 'D', 'E', 'F', 'G', 'Ğ', 'H', 'I', 'İ', 'J', 'K', 'L', 'M', 'N', 'O', 'Ö', 'P', 'Q', 'R', 'S', 'Ş', 'T', 'U', 'Ü', 'V', 'W' };
// Şifre çözme tablosu
const char sifre_cozme_tablosu[TABLO_BOYUTU] = { 'A', 'B', 'C', 'Ç', 'D', 'E', 'F', 'G', 'Ğ', 'H', 'I', 'İ', 'J', 'K', 'L', 'M', 'N', 'O', 'Ö', 'P', 'Q', 'R', 'S', 'Ş', 'T', 'U', 'Ü', 'V', 'W',};

// Karakteri şifreleme fonksiyonu
char sifrele(char karakter, int oteleme_miktari) {
    if (isalpha(karakter)) {
        for (int i = 0; i < TABLO_BOYUTU; ++i) {
            if (toupper(karakter) == sifreleme_tablosu[i]) {
                return sifreleme_tablosu[(i + oteleme_miktari) % TABLO_BOYUTU];
            }
        }
    }
    return karakter; // Eğer karakter tabloda yoksa olduğu gibi döndür kodcuk
}

// Karakteri şifre çözme fonksiyonu
char sifre_coz(char karakter, int oteleme_miktari) {
    if (isalpha(karakter)) {
        for (int i = 0; i < TABLO_BOYUTU; ++i) {
            if (toupper(karakter) == sifre_cozme_tablosu[i]) {
                return sifre_cozme_tablosu[(i - oteleme_miktari + TABLO_BOYUTU) % TABLO_BOYUTU];
            }
        }
    }
    return karakter; // Eğer karakter tabloda yoksa olduğu gibi döndür kodcuk
}

// Metni şifreleme fonksiyonu
void metni_sifrele(char metin[], int oteleme_miktari) {
    for (int i = 0; i < strlen(metin); ++i) {
        metin[i] = sifrele(metin[i], oteleme_miktari);
    }
}

// Metni şifre çözme fonksiyonu
void metni_sifre_coz(char metin[], int oteleme_miktari) {
    for (int i = 0; i < strlen(metin); ++i) {
        metin[i] = sifre_coz(metin[i], oteleme_miktari);
    }
}

int main() {
    setlocale(LC_ALL, "Turkish");
    char metin[1000];
    int oteleme_miktari;

    // Kullanıcıdan metni ve öteleme miktarını isteyin hocam
    printf("Test Değeri 1: Ö İ W N \nGeri öteleme miktarı: 11\n");
    printf("Metni girin: ");
    fgets(metin, sizeof(metin), stdin);
    metin[strcspn(metin, "\n")] = '\0'; // fgets() ile alınan metnin sonuna eklelen '\n' karakterini kaldır

    oteleme_miktari = 11;

    // Metni şifrele ve yazdır
    printf("\nŞifrelenmiş metin: ");
    metni_sifrele(metin, oteleme_miktari);
    printf("%s\n", metin);

    // Şifrelenmiş metni şifre çöz ve yazdır
    printf("\nŞifre çözülmüş metin: ");
    metni_sifre_coz(metin, oteleme_miktari);
    printf("%s\n", metin);

    return 0;
}
