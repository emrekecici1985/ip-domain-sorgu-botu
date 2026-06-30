# 🚀 Termux IP & Domain Sorgu Botu (Sıfır Bağımlılık)

Termux üzerinde herhangi bir harici kütüphane (`pip`, `python`, `node` vb.) yüklemeye gerek kalmadan, tamamen terminalin kendi gücüyle çalışan pratik bir IP ve Domain bilgi sorgulama (OSINT) aracıdır. İçi bomboş, yeni kurulmuş bir Termux'ta bile anında çalışır.

## 🛠️ Tek Tıkla Kurulum ve Çalıştırma

Termux terminalinizi açın, aşağıdaki kod bloğunun tamamını kopyalayıp yapıştırın ve **ENTER** tuşuna basın:

```bash
mkdir -p ~/.sorgubot && cat << 'EOF' > ~/.sorgubot/sorgu.sh && chmod +x ~/.sorgubot/sorgu.sh && sed -i '/alias sorgu=/d' ~/.bashrc && echo "alias sorgu='~/.sorgubot/sorgu.sh'" >> ~/.bashrc && source ~/.bashrc 2>/dev/null || true && ~/.sorgubot/sorgu.sh --ilk
