---
title: Önsöz
type: book-tr-tr
order: 0
---

# Önsöz

[TOC]

## Giriş

C++ kullanıcı grubu epey büyüktür. C++98'in ortaya çıkışından C++11'in resmi olarak tamamlanmasına kadar, on yıldan uzun bir süredir üstüne eklenmiştir. C++14/17, C++11 için önemli bir tamamlayıcı ve optimizasyondur ve C++20 bu dili modernizasyonun kapısına getirmiştir. Tüm bu yeni standartların genişletilmiş özellikleri C++ diline verilmiştir. Yeni canlılık ile aşılanmıştır.
Hala **geleneksel C++** (bu kitap, C++98 ve önceki C++ standartlarını geleneksel C++ olarak ifade eder) kullanan C++ programcıları, modern C++ ile yazılmış kodları okurken aslında aynı dili bile kullanmıyor olmalarına şaşırabilirler.

**Modern C++** (bu kitap C++11/14/17/20'ye atıfta bulunur) geleneksel C++'a birçok özellik ekler ve bu da tüm C++'ı modernize edilmiş bir dil haline getirir. Modern C++, yalnızca C++ dilinin kullanılabilirliğini geliştirmekle kalmaz, aynı zamanda `auto` anahtar kelime semantiğinin değiştirilmesi, son derece karmaşık şablon türlerini manipüle etme konusunda bize daha çok güven verir. Aynı zamanda, dilin çalışma zamanında da birçok geliştirme yapılmıştır. Lambda ifadelerinin ortaya çıkması, C++'ın neredeyse (Python, Swift gibi) tüm modern programlama dillerinde bulunan "anonim fonksiyonların" "closure" özelliğine sahip olmasını sağlamıştır. Lambda ifadelerinin ortaya çıkması, C++'ın neredeyse modern programlama dillerinde (Python, Swift vb.) Bu artık sıradan hale geldi ve rvalue referanslarının ortaya çıkması, C++'ın uzun süredir eleştirilen geçici nesne verimliliği sorununu çözdü.

C++17, son üç yıldır C++ topluluğu tarafından teşvik edilen yönelimdir ve aynı zamanda **modern C++** programlamasının önemli bir gelişim yönüne de işaret etmektedir. C++11 kadar görünür olmasa da çok sayıda küçük ve güzel dil özelliği ve yenilik (structured binding gibi) içeriyor ve bu özelliklerin ortaya çıkması C++'taki programlama paradigmamızı bir kez daha düzeltiyor.

Modern C++ aynı zamanda standart kütüphaneye, eşzamanlı programlamayı destekleyen ve artık farklı platformlardaki altta yatan sisteme bağlı olmayan, dil düzeyinde `std::thread` gibi birçok araç ve yöntem ekler. API, dil düzeyinde, platformlar arası destek gerçekler; `std::regex` tam düzenli ifade desteği ve daha çoğunu sağlar. C++98'in çok başarılı bir "paradigma" olduğu kanıtlanmıştır ve modern C++'ın ortaya çıkışı bu paradigmayı daha da geliştirerek C++'ı sistem programlama ve kütüphane geliştirme için daha iyi bir dil haline getirir. Concept'ler, şablon parametrelerinin derlenme zamanını doğrulayarak dilin kullanılabilirliğini daha da artırır.

Sonuç olarak, bir C++ savunucusu ve uygulayıcısı olarak, yeni şeyleri kabul etmede her zaman açık fikirliyiz ve C++'ın gelişimini daha hızlı destekleyerek bu eski ve yeni dili daha canlı hale getirebiliriz.

## Hedefler

- Bu kitap, okuyucuların halihazırda geleneksel C++'a (yani C++98 ve öncesine) aşina olduklarını veya en azından geleneksel C++ kodunu okumakta zorluk çekmediklerini varsayar. Başka bir deyişle, geleneksel C++'ta uzun deneyime sahip olanlar ve modern C++'ın özelliklerini kısa sürede hızlı bir şekilde anlamak isteyenler kitabı okumak için çok uygundur.

- Bu kitap, bir dereceye kadar modern C++'ın kara büyüsünü tanıtıyor. Ancak bu sihir numaraları çok sınırlıdır, ileri düzey C++ öğrenmek isteyen okuyucular için uygun değildir. Bu kitabın amacı, modern C++ için hızlı bir başlangıç sunmaktır. Elbette, ileri düzey okuyucular da bu kitabı modern C++'ı incelemek ve kendilerini C++ konusunda test etmek için kullanabilirler.

## Amaç

Bu kitap C++'ı "Şıp Diye" öğreteceğini iddia ediyor. Amacı, modern C++ ile ilgili (2020'ler öncesi) özelliklere kapsamlı bir giriş sağlamaktır. Okuyucular, aşağıdaki içindekiler tablosundan öğrenmek veya hızlıca aşinalık kazanmak istedikleri yeni özellikler hakkında ilginç içerikler seçebilirler. Okuyucular, bu özelliklerin hepsinin birden gerekli olmadığını bilmelidir. Bunun yerine, bunlar gerçekten ihtiyaç duyulduğu zaman öğrenilmelidir.

Aynı zamanda, kitap sadece kodlama öğretmek yerine, teknik gereksinimlerinin tarihsel arka planını da (mümkün olabildiğince basit bir şekilde) tanıtıyor, bu da bu özelliklerin neden ortaya çıktığını anlamada büyük yardım sağlıyor.

Ayrıca yazar, okuyucuları yeni projelerinde doğrudan modern C++ kullanmaya ve kitabı okuduktan sonra eski projelerini kademeli olarak modern C++'a geçirmeye teşvik etmek istiyor.

## Kod

Bu kitabın her bölümü çok sayıda kod içeriyor. Kitapta tanıtılan özelliklerle ilgili kendi kodunuzu yazarken sorun yaşıyorsanız kitabın ekindeki kaynak kodları okumanız işinize yarayabilir. Kitaptaki kodları [burada](../../code) bulabilirsiniz. Tüm kodlar bölümlere göre düzenlenmiştir, klasör adı bölüm numarasıdır.

## Alıştırmalar

Kitabın her bölümünün sonunda birkaç alıştırma var. Bunlar, mevcut bölümdeki bilgiye hakim olup olmadığınızı test etmek içindir. Soruların olası yanıtlarını [burada](../../exercise) bulabilirsiniz. Yine, klasör adı bölüm numarasıdır.

[İçindekiler](./toc.md) | [Sonraki Bölüm: Modern C++'a Doğru](./01-intro.md)

## Lisanslar

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />Bu çalışma [Ou Changkun](https://changkun.de) tarafından yazılmıştır ve <a rel="license" href="https://creativecommons.org/licenses/by-nc-nd/4.0/deed.tr">Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License</a> ile lisanslanmıştır. Bu depodaki kaynak kodlar, [MIT lisansı](../../LICENSE) altında açık kaynaklıdır.
