# Türkçe Refactoring Kılavuzu

## Refactoring Nedir?

Refactoring, kodun işlevselliğini değiştirmeden, kodun kalitesini artırma, temiz bir hale ve kolay bir tasarıma dönüştürme sürecidir. Refactoring kavramını anlamak için öncelikle temiz ve basit kod nedir, temiz kodu engelleyen, kötü kod yazmaya iten sebepler nelerdir bir diğer deyişle teknik borç nedir teknik borca iten sebepler nelerdir, onu anlamaya çalışalım.

### Temiz Kod Nedir?

#### Temiz kod diğer geliştiriciler için gayet açık ve anlaşılabilirdir. 

Değişken isimlendirmeleri, sınıfların ve metodların uzunlukları ve karmaşıklıkları vs. gibi kodun okunmasını, anlaşılmasını ve bakımını zorlaştıran şeylerin olmaması.

#### Temiz kod, kod tekrarları içermez.

Kod tekrarı, her defasında, aynı değişiklikleri farklı yerlerde yapmaya sebep olur. Her defasında, bir değişiklik yapıldığında, başka nerelerin değişeceğini akılda tutmak gerekir. Kodun anlaşılmasındaki yükü artırır ve süreçleri uzatır.

#### Temiz kodda gereğinden fazla satır/sınıf/metod olmaz.

Az kod, daha az akılda tutulması gereken şey, daha az bakım yapılması, daha az hata demektir. Olabildiğince kısa ve basit kod her zaman temiz koddur.

#### Temiz kodun bakım maliyeti düşüktür.

Temiz kod bakımı kolaylaştırır, hız kazandırır ve bakım maliyetini düşürür.

### Teknik Borç Nedir?

Hiç kimse, projeye zarar vermek için bilerek kötü kod yazmaz. Herkes elinden gelenin en iyisini yapmak ister. Kötü kod yazmaya iten sebepler vardır. Kötü yazılan kod da, ilerde başımıza dert açabilir.

Teknik borcu anlatmak için, bankadan çekilen kredi örnek verilir. Acil ödemeniz gereken bir borç için, günü kurtarmak adına çekilen kredi, daha sonra daha fazla borç olarak tekrar karşımıza çıkar. Çekilen tutar tekrar faizi ile geri ödenir. 

Aynı şekilde, daha hızlı geliştirmek adına; mesela test yazmadan, geliştirilen her özellik, gün geçtikçe bakım maliyetini artırarak, geliştirme hızını da düşürür, ta ki teknik borcu ödeyene kadar.

Peki teknik borca, kötü kod yazmaya iten sebepler nelerdir?

#### Ticari kaygılar

Bazen iş koşulları, tamamlanmadan önce özellikleri kullanıma sunmaya zorlayabilir. Bu durumda, projenin bitmemiş bölümlerini gizlemek için kodda fazladan (aslında kodun parçası olmayan) satırlar olabilir.

#### Teknik borcun sonuçlarının anlaşılmaması

İşverenler/yöneticiler, geride teknik borç biriktirdikçe, maliyetin katlanarak arttığını anlamayabilirler. Bundan dolayıda, ekibin refactoring için zaman ayırmasını, vakit kaybı olarak görürler ve değer vermezler.


#### Ekip üyeleri arasındaki iletişim eksikliği 

İletişim eksikliğinden dolayı bilgi, ekip üyeleri arasında sağlıklı dağılmaz veya tecrübeli birisi bilgiyi tecrübesiz olana yanlış aktarabilir. Bundan dolayıda ekip elindeki güncel olmayan, eksik veya yanlış anlaşılmış bilgi ile geliştirme yapabilir. 

#### Uzun süre farklı dallarda(branch) çalışılması

Teknik borcun birikmesine ve birleştirme işleminde daha da artmasına sebep olur. Toplam teknik borç, ayrı ayrı biriken teknik borç toplamından daha büyük olur.

#### Gecikmeli refactoring 

Refactoring gerekli durumlarda, refactoring ertelenirse, düzenlenmesi gereken bu parçaya bağımlı yeni yazılan her kod, eski düzene göre yazılacağından, teknik borç her yeni yazılan kod için de artar. Oysa anında müdahale edilse, arkasından gelen kodlar için de aynı düzenleme gerekmeyecek.

