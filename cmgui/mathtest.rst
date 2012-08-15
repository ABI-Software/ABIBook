..  _mathtest:

Testing MathJax LaTeX support
=============================

Just a test. Also, a cheeky little test of :ref:`pep-3118-update`.

First test
----------

.. math::

   (a + b)^2 = a^2 + 2ab + b^2

   (a - b)^2 = a^2 - 2ab + b^2

Some text

.. math::

   z \left( 1 \ +\ \sqrt{\omega_{i+1} + \zeta -\frac{x+1}{\Theta +1} y + 1}
   \ \right)
   \ \ \ =\ \ \ 1

More intervening text

.. math::

   \frac{d}{dx}\left( \int_{0}^{x} f(u)\,du\right)=f(x).

Does this get stripped?

.. raw:: html

   <p id="demo">This is a paragraph.</p>

   <script type="text/javascript">
   document.getElementById("demo").innerHTML=Date();
   </script>

Probably.