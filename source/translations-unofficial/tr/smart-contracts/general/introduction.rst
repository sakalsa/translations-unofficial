.. Should answer:
    - What is a smart contract
    - Why use a smart contract
    - What are the use cases
    - What are not the use cases

.. _introduction:

===============================
Akıllı Sözleşmelere Giriş
===============================

Akıllı Sözleşme, Concordium blok zincirine gönderilen ve doğrudan çekirdek
protokolün parçası olmayan davranışı tanımlamak için kullanılan, kullanıcı
tarafından sağlanan bir kod parçasıdır. Bu Akıllı Sözleşmeler, Concordium
Network' teki Node Sunucular tarafından önceden tanımlanmış kurallara göre
işletilir. Bu işlemler tamamen şeffaftır ve tüm Node Sunucular, işlem
sonucunun yalnızca herkese açık bilgilere dayandığı konusunda hemfikir
olmalıdır.

Bir Akıllı Sözleşme GTU (Concordium Madeni Para)'yu alabilir, saklayabilir ve
gönderebilir, zincirin bazı yönlerini gözlemleyebilir ve kendi durumunu
koruyabilir. Akıllı Sözleşmeler her zaman harici eylemlere bir yanıt olarak
yürütülür. Örnek olarak mesaj gönderen bir hesap verilebilir. Pratikte Akıllı
Sözleşmeler, zincir içi ve zincir dışı işlevselliği birleştiren ve genellikle
daha büyük bir sistemin küçük bir parçası olacaktır. Zincir dışı işlevselliğe
bir örnek olarak ise hisse senedi fiyatları veya hava durumu bilgileri gibi
gerçek dünyadaki verilere dayalı olarak akıllı sözleşmeyi başlatan bir Node
Sunucu olabilir.

Akıllı Sözleşmeler Ne İçindir?
=============================

Akıllı sözleşmeler üçüncü şahıslara duyulması gereken güven miktarını
azaltabilir. Bazı durumlarda güvenilir bir üçüncü şahsa duyulan ihtiyacı
ortadan kaldırabilir, bunun dışındaki durumlarda ise yeteneklerini azaltabilir
ve böylece onlara duyulan güven miktarını azaltabilir.

Akıllı Sözleşmeler, bir Node Sunucuya erişimi olan herkesin doğrulayabileceği,
tamamen şeffaf bir şekilde yürütüldüğünden, taraflar arasında güveni sağlamak
için çok yararlı olabilirler.

.. _auction:

Açık Arttırma için Akıllı Sözleşme Örneği
-----------------------------------------

Akıllı sözleşmeler için bir kullanım örneği olarak akla gelebilecek örnek
bir açık artırma düzenlemek olabilir. Bu örnekte Akıllı Sözleşmeyi herkesten
farklı teklifleri kabul edebilecek ve en yüksek teklifi vereni takip edecek
şekilde yazıyoruz. Açık Artırma sona erdiğinde Akıllı Sözleşme, kazanan teklif
GTU (Concordium Madeni Para)'sunu satıcıya gönderir ve diğer tüm teklifleri
geri gönderir. Satıcı da ödemeyi aldıktan sonra ürünü kazanana göndermelidir.

Akıllı Sözleşme müzayede firmasının rolünü alır. Sözleşmenin kendisi
yalnızca teklif bölümünü ve GTU (Concordium Madeni Parası)'ların blok zincir
üzerindeki dağıtımını yönetir. Satıcı yükümlülüklerini yerine getirmez ise
muhtemelen en yüksek teklifi verene geri ödeme yapmak için biraz mantığa
ihtiyaç duyacaktır. Bu sözleşmenin satıcının gerçekten yükümlülüğünü yerine
getirdiğine veya en yüksek teklif verenin bir şikayette bulunabilmesi için
bir şekilde bir kanıtın desteklemesi gerektiği anlamına gelir. Akıllı
Sözleşmeler hayatımızdaki sorunları otomatik olarak çözemez ve en iyi
çözüm Açık Artırmanın özelliklerine bağlı olacaktır.

Akıllı Sözleşmeler Ne İçin *Değildir?*
===================================

Akıllı sözleşmeler çok heyecan verici bir teknolojidir ve insanlar bunlardan
yararlanmanın yeni yollarını bulmaya devam etmektedir. Bununla birlikte, akıllı
sözleşmelerin iyi bir çözüm olmadığı bazı durumlar vardır.

Akıllı sözleşmelerin en önemli avantajlarından biri kodun çalıştırılmasına
duyulan güvendir ve bunu başarmak için blok zinciri ağındaki çok sayıda Node
Sunucunun aynı kodu çalıştırması ve sonucun kabul edilmesini sağlaması gerekir.
Doğal olarak bu aynı kodu bazı bulut hizmetlerinde tek bir düğümde çalıştırmaya
kıyasla pahalıya maal olacaktır.

Akıllı sözleşmenin ağır hesaplamalara dayandığı durumlarda ise hesaplamayı
akıllı sözleşmenin dışına çıkarmak ve akıllı sözleşmenin diğer bölümlerin
doğru şekilde çalıştırılmasını sağlamak için kriptolama ile ilgili teknikler
kullanarak hesaplamanın yalnızca bazı önemli bölümlerini yürütmesini sağlamak
daha yararlı olabilir.

Sonuç olarak Akıllı Sözleşmelerin hiçbir gizliliği olmadğınıdan hassas veriler
bir akıllı sözleşmede ele almak zordur. Concordium ağdaki herkesin Akıllı
Sözleşmeye erişimi vardır. Bazı durumlarda doğrudan verilerle çalışmamak için
kripto araçların kullanılması mümkün olabilir. Bunun yerine Akıllı Sözleşmelerin
gerçek verileri gizleyen şifreleme ve taahhütler gibi türetilmiş kavramlarla
çalışmasını sağlamak mümkün olabilir.

Bir Akıllı Sözleşmenin Yaşam Döngüsü
====================================

Akıllı bir sözleşme ilk olarak zincire bir :ref:`Sözleşme
Modülü <contract-module>`parçası olarak dağıtılır. Bundan sonra bir
:ref:`akıllı sözleşme örneği <contract-instances>` almak için bir Akıllı
Sözleşme çalıştırılır. Son olarak Akıllı Sözleşme Örneği kendi yazılım mantığına
göre tekrar tekrar güncellenebilir.
