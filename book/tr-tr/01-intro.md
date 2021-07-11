---
title: "Bölüm 01: Modern C++'a Doğru"
type: book-tr-tr
order: 1
---

# Bölüm 01: Modern C++'a Doğru

[TOC]

**Derleme Ortamı**: Bu kitapta derleyici olarak sadece `clang++` kullanacaktır ve kodlar derlenirken her zaman `-std=c++2a` derleme bayrağı eklenecektir.

```bash
> clang++ -v
Apple LLVM version 10.0.1 (clang-1001.0.46.4)
Target: x86_64-apple-darwin18.6.0
Thread model: posix
InstalledDir: /Library/Developer/CommandLineTools/usr/bin
```

## 1.1 Kullanımdan Kaldırılan Özellikler

Modern C++'ı öğrenmeden önce, C++11'den beri kullanımdan kaldırılan ana özelliklere bir göz atalım:

> **Not**: Kullanımdan kaldırma tamamen kullanılamaz hale getirme demek değildir, yalnızca özelliklerin gelecekteki standartlardan kaldırılacağı ve bu özellikleri kullanmaktan kaçınılması gerektiği anlamına gelir. Ancak, kullanımdan kaldırılan özellikler hala standart kitaplığın bir parçasıdır ve özelliklerin çoğu aslında uyumluluk nedenleriyle "kalıcı olarak" tutulmuştur.

- **String literal sabitinin artık bir `char *`'a atanmasına izin verilmiyor. Bir `char *` karakterini bir string literal sabitiyle atamanız ve başlatmanız gerekiyorsa `const char *` veya `auto` kullanmalısınız.**

  ```cpp
  char *str = "hello world!"; // Bir kullanımdan kaldırma uyarısı görünecek
  ```

- **C++98 istisna açıklaması,, `unexpected_handler`, `set_unexpected()` ve diğer ilgili özellikler kullanımdan kaldırılmıştır ve `noexcept` kullanılmalıdır.**

- **`auto_ptr` kullanımdan kaldırılmıştır ve `unique_ptr` kullanılmalıdır.**

- **`register` anahtar kelimesi kullanımdan kaldırılmıştır, kullanılabilir ancak artık pratik bir anlamı yoktur.**

- **`bool` türünün `++` işlemi kullanımdan kaldırılmıştır.**

- **Bir sınıfın bir yıkıcısı varsa, kopya oluşturucular ve kopya atama işleçleri oluşturan özellikler kullanımdan kaldırılmıştır.**

- **C dili stili tür dönüştürmesi (yani değişkenlerden önce `(convert_type)` kullanılması) kullanımdan kaldırılmıştır ve tür dönüştürme için `static_cast`, `reinterpret_cast`, `const_cast` kullanılmalıdır.**

- **Özellikle, `<ccomplex>`, `<cstdalign>`, `<cstdbool>` ve `<ctgmath>` gibi kullanılabilecek bazı C standart kütüphaneleri, en son C++17 standardında kullanımdan kaldırılmıştır.**

- ... ve daha çoğu

Ayrıca parameter binding (C++11, `std::bind` ve `std::function` sunar), `export` gibi bazı diğer özellikler de kullanımdan kaldırılmıştır. Yukarıda bahsedilen bu özellikleri **daha önce hiç kullanmadıysanız veya duymadıysanız lütfen anlamaya çalışmayın. Doğrudan yeni standarda yaklaşmalı ve yeni özellikleri öğrenmelisiniz**. Sonuçta teknoloji ilerliyor.

## 1.2 C ile Uyumluluklar

Örneğin Linux sistem çağrıları gibi bazı mücbir sebepler ve tarihsel nedenlerle, C++'ta bazı C kodlarını (hatta eski C kodlarını) kullanmak zorunda kaldık. Modern C++'ın ortaya çıkmasından önce, çoğu insan "C ve C++ arasındaki fark nedir" hakkında konuşuyordu. Genel olarak konuşursak, nesne yönelimli sınıf özelliklerine ve jenerik programlamanın şablon özelliklerine ek olarak, başka bir görüş veya hatta doğrudan bir cevap yoktur. Şekil 1.2'deki Venn şeması, C ve C++ ile ilgili uyumluluğu kabaca yanıtlar.

![Şekil 1.2: ISO C ve ISO C++ arasındaki uyumluluklar](../../assets/figures/comparison.png)

