Whats new in Python 2.7
=======================

Full details from the source http://docs.python.org/dev/whatsnew/2.7.html

.. warn::

   Pygments (used by Sphinx for Syntax highlighting) will not render this
   source unless you tell it to treat it as Python 3. This is due to the 
   new set literals and set/dict comprehensions.

.. highlight:: py3

Sample code::

    from os import system
    import unittest
    import collections


    class TestMe(unittest.TestCase):

        def setUp(self):
            system('touch input')

        def test_set_literal(self):
            a = set((1, 2,))
            b = {1, 2,}
            self.assertEquals(a, b)

        def test_set_comprehension(self):
            a = set(c for c in range(5) if c % 2)
            b = {c for c in range(5) if c % 2} 
            self.assertEquals(a, b)
            self.assertEquals(a, {1, 3})

        def test_dict_comprehension(self):
            a = dict((c, str(c)) for c in range(3))
            b = {c: str(c) for c in range(3)}
            self.assertEqual(a[2], '2')
            self.assertEqual(a, b)

        def test_multi_with(self):
            with file('input') as i: # or used contextlib.nested()
                with file('output', 'w') as o:
                    o.write(i.read())
            with file('input') as i, file('output', 'w') as o:
                o.write(i.read())

        def test_counter(self):
            c = collections.Counter()
            for letter in "hello world":
                c[letter] += 1
            self.assertEquals(c["a"], 0)
            self.assertEquals(c[" "], 1)
            self.assertEquals(c["o"], 2)
            self.assertEquals(c["l"], 3)

        def test_ordered_dict(self):
            a = collections.OrderedDict()
            a['first'] = 1
            a['second'] = 2
            a['athird'] = 3
            self.assertEquals(a.items()[-1], ('athird', 3,))

            del a['first']
            a['first'] = 1
            self.assertEquals(a.items()[-1], ('first', 1,))

            # replace does not change position
            a['second'] = 2
            self.assertEquals(a.items()[-1], ('first', 1,))

        def test_format1000(self):
            self.assertEquals("{:,d}".format(1234567890,), '1,234,567,890')

        @unittest.skip("uhm. not today")
        def test_skipme(self):
            pass

        @unittest.skipIf(1 == 1, "not doing this")
        def test_skipme_conditional(self):
            """there is also a skipUnless version of this"""

        @unittest.expectedFailure
        def test_raises(self):
            self.assertEqual(0, 1)

        def test_context(self):
            with self.assertRaises(ZeroDivisionError):
                a = 1 / 0

        def test_dict_view(self):
            a = {1: 10, 2: 20, 3: 30,}
            v = a.viewkeys()
            del a[2]
            self.assertEquals(list(v), [1, 3])
            self.assertEquals(v | {1, 2}, {1, 2, 3})

        @staticmethod
        def static():
            pass



Not covered in here:
argparse replaces optparse
logging can be configured w/ dicts
memoryviews

