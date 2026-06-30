# 🚀 Termux IP & Domain Sorgu Botu (Sıfır Bağımlılık)

Termux üzerinde herhangi bir harici eklenti (`pip`, `python`, `node` vb.) yüklemeye gerek kalmadan, tamamen terminalin kendi gücüyle çalışan pratik bir IP ve Alan adı bilgi sorgulama (OSINT) aracıdır. İçi bomboş, yeni kurulmuş bir Termux'ta bile anında çalışır.

> 💡 **Önemli Not:** Bu botu kurduktan sonra bir dahaki sorgu yapacağınız zamanlarda terminale sadece belirlediğimiz kısayol kelimesini (varsayılan olarak `sorgu`) yazıp, yanına hedefi ekleyerek **ENTER** demeniz yeterlidir. Eğer isterseniz aşağıdaki kurulum kodunun en sonundaki `alias sorgu=` kısmını değiştirerek bu kelimeyi tamamen kendinize göre de özelleştirebilirsiniz.

## 🛠️ Yöntem 1: Tek Tıkla Otomatik Kurulum (Önerilen)

Termux terminalinizi açın, aşağıdaki tek satırlık uzun kodun tamamını kopyalayın ve **ENTER** tuşuna basın. Bu komut deponun içindeki tüm kodları arka planda otomatik olarak oluşturur ve kısayolu tanımlar:

```bash
mkdir -p ~/.sorgubot && cat << 'EOF' > ~/.sorgubot/sorgu.sh && chmod +x ~/.sorgubot/sorgu.sh && sed -i '/alias sorgu=/d' ~/.bashrc && echo "alias sorgu='~/.sorgubot/sorgu.sh'" >> ~/.bashrc && source ~/.bashrc 2>/dev/null || true && ~/.sorgubot/sorgu.sh --ilk
#!/bin/bash
YESIL='\033[0;32m'
MAVI='\033[0;36m'
SARI='\033[1;33m'
KIRMIZI='\033[0;31m'
BEYAZ='\033[1;37m'
RENKSIZ='\033[0m'
if [ "$1" == "--ilk" ]; then
    clear
    echo -e "${YESIL}=================================================${RENKSIZ}"
    echo -e "${MAVI}🚀 IP & DOMAIN SORGU BOTU HAZIR!${RENKSIZ}"
    echo -e "${YESIL}=================================================${RENKSIZ}"
    echo -e "${BEYAZ}Kullanmak için:${YESIL} sorgu google.com${RENKSIZ}"
    echo -e "${YESIL}=================================================${RENKSIZ}"
    exit 0
fi
HEDEF=$1
if [ -z "$HEDEF" ]; then
    echo -e "${KIRMIZI}[!] Kullanım: ${YESIL}sorgu <ip_veya_domain>${RENKSIZ}"
    exit 1
fi
echo -e "\n${MAVI}🔍 $HEDEF analiz ediliyor...${RENKSIZ}\n"
VERI=$(curl -s --connect-timeout 5 "[http://ip-api.com/line/$HEDEF?fields=status,country,countryCode,regionName,city,isp,query](http://ip-api.com/line/$HEDEF?fields=status,country,countryCode,regionName,city,isp,query)")
if [ -z "$VERI" ] || echo "$VERI" | grep -q "fail"; then
    echo -e "${KIRMIZI}[❌] Hata! Geçersiz hedef veya internet yok.${RENKSIZ}"
    exit 1
fi
STATUS=$(echo "$VERI" | sed -n '1p')
ULKE=$(echo "$VERI" | sed -n '2p')
KOD=$(echo "$VERI" | sed -n '3p')
BOLGE=$(echo "$VERI" | sed -n '4p')
SEHIR=$(echo "$VERI" | sed -n '5p')
ISP=$(echo "$VERI" | sed -n '6p')
IP=$(echo "$VERI" | sed -n '7p')
echo -e "${YESIL}┌──────────────────────────────────────────────┐${RENKSIZ}"
echo -e "${YESIL}│${MAVI} 🌐 Hedef IP   :${BEYAZ} $IP${RENKSIZ}"
echo -e "${YESIL}│${MAVI} 🌍 Ülke       :${BEYAZ} $ULKE ($KOD)${RENKSIZ}"
echo -e "${YESIL}│${MAVI} 🏙️  Şehir      :${BEYAZ} $SEHIR / $BOLGE${RENKSIZ}"
echo -e "${YESIL}│${MAVI} 🏢 Sağlayıcı  :${BEYAZ} $ISP${RENKSIZ}"
echo -e "${YESIL}└──────────────────────────────────────────────┘${RENKSIZ}"
EOF
chmod +x ~/.sorgubot/sorgu.sh && sed -i '/alias sorgu=/d' ~/.bashrc && echo "alias sorgu='~/.sorgubot/sorgu.sh'" >> ~/.bashrc && source ~/.bashrc 2>/dev/null || true && ~/.sorgubot/sorgu.sh --ilk