Şu andan itibaren, zihninizde "C++, C'nin **bir üst kümesi değildir**" fikrine sahip olmalısınız ([Ek okumalar için verilen kaynaklarda](#further-readings) C++98 ve C99 arasındaki fark verilir). C++ yazarken, mümkün olduğunca `void*` gibi programlama stillerini kullanmaktan da kaçınmalısınız. C kullanmanız gerektiğinde, `extern "C"` kullanımına dikkat etmeli, C kodunu C++ kodundan ayırmalı ve ardından bağlantıyı birleştirmelisiniz, örneğin:

```cpp
// foo.h
#ifdef __cplusplus
extern "C" {
#endif

int add(int x, int y);

#ifdef __cplusplus
}
#endif

// foo.c
int add(int x, int y) {
    return x+y;
}

// 1.1.cpp
#include "foo.h"
#include <iostream>
#include <functional>

int main() {
    [out = std::ref(std::cout << "C kodundan sonuç: " << add(1, 2))](){
        out.get() << ".\n";
    }();
    return 0;
}
```

Önce C kodunu `gcc` ile derlemelisiniz:

```bash
gcc -c foo.c
```

`foo.o` dosyasını derleyin ve çıktısını alın, sonra C++ kodunu `clang++` kullanarak `.o` dosyasına bağlayın (veya her ikisini de `.o` dosyasına derleyin ve ardından bunları birbirine bağlayın):

```bash
clang++ 1.1.cpp foo.o -std=c++2a -o 1.1
```

Tabii ki, yukarıdaki kodu derlemek için `Makefile` kullanabilirsiniz:

```makefile
C = gcc
CXX = clang++

SOURCE_C = foo.c
OBJECTS_C = foo.o

SOURCE_CXX = 1.1.cpp

TARGET = 1.1
LDFLAGS_COMMON = -std=c++2a

all:
	$(C) -c $(SOURCE_C)
	$(CXX) $(SOURCE_CXX) $(OBJECTS_C) $(LDFLAGS_COMMON) -o $(TARGET)

clean:
	rm -rf *.o $(TARGET)
```

> **Not**: `Makefile` içindeki girintiler için boşluk karakteri yerine sekme kullanılır. Bu kodu doğrudan düzenleyicinize kopyalarsanız sekme otomatik olarak değiştirilebilir. Lütfen `Makefile` içindeki girintilerin sekmelerle oluşturulduğundan emin olun.
>
> `Makefile` kullanımını bilmiyorsanız, önemli değil. Bu öğreticide, çok karmaşık yazılmış kodlar oluşturmayacaksınız. Bu kitabı ayrıca komut satırında `clang++ -std=c++2a` kullanarak da okuyabilirsiniz.

Modern C++'ta yeniyseniz, muhtemelen şu küçük kod parçasını hala anlamıyorsunuzdur:

```cpp
[out = std::ref(std::cout << "C kodundan sonuç: " << add(1, 2))](){
    out.get() << ".\n";
}();
```

Şimdilik merak etmeyin, daha sonraki bölümlerimizde bunlarla tanışacağız.

[İçindekiler](./toc.md) | [Önceki Bölüm](./00-preface.md) | [Sonraki Bölüm: Dil Kullanılabilirlik İyileştirmeleri](./02-usability.md)

## Ek Okumalar

- [C++ Turu (2. Baskı) Bjarne Stroustrup](https://www.amazon.com/dp/0134997832/ref=cm_sw_em_r_mt_dp_U_GogjDbHE2H53B)
- [C++ Tarihçesi](http://en.cppreference.com/w/cpp/language/history)
- [C++ Derleyici Desteği](https://en.cppreference.com/w/cpp/compiler_support)
- [ISO C ve ISO C++ Arasındaki Uyumsuzluklar](http://david.tribble.com/text/cdiffs.htm#C99-vs-CPP98)

## Lisanslar

<a rel="license" href="http://creativecommons.org/licenses/by-nc-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nc-nd/4.0/88x31.png" /></a><br />Bu çalışma [Ou Changkun](https://changkun.de) tarafından yazılmıştır ve <a rel="license" href="https://creativecommons.org/licenses/by-nc-nd/4.0/deed.tr">Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License</a> ile lisanslanmıştır. Bu depodaki kaynak kodlar, [MIT lisansı](../../LICENSE) altında açık kaynaklıdır.
