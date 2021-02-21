.. highlight:: toml

.. _setup-contract:

=====================================
Bir akıllı sözleşme projesi oluşturma
=====================================

Rust' ta bir akıllı sözleşme sıradan bir kütüphane olarak yazılır. Daha sonra
Rust hedefine Wasm ``wasm32-unknown-unknown`` kullanılarak derlenir
ve Rust kütüphanesi bağımlılıklarının yönetmek için sadece Cargo_ kullanılır.

Yeni bir akıllı sözleşme oluşturmak için öncelikle bir dizin oluşturun ve dizin
içinde terminal ekranında şu konutu çalıştırın;

.. code-block:: console

   $cargo init --lib

Bu işlem birkaç dosya ve dizin oluşturarak Rust Kütüphanesi' nı kuracaktır.
This will set up a default Rust library project by creating a few files and
directories.
Bu dizin ``Cargo.toml`` dosyası ``src`` dizini ve bazı gizli dosyalar içerir.

Wasm' ı derleyebilmek için cargo' ya doğru ``crate-type`` 'ı belirtmeliyiz.'
Bu belirme işlemini ``Cargo.toml``: içerisinde aşağıdaki komutlar eklenerek
yapılır.

   [lib]
   crate-type = ["cdylib", "rlib"]

Akıllı sözleşme standart kütüphanesini oluşturma
================================================

Sıradaki adım ``concordium-std`` 'ı bağımlılık olarak eklemektir.
Bu Rust Kütüphanesi küçük ve verimli akıllı söyleşmeler yazmak için çeşitli
makrolar ve komutlar içerir.

Kütüphaneyi eklemek için ``Cargo.toml`` dosyasına aşağıdaki kod satırı eklenir.
``concordium-std = "*"`` (`*` yerine `concordium-std`_ ın en son sürüm numarası
gelmelidir.)

   [dependencies]
   concordium-std = "0.4"

Kütüphane ile ilhili bilgilere docs.rs_ 'den ulaşabilisiniz.

.. note::

   Standart kütüphane yerine özelleştirilmiş bir tane kullanmak isterseniz,
   ``concordium-std`` reposunu klonlayıp,``Cargo.toml``: içerisine bağımlılıklar
   için gerekli kodları eklemelisiniz.

      [dependencies]
      concordium-std = { path = "./path/to/concordium-std" }

.. _Rust: https://www.rust-lang.org/
.. _Cargo: https://doc.rust-lang.org/cargo/
.. _rustup: https://rustup.rs/
.. _repository: https://gitlab.com/Concordium/concordium-std
.. _docs.rs: https://docs.rs/crate/concordium-std/
.. _`concordium-std`: https://docs.rs/crate/concordium-std/

Herşey tamam. Yeni bir akıllı sözleşme geliştirmek için artık hazırsınız.