#### Beceriksizlik & tecrübesizlik

Bazen sadece tecrübesizlikten veya beceriksizlikten kötü kod yazarak, teknik borç biriktiririz.

### Refactoring Ne Zaman Yapılmalı?

#### Üç kural

1. İlk defa bir şey yapıyorsan, sadece yap.
2. İkinci defa aynı şeyi yapıyorsan, tekrara düşmekten çekin ama yinede bir şekilde yap.
3. Üçüncü defa aynı şeyi yapıyorsan, refactor et.

#### Özellik ekleme

Refactoring, başkalarının kodlarını anlamayı kolaylaştırır. Yeni özellik eklemek için kodun iyi anlaşılması gereklidir. Kod ne kadar temiz olursa o kadar anlaşılır olur. Dolayısıyle yeni özellik eklemeden önce kodlar refactor edilebilir.

#### Hata düzeltme

Yine hata bulmak için öncelikle kodun iyi anlaşılması lazımdır. Daha iyi anlamak için kodu refactor ederiz. Refactor işlemi sırasında, çoğunlukla hata bulunur. 

#### Kod inceleme (code review)

Kod inceleme, hem kodu yazan hem de inceleyen için en faydalı iştir. Kod incleme yaparken, hata bulmak daha kolay ve hızlı olur. İlerde yapılabilecek daha büyük hatalar için de, önceden bilgi sahibi olmayı sağlar.

### Refactoring Nasıl Yapılır?

Refactoring kodun normal çalışmasında hiçbir değişiklik yapmadan, kodun daha iyi bir hale gelmesi için yapılan değişiklikler şeklinde olmalıdır.

#### Kod daha temiz hale gelmeli

Refactoring işleminden sonra kodlar hala temiz ve anlaşılır değilse, harcadığımız zaman boşa gitmiş demektir. Bu durumda neden böyle olduğunu anlamaya çalışmak lazım. Refactoring yaparken genelde; küçük değişiklikler yaparken, birden tek seferde çok büyük bir değişiklikler silsilesi içine girince ve üstüne bir de zaman kısıtı varsa işlerin karışmasına sebep olabilir. Bundan dolayı da refactoring sonucunda ortaya çıkan kod pek de temiz bir kod olmaz.

Ancak bazı kod altyapısı o kadar kötüdür ki, ne yaparsanız yapın iyileştirilemeyebilir. İşte bu durumda, kodun yeniden yazılması düşünülebilir. Tabi bunu yapacaksak, kesinlikle ilgili yerlerin testlerinin yazılmış olması şart. Ayrıca biraz zaman ayırmak da gerekli.

#### Refactoring sırasında yeni bir özellik/fonksiyonelite eklenmemeli

Yeni özellik eklemek için yazılan kodlar ile refactoring için yazılan kodlar farklı commit'lerde olmalıdır. Refactoring kodun işlevini değiştirmez, sadece daha iyi hale getirir.

#### Tüm testler refactoring işleminden sonra başarılı olmalı

Testleri olmayan kodları refactor etmek, refactoring sürecindeki en tehlikeli kısımdır. Refactoring yaptıktan sonra 2 durumda testler başarısız olabilir.

- **Refactoring sırasında hata yaptın ve çokta önemli değil:** Devam et ve hatayı düzelt.
- **Testler çok alt seviye kodları test ediyordur. Örneğin, bir sınıfın private metodunu test ediyordur:** Bu durumda, sıkıntı testlerdedir. Dolayısıyla testleri de refactor edebiliriz veya yüksek seviye kodları test eden yeni testler yazabiliriz. Tabi bunun en ideal çözümü, [BDD-style](https://en.wikipedia.org/wiki/Behavior-driven_development) test yazmakdır.

## Koddan Kötü Kokular Geliyor



---

**NOT**: Yararlanılan kaynaklar sürekli eklenecek. 

- https://refactoring.guru/
- http://www.yilmazcihan.com/yazilim-gelistirmede-teknik-borc/
- https://medium.com/bili%C5%9Fim-hareketi/refactoring-prensipleri-ne-zaman-refactoring-yapmal%C4%B1y%C4%B1z-bfb0794fecde
