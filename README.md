### Kişisel Git(VCS) Kullanım Notları


##### Linux Git Kurulumu
```bash
sudo apt install git
```

##### Git Yapılandırması 
Git kurulduktan sonra ilk yapılması gereken, değişiklikleri 
kimin yapacağını git sistemine bildirmektir. 
```
git config --global user.email "youremail@mail.com"
git config --global user.name "Name Surname"
```

##### Proje Başlatmak
** Yerelden - Repoya **
Proje klasörü yerelde yaratılır, sonra uzak repoya gönderilir.
```
git init
```
** Repodan - Yerele **
Uzak repodan yerele tüm proje kopyalanır. Üzerinde direk değişikliğe
başlanılabilir.
```
git clone https://github.com/user/repoadı
```
##### Stage(index) alanına değişiklik bildirmek
VCS sisteminde, değişiklik kaydı öncelikle Stage alanına bildirilir.
Stage 'Geçici Biriktirme Alanı' veya 'Paketleme Öncesi Toplama alanı' 
olarak anlayabiliriz. Şöyle ki; bir koli(Commit) hazırlayıp 
kargolayacaz(Yerel depodan, Uzak Depoya).Koliyi paketlemeden önce 
kolinin içerisine koyacağımız eşyaları belli alanda(Stage area)
toplayıp,sonra bu alandaki ürünleri koliye koyup paketleriz(Commit). 
Sonra Uzaktaki konuma yollarız(git push). 

```
git add .
```

##### Commit'lemek
Commit, 'havale edilecek koli' anlamında kullanılabilir. Havale edilecek yer
'Uzak Repodur'. Havale edilen yer ise 'Yerel Depodur'. Havale edici ise Git
programıdır. 

```
git commit -m "Değişklik Etiketi"
```
##### Geçmişe Bak
Bir dosyada veya tüm dosyalarda değişiklikleri görmek için `git diff [dosya-adı]`
Dizin ile Stage arasındaki farka bakmak için `git status`
Commit geçmişine bakmak için `git log`


##### Değişiklikleri Geri Alma
Dizinde silinen veya değiştirilen ama Stage'e eklenmeyen 
değişiklikleri geri almak için.(İlgili dosya deneme.py olsun.)
```
# To undo your local changes in a certain file...
git restore my-file.txt

# To unstage a file, but leave its actual changes untouched...
git restore --staged my-file.txt

# To undo all of the local changes in your working copy (be careful!)...
git restore .
```


##### Branch işlemleri
Öncelikle uzak repo yerele `git clone repo_url` ile kopyalanır. 
`cd repo` ile klasör içerisine girilir. Switch ie branc deiştirlir,
yoksa oluşturulur. Push ile branc uzak repoya gönderilir. 
```
git switch -c new_branch
git push --set-upstream origin new_branch
```


##### Bazı Komutlar

Bazı
```
git config -l	# Configleri görüntüle
git reflog		# Geçmiş aktiviteleri göster
git remote -v	# Uzak sunucu ayarları
git branch -vva	# Tüm Branchlar ve detaylarını göster

```
