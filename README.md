\# Cisco Packet Tracer - Inter-VLAN Routing \& DHCP Laboratory



Bu projede, Cisco Packet Tracer kullanılarak iki farklı yerel ağın (LAN) tek bir Router üzerinden haberleşmesini sağlayan ve IP dağıtımını otomatikleştiren bir ağ topolojisi tasarlanmıştır.



\## 🚀 Kullanılan Teknolojiler ve Konseptler

\* \*\*Inter-VLAN Routing (Katman 3 Yönlendirme):\*\* Farklı IP bloklarındaki ağların birbiriyle konuşması sağlandı.

\* \*\*DHCP Sunucusu (Dynamic Host Configuration Protocol):\*\* Cihazlara manuel IP vermek yerine Router üzerinde havuz oluşturularak dinamik IP dağıtımı yapıldı.

\* \*\*Cisco IOS CLI:\*\* Router ve Switch yapılandırmaları komut satırı üzerinden gerçekleştirildi.



\## 🛠️ Ağ Topolojisi Bilgileri



| Bölge / Ağ | IP Bloğu | Ağ Geçidi (Default Gateway) | Cihazlar |

| :--- | :--- | :--- | :--- |

| \*\*Sol Mahalle\*\* | `192.168.1.0/24` | `192.168.1.1` (Gig0/0) | PC-0, Laptop0 |

| \*\*Sağ Mahalle\*\* | `10.0.0.0/8` | `10.0.0.1` (Gig0/1) | PC-1 |



\---



\## 💻 Uygulanan Temel CLI Komutları



\### 1. Router Port Yapılandırmaları

```text

SedRouter(config)# interface gigabitEthernet 0/0

SedRouter(config-if)# ip address 192.168.1.1 255.255.255.0

SedRouter(config-if)# no shutdown



SedRouter(config)# interface gigabitEthernet 0/1

SedRouter(config-if)# ip address 10.0.0.1 255.0.0.0

SedRouter(config-if)# no shutdown 



SedRouter(config)# ip dhcp pool SOL\_MAHALLE

SedRouter(dhcp-config)# network 192.168.1.0 255.255.255.0

SedRouter(dhcp-config)# default-router 192.168.1.1



SedRouter(config)# ip dhcp pool SAG\_MAHALLE

SedRouter(dhcp-config)# network 10.0.0.0 255.0.0.0

SedRouter(dhcp-config)# default-router 10.0.0.1





🔍 Sistemin Test Edilmesi ve Doğrulanması

Sistemin sorunsuz çalıştığından emin olmak için şu iki kritik test yapılmıştır:



Otomatik IP Kontrolü: Ağdaki bilgisayarlar ve laptop DHCP moduna alınmış ve Router'ın her cihaza kendi mahallesine uygun IP adresini (ve Gateway bilgisini) otomatik olarak tıkır tıkır dağıttığı gözlemlenmiştir.



Ağlar Arası İletişim (Ping Testi): Sol mahalledeki bilgisayardan (192.168.1.x), sağ mahalledeki tamamen farklı bir ağda olan bilgisayara (10.0.0.10) ping atılmış ve paketlerin Router üzerinden başarıyla geçerek hedefe ulaştığı (Reply mesajlarıyla) kanıtlanmıştır.

