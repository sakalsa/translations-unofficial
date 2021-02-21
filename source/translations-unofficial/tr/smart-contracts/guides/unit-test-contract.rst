.. _unit-test-contract:

=================================
Rust 'ta bir sözleşmeyi test edin
=================================

Bu kılavuz size Rust'ta yazılmış akıllı bir sözleşme için birim testlerinin
nasıl yazılacağını gösterecektir. Akıllı sözleşme Wasm modülünü test etmek için
 :ref:`local-simulate` bakabilirisiniz.

Rust 'ta bir akıllı sözleşme kütüphane olarak yazılır ve işlevler bir ``#[test]``
özniteliği ekleyerek işlemleri test edebiliriz.

.. code-block:: rust

    // sözleşme kodu
    ...

    #[cfg(test)]
    mod test {

        #[test]
        fn some_test() { ... }

        #[test]
        fn another_test() { ... }
    }

Testi ``cargo`` ile şu komutla çalıştırıyoruz.

.. code-block:: console

   $cargo test

Varsayılan olarak, bu komut sözleşmeyi derler ve yerel hedefiniz için
(büyük olasılıkla x86_64) kod işlemek için test eder ve bunları çalıştırır.
Bu tür testler, ilk geliştirmede ve işlevselliğin test edilmesinde yararlı
olabilir.
Kapsamlı testler için hedef platformu, yani Wasm32 'yi dahil etmek
önemlidir. Platformlar arasında bir sözleşmenin davranışını değiştirebilecek
bir dizi ince fark vardır. Bir fark, Wasm32 'nin çoğu platform için ortak olan
sekiz bayt yerine dört bayt kullandığı işaretçilerin boyutuyla ilgilidir.

Birim Testleri Yazma
====================

Birim testleri genellikle şunları yaptığınız üç bölümden oluşan bir yapıyı izler:
bir durum kurar, bir birim kod çalıştırır ve kodun durumu ve çıktısı durumunu
sorgular.

Eğer sözleşme fonksiyonları ``#[init(..)]`` yada ``#[receive(..)]`` kullanılarak
yazılmışsa bunları direkt test edebilisiniz.

.. code-block:: rust

   use concordium_std::*;

   #[init(contract = "my_contract", payable, enable_logger)]
   fn contract_init(
      ctx: &impl HasInitContext<()>,
      amount: Amount,
      logger: &mut impl HasLogger,
   ) -> InitResult<State> { ... }

   #[receive(contract = "my_contract", name = "my_receive", payable, enable_logger)]
   fn contract_receive<A: HasActions>(
      ctx: &impl HasReceiveContext<()>,
      amount: Amount,
      logger: &mut impl HasLogger,
      state: &mut State,
   ) -> ReceiveResult<A> { ... }

Fonksiyon bağımsız değişkenleri için test saplamaları ``concordium-std`` 'ı'
``test_infrastructure`` alt bölümünde bulabilisiniz.

.. seealso::

   Daha fazla bilgi için concordium-std yardım bölümüne bakabilirsiniz.

.. todo::

   Birim testelerinin nasıl yazılacağı ilgili daha fazla bilgi gösterin.

Wasm 'da test çalıştırma
========================

Testlerin yerel makine koduna derlenmesi çoğu durumda yeterlidir,
ancak testleri Wasm'a derlemek ve düğümler tarafından kullanılan tam
yorumlayıcıyı kullanarak çalıştırmak da mümkündür. Bu, test ortamını zincir
üzerindeki çalışma ortamına daha yakın hale getirir ve bazı durumlarda daha
fazla hata yakalayabilir.

Geliştirme aracı olarak kullanıdığımız ``cargo-concordium`` testin Wasm
yorumlayıcısı ile Concordium Node 'larına gönderebileceği komutları içerir.

.. seealso::

   ``cargo-concordium`` kurulumu için ayrıca bakınız :ref:`setup-tools`.

Açıklamalı birim testi için ``#[test]`` yerine ``#[concordium_test]``,
``#[cfg(test)]`` yerine ``#[concordium_cfg_test]`` kullanınız.

.. code-block:: rust

   // contract code
   ...

   #[concordium_cfg_test]
   mod test {

       #[concordium_test]
       fn some_test() { ... }

       #[concordium_test]
       fn another_test() { ... }
   }

``concordium-std`` ``#[concordium_test]`` 'i Wasm makro testlerimizde
çalıştırmak için derlendi. ``wasm-test`` özelliği ile derlendiği zaman
``#[test]`` özelliğini ``cargo test`` şeklinde kullanmak mümkün olur.

Benzer şekilde makro ``#[concordium_cfg_test]`` içeriği ile birlikte
``concordium-std`` ile ``wasm-test`` derlendiğinde ``#[test]`` bize derleme
esnasında testi kontrol etme imkanı verir.

Testler artık aşağıdakiler kullanılarak oluşturulabilir ve çalıştırılabilir:

.. code-block:: console

   $cargo concordium test

BU komut testler ``cargo-concordium`` ile çalıştırldığında ``concordium-std`` 'a
 `wasm-test`` özelliğini kullanacak şekilde derler..

.. warning::

   ``panic!``'ten gelen hata mesajları``assert!`` 'ın farklı versiyonlarında
   Wasm derlerken gösterilmez.

   Bunun yerine tetlerde ``fail!`` yada ``claim!`` varyantını kullanın. Bu
   varyatlarla test başarısız olmadan önce çıktısını hata mesajı olarak geri
   döndürür.
   Bu varyantlar ``concordium-std``içerinde bulunur.

.. todo::

   Yayınlama ile ilgili bilgileri concordium-std: docs.rs/concordium-std 'den
   edinebilirniz.
