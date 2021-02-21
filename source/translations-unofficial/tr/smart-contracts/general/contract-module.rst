.. _contract-module:

======================
Akıllı Sözleşme Modülleri
======================

Akıllı sözleşmeler, *akıllı sözleşme modüllerindeki* zincirde oluşturulur.

.. note::

   Akıllı Sözleşme Modülüne genellile basit olarak *modül* olarak adlandırılır.

Bir modül, kodun sözleşmeler arasında paylaşılmasına izin veren bir veya
daha fazla akıllı sözleşme içerebilir ve isteğe bağlı olarak
:ref:`kontrat şablonu <contract-schema>` içerebilir..

.. graphviz::
   :align: center
   :caption: A smart contract module containing two smart contracts.

   digraph G {
       subgraph cluster_0 {
           node [fillcolor=white, shape=note]
           label = "Module";
           "Crowdfunding";
           "Escrow";
       }
   }

Modül bağımsız olmalıdır ve yalnızca zincirle etkileşime izin veren kısıtlı
bir içeri alma listesine sahip olmalıdır. Bunlar Node Sunucular tarafından
sağlanır ve ``concordium`` adı verilen bir modülü içe aktararak akıllı
sözleşme için kullanılabilir.

.. seealso::

   Check out :ref:`host-functions` for a complete reference.

Blok Zincir Yazılım Dili
========================

Concordium blok zincirinin akıllı sözleşme dili, taşınabilir bir derleme hedefi
olacak ve korumalı ortamlarda çalıştırılmak üzere tasarlanmış bir Web Assembly
(kısaca Wasm) alt kümesidir. Bu kullanışlıdır. Çünkü akıllı sözleşmeler ağdaki
koda güvenmeyen Baker' lar tarafından çalıştırılacaktır.

Wasm düşük seviyeli bir dildir ve elle yazmak pratik değildir. Bunun yerine
daha yüksek seviyeli bir dilde akıllı sözleşmeler yazılabilir ve bunlar daha
sonra Wasm'a derlenir.

.. _wasm-limitations:

Sınırlamalar
-----------

.. todo::

   Add other limitations, such as start sections...

Blok zinciri ortamı, her bir Node Server' ın akıllı sözleşmeyi tam olarak aynı
miktarda kaynağı kullanarak tam olarak aynı şekilde çalıştırabilmesi açısından
çok özeldir. Aksi takdirde Node Server' lar, zincirin durumu hakkında fikir
birliğine varamazlar. Bu nedenle akıllı sözleşmelerin sınırlı bir Wasm alt
kümesine yazılması gerekir.

Kayan Nokta Sayıları
^^^^^^^^^^^^^^^^^^^^

Wasm'ın kayan nokta sayılarını desteklemesine rağmen, bir akıllı sözleşmenin
bunları kullanmasına izin verilmez. Bunun nedeni, Wasm kayan noktalı sayıların
özel bir NaN ("sayı olmayan") değeri olabilmesidir ve bu değerin işlenmesi
belirsizlikle sonuçlanabilir.

Kısıtlama statik olarak uygulanır, yani akıllı sözleşmeler kayan nokta türleri
içeremez veya kayan nokta değerleri içeren herhangi bir talimat içeremez.

Dağıtım
=======

Zincire bir modül dağıtma işlemi, modül bayt kodunu Concordium ağına bir işlem
olarak göndermeyi ifade eder. Eğer bu işlem geçerli ise bir bloğa dahil
edilecektir. Bu işlem, diğer her işlem gibi belirli bir maliyete sahiptir.
Maliyet, bayt kodunun boyutuna bağlıdır ve hem modülün geçerliliğini kontrol
etmek hem de zincir üzerinde depolamak için tahsil edilir.

Dağıtımın kendisi akıllı sözleşme yürütmez. Yürütmek için, bir kullanıcının
önce bir sözleşmenin bir örneğini oluşturması gerekir.


.. seealso::

   See :ref:`contract-instances` for more information.

.. _smart-contracts-on-chain:

.. _smart-contracts-on-the-chain:

.. _contract-on-chain:

.. _contract-on-the-chain:

Blok Zincir üzerinde Akıllı Sözleşme
====================================

Blok zincirdeki akıllı sözleşme, konuşlandırılmış bir modülden dışa aktarılan
işlevlerin bir koleksiyonudur. Bunun için kullanılan somut mekanizma Web
Assembly' nin dışa aktarma bölümüdür. Bir Akıllı Sözleşme, yeni örnekleri
başlatmak için bir işlevi dışa aktarmalıdır ve örneği güncellemek için sıfır
veya daha fazla işlevi dışa aktarabilir.

Bir akıllı sözleşme modülü, birden çok farklı akıllı sözleşme için işlevleri
dışa aktarabildiğinden, işlevleri bir adlandırma şeması kullanarak
ilişkilendiririz:

- ``init_<contract-name>``: Bir akıllı sözleşme başlatmak için ``init_`` komutu
  ve ardından akıllı sözleşmemini adıyla başlamalıdır. Akıllı sözleşme sadece
  ASCII alfanümerik yada noktalama işaretleniden oluşabilir. Sadece ``.`` karakterine
  izin verilmez.

- ``<contract-name>.<receive-function-name>``: Bir akıllı sözleşmeyle etkileşime
  girmek için ``.`` işlevinden sonra sözleşme adı ve ardından işlev adı gelir.
  Akıllı sözleşmenin adının ``.`` karekteri içermesine izin verilmez.

.. Not::

   Eğer Rust ve ``concordium-std`` kullanan bir akıllı sözleşme geliştiricisi
   iseniz, prosedür makrolalrı için ``#[init(...)]`` ve ``#[receive(...)]``
   şemalarından doğru olanı seçmelisiniz.

.. _Web Assembly: https://webassembly.org/
