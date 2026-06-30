# 🚀 Termux IP & Domain Sorgu Botu (Sıfır Bağımlılık)

Termux üzerinde herhangi bir harici eklenti (`pip`, `python`, `node` vb.) yüklemeye gerek kalmadan, tamamen terminalin kendi gücüyle çalışan pratik bir IP ve Alan adı bilgi sorgulama (OSINT) aracıdır. İçi bomboş, yeni kurulmuş bir Termux'ta bile anında çalışır.

> 💡 **Önemli Not:** Bu botu kurduktan sonra bir dahaki sorgu yapacağınız zamanlarda terminale sadece belirlediğimiz kısayol kelimesini (varsayılan olarak `sorgu`) yazıp, yanına hedefi ekleyerek **ENTER** demeniz yeterlidir. Eğer isterseniz aşağıdaki kurulum kodunun en sonundaki `alias sorgu=` kısmını değiştirerek bu kelimeyi tamamen kendinize göre de özelleştirebilirsiniz.

## 🛠️ Tek Tıkla Kurulum ve Çalıştırma

Termux terminalinizi açın, aşağıdaki tek satırlık uzun kodun tamamını kopyalayın ve **ENTER** tuşuna basın *(Kod dikey ekranlarda kısa görünebilir, yana doğru kaydırarak tamamını kopyaladığınızdan emin olun)*:

```bash
mkdir -p ~/.sorgubot && cat << 'EOF' > ~/.sorgubot/sorgu.sh && chmod +x ~/.sorgubot/sorgu.sh && sed -i '/alias sorgu=/d' ~/.bashrc && echo "alias sorgu='~/.sorgubot/sorgu.sh'" >> ~/.bashrc && source ~/.bashrc 2>/dev/null || true && ~/.sorgubot/sorgu.sh --ilk
