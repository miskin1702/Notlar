
### MANİPULE KERNEL MODULES
Modüller /lib/modules/generic/kernel/drivers

```
lsmod				#modulleri listele
modprobe modadı 	## Module Ekle
rmmod mod_ad_bagımlılıgı	## önce bağımlılığını kaldır
rmmod modadı				## Sonra modulu kaldır
depmod 				# dependicy görüntüle 

```
### Networking
Bilgi al
```
ip add				## Kendi ip'ni bul, 
ping your.ip 		# Kendine network varlığını kontrol et
ping another_ıp_inlocal		# Rastgele başka yerel ip ye ping at 
ip route 			# default gateway görünür
```

### DNS sorgula DNS server:port ve web address to ip
dns dorgulaması yapılan ilk yer /etc/hosts dosyasıdır. 
```
dig @dns-server-ip host			# Dns adresini verip host adresini ordan sorabiliriz.
dig @127.0.0.1:76 google.com	# Dns server kaldırıp adresi olarak 127.0.0.1:76 olarak 
								# belirledik
```

### OS bilgisi alma

```
cat /etc/os-release

cat /etc/network/interfaces		# Eski yapılarda
cat /etc/netplan/any-name.yaml 
netplan apply 					# Yapılan değişiklikleri uygulama

sudo nmtui						#arayüzsüz linuxlarda gui ile network
```

### Disk ile uğraş

```
lsblk							# bok aygıtlar yani diskleri göster ya da
cat /proc/partitions			# veya
ls /dev | grep sd  				#yukardakilerin tümü benzer iş görür

fdisk /dev/sdb					#sdb diski partition delete
mkfs.ext4 /dev/sdb1				#Bölümlendirilen diske filesystem kurma
```

### Mount ve Boot mount


```
blkid 								# Mount edeceğimiz diskin filesystemini görme
mount -t ext4 /dev/sdc1 /mnt/10GB	# Sdc1 bölümünü ext4 dosya türünde mount ettik
mount								#mountları listele
umount /mnt/10GB					#umount etme

vi /etc/fstab						#On boot mount settings açılır ve aşağıdaki gibi eklenir.

#	Fstab Root Filesystem Pass 1 olmalı, diğerleri 2 veya boş olabilir.

filesystem	mountpoint	Type	options		Dumps	Pass
/dev/sdc1	/mnt/10GB	ext4	defaults	0		2

```


### fsck (File system check)
Öncelikle check edilecek disk, /etc/fstab içinde tanıtılmış olmalı ve
PASS değeri 1 veya 2 olmalı. Sonra Maximum Mount sayısını aşmış olmalı. 
Sonra fsck çalışmaıdır

```
tune2fs -l /dev/sdb1	#Öncelikle  mount count öğrenilir.
tune2fs -c 10 /dev/sdb1	# Sonra Max Mount Count 10 olarak ayarlanır.
						#sonra fsck çalıştırılailir.
```

### Phsyzal and Logical Volume (LVM)
Fiziksel Volumler /dev/sd gibi bir şeyle başlarken 
Logical Volumler /dev/centos gibi yapay bir isimle başlar ve
aynen disk gibi root ve swap gibi partitions barındırır.

```
cat /etc/fstab	#Burda /dev/sdb.. gibi asıl diski öğreniriz. 
pvdisplay		#Phsycal Volume display
lvdispaly		#Logical Volume display 
```
LVM Oluşturma
sdb, sdc, sde adında, partition oluşturulmamış 3 diskimiz olsun.
bunlar ile tek bir lvm oluşturalım. LVM 3 diskten oluşacak ama
tek bir disk gibi davranacak.  

```
pvcreate /dev/sdb /dev/sdc /dev/sde 			# 3 diski dahil edelim 
vgcreate grup_lvm /dev/sdb /dev/sdc /dev/sde 	# 3 diski bir Volume Grup altında topladık.
vgdisplay 										# Grubu görüntüledik
lvcreate -L 20G -n LVM_ADİ grup_lvm 			# L ile Volume boyutu, n ile isim verdik ve 
												# grup_lvm grubuna dahil ettik
mkfs.ext4 /dev/grup_lvm/LVM_ADİ 				# LVM de Filesystemimizi de oluşturduk. 

lvextend -L+5G /dev/grup_lvm/LVM_ADİ			# LVM'yi 5 GB büyüttük.
```







