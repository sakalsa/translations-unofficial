.. _Rust: https://www.rust-lang.org/
.. _Cargo: https://doc.rust-lang.org/cargo/
.. _rust-analyzer: https://github.com/rust-analyzer/rust-analyzer

.. _compile-module:

=====================================
Rust akıllı sözleşme modülünü derleme
=====================================

Bu kılavuz size Rust'ta yazılmış akıllı sözleşme modülünü bir Wasm modülüne
nasıl derleyeceğinizi açıklamamaktadır.

Hazırlıklar
===========

Rust ve Cargo' nun kurulu olduğundan ve ``wasm32-unknown-unknown``hedefin
``cargo-concordium`` ile Rust kaynak kodunu derlemeye hazır olduğundan emin olun.

.. seealso::

   Geliştirici araçlarının kurulum ile ilgili gerekli bilgiye burada
   ulaşabilirsiniz.
   :ref:`setup-tools`.

Wasm' a Derleme
===============

Akıllı sözleşme modülleri oluşturmaya yardımcı olmak ve aşağıdaki gibi
özelliklerden yararlanmak için :ref:`Sözleşme Şemaları <contract-schema>` 'na
göz atabilirsiniz. Biz Rust Akıllı Sözleşme oluşturmak için ``cargo-concordium``
aracını kullanmanızı öneririz.

Akıllı sözleşme oluşturmak için şunu çalıştırın;

.. code-block:: console

   $cargo concordium build

Bu kumut, derleme için Cargo_ 'yu kullanır ve sonuş üstünde daha fazla
optimizasyon sağlar.

.. seealso::

  Ayrıca derleme için gerekli adımlara <build-schema>` 'dan ulaşabilirsiniz.'

.. note::

   Aşağıdaki komut ile Cargo_ 'yu kullanarak tek komutla derlemek mümkündür.

   .. code-block:: console

      $cargo build --target=wasm32-unknown-unknown [--release]

   ``--release`` tanımlandığında Wasm modulünün hata ayıklama bilgisi
   içerdiğini unutmayın.

Ana bilgisayar bilgilerini Derleme içerisinden kaldırma
=======================================================

Derlemden sonra Wasm modülünü oluşturan bilgiler ``.cargo`` dizini altında
bulunur.

Çoğu insan için bu hassas bir bilgi değildir, ancak bunun farkında olmak
önemlidir.

Linux'ta yollar şu şekilde incelenebilir:

.. code-block:: console

   strings contract.wasm | grep /home/

.. rubric:: Bilgilerin Kaldırılması

İdeal çözüm, bu yolu tamamen kaldırmak olacaktır, ancak bu maalesef genel
olarak önemsiz bir görev değildir.

Sözleşmenin derlenmesi esnasında ``--remap-path-prefix`` ile dizin bilgilerini
kaldırmak mümkündür.

Unix tabanlı sistemlerde ``cargo concordium``kullanımı sırasında
``RUSTFLAGS`` tanımıyla kaldırılabilir.

.. code-block:: console

   $RUSTFLAGS="--remap-path-prefix=$HOME=" cargo concordium build

Bu işlem kullanıcıların ana yolunu boş dizeyle değiştirir. Diğer yollar da
benzer bir şekilde değiştirilebilir.. Genel kullanım ``--remap-path-prefix=from=to``
ile tanımlama yapılabilir.

Bu tanımla derleme esnansında kalıcı kullanıcı yollu``.cargo/config``
altına tanımlanabilir.

.. code-block:: toml

   [build]
   rustflags = ["--remap-path-prefix=/home/<user>="]

burada `<user>` Wasp modülünü derleyen kullanıcı adı ile değiştirilmelidir.

Uyarılar
--------

Rust araçzinciri için `rust-src`` yüklenmişse bu yukarıdakile muhtemelen
bilgileri kaldırmayacaktır. Bunu için rust-analyzer_ tarzı araçlara ihtiyacınız
olabilir.

.. Ayrıca Bakınız::

   An issue reporting the problem with ``--remap-path-prefix`` and ``rust-src``
   https://github.com/rust-lang/rust/issues/73167
