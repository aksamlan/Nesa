# Nesa Miner Program. Validator daha sonra gelecek.
![image](https://github.com/user-attachments/assets/f562e1f3-e6fc-40e1-9166-25b24ea753cf)

# Sistem Gereksinimleri
- CPU: Multi-core processor
- Memory: Minimum 4 GB RAM
- Storage: 50 GB boş disk alanı (testnet sırasında düğümünüzün yeteneklerini test etmek için başka işler göndermemize olanak sağlamak amacıyla daha fazlası önerilir)
- GPU: CUDA etkin GPU'lar önerilir. MPS de desteklenir. CPU madenciliği mevcuttur, ancak tüm modeller için geçerli değildir.

# Gereklilikleri yükleyelim
```console
sudo apt update && sudo apt upgrade -y
sudo apt install jq -y
```
```console
# Docker kuralım
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
docker version

# Docker-compose kuralım
VER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep tag_name | cut -d '"' -f 4)

curl -L "https://github.com/docker/compose/releases/download/"$VER"/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

chmod +x /usr/local/bin/docker-compose
docker-compose --version
```
# [HugginFace](https://huggingface.co/)'de hesap açıyoruz ve Token oluşturup kayıt ediyoruz.
# Hugging Face > Profile > Settings > Access Tokens , oluştururken Write yetkisini veriyoruz.
![image](https://github.com/user-attachments/assets/339bcbba-083b-4a89-b869-2505095197f3)

# Bootstrap Komut Dosyasını İndirelim ve Çalıştıralım - Gerekli PORT'u da açalım
```console
# Portu açalım
sudo ufw allow 31333

# Script çalıştıralım
bash <(curl -s https://raw.githubusercontent.com/nesaorg/bootstrap/master/bootstrap.sh)
```
# Sırasıyla aşağıdaki adımlarla ilerleyelim.
- `Wizardy` > `Kendine isim belirle` > `ENTER` > `ENTER` > `Miner` > `Cüzdan Kelimeleri` > `NON-Distributed Miner` > `ister ENTER de mevcut model ile devam et istersen HugginFace'den model ismi gir` > `Huggingface API key gir` > `YES`
- Model girdiğinizde HugginFace'de ismini bulup lisansı kabul etmeniz gerekiyor.

# Miner'i kontrol edelim aşağıdaki gibi olmalı
```console
docker ps -a
```
![image](https://github.com/user-attachments/assets/4f665208-6bd9-4d9e-8b63-f21526e35953)

# [Explorer'den](https://node.nesa.ai/) Miner aktif olup olmadığını kontrol edelim `Peer ID'miz` sayesinde
```console
cat ~/.nesa/identity/node_id.id
```

# İŞLEMLERİMİZ BU KADAR İYİ ŞANSLAR. AŞAĞIYA DA NESA EKİBİNİN KURULUM GİF'İNİ BIRAKIYORUM.
![gif](https://raw.githubusercontent.com/nesaorg/bootstrap/master/images/bootstrap.gif)
