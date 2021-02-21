.. _setup-tools:

==========================================
Geliştirme için gerekli araçların kurulumu
==========================================

Bir akılı sözleşme geliştirmeye başlamadan gerekli yazılımların kurulması
gerekmektedir.

Rust ve Cargo
==============

Öncelikle `install rustup`_ ile makinenize Rust ve Cargo' yu kurmalısınız.
Kurulumdan sonra ``rustup`` komutunu Wasm hedefini derlemek için kullanın;

.. code-block:: console

   $rustup target add wasm32-unknown-unknown

Cargo Concordium
================

Cargo Concordium, Concordium blok zincirinde akıllı sözleşmeler geliştirmenizi
sağlayan bir araçtır.
Şunlar için kullanılabilir;
:ref:`Derleme <compile-module>` ve :ref:`Test Etme <unit-test-contract>`
gibi akıllı sözleşmeleri özelliklerini çalıştırır ve :ref:`sözleşme şeması oluşturma
<build-schema>` özelliğini aktif edebilir.

.. todo::

   Add links for testing and schemas.

Cargo Concordium, :ref:`Concordium Yazılımı <downloads>` paketiyle dağıtılır.
Bu araç PATH 'inize tanımlanmalıdır.

Cargo Concordium çalıştırılması ile ilgili yardım;

.. code-block:: console

   $cargo concordium --help

Concordium Yazılımı
===================

:ref:`concordium-client<concordium_client>` akıllı sözleşmeleri devreye alma
ve bunlarla etkileşim kurmaya yarayan bir araçtır. :ref:`Concordium Yazılımı
<downloads>` nın bir parçası olarak dağıtılır.

.. Not::

   Bir akıllı sözleşme dağıtmak yada zincirle etkileşimde bulunmak için Bir
   Node Server çalıştığınızdan emin olun. Daha fazla bilgi için
   :ref:`Node Server Çalıştırma <run-a-node>`.

.. _Rust: https://www.rust-lang.org/
.. _Cargo: https://doc.rust-lang.org/cargo/
.. _install rustup: https://rustup.rs/
.. _crates.io: https://crates.io/
