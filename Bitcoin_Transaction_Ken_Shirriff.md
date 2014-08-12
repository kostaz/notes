Understanding Bitcoin Transaction
---------------------------------

I've decided to really get hold of Bitcoin Transactions.
The most disappointing thing about Bitcoin is there are too many wordy posts
and blog posts - you really get drown in that information... not adding to
the actual understanding how the stuff works.

This article is going to fix it.  :-)

This post explains the code that stands behind the **excellent** post by
Ken Shirriff about Bitcoin Transaction:
http://www.righto.com/2014/02/bitcoins-hard-way-using-raw-bitcoin.html.
This Ken's post is a must-pre-read for this post!

The only missing part as I found it myself is explanation of the Python code
that does all the magic of creating a Bitcoin Transaction from scratch.

Important note: I have total zero experience and even knowledge of Pythong,
hence, the post talks about a **lot** of details which may be readily skipped
by a knowledgeable reader.

Let's take a deep dive!

The steps are:
 - Generate Bitcoin address and keys
 - Create raw Bitcoin transaction from scratch
 - Sign raw Bitcoin transaction
 - Send signed transaction to Bitcoin network
 - Verify that transaction is excepted and processed


`countLeadingChars`
------------------

The most simple function to understand is `countLeadingChars`:
```
def countLeadingChars(s, ch):
    count = 0
    for c in s:
        if c == ch:
            count += 1
        else:
            break
    return count
```

Well, `countLeadingChars` returns a number of leading characters `ch`
in the string `s`. For example, `countLeadingChars("QQ42", 'Q')` returns 2.

Let's test it by writing a simple test function:

```
def test_countLeadingChars(s, ch):
	count = utils.countLeadingChars(s, ch)
	print 'String "' + s + '" has ' + str(count) + " leading char '" + ch + "'"

test_countLeadingChars("0", '1')
test_countLeadingChars("1", '1')

test_countLeadingChars("0", '0')
test_countLeadingChars("1", '0')

test_countLeadingChars("112233", '0')
test_countLeadingChars("112233", '1')
test_countLeadingChars("112233", '2')
```

Well, the output is:
```
$ python test_countLeadingChars.py
String "0" has 0 leading char '1'
String "1" has 1 leading char '1'
String "0" has 1 leading char '0'
String "1" has 0 leading char '0'
String "112233" has 0 leading char '0'
String "112233" has 2 leading char '1'
String "112233" has 0 leading char '2'
```

`struct.pack`
------------
This `struct.pack` is taken straight from Python Standard Library's
String Services:
Link https://docs.python.org/2/library/struct.html#struct.pack

Excerpt:
`struct.pack(fmt, v1, v2, ...)`
Return a string containing the values v1, v2, ... packed according to the given format. The arguments must match the values required by the format exactly.

Ken uses various formatters (`fmt`) in the code. Let's look at some of them here
and the others formatters will be explained in the place of usage.

**`struct.pack('<B', n)`**
Converts a number `n` of type `unsigned char` to little-endian string.
Note: Little-Endian defined controlled by `<`.

Let's test it:
```
import struct

print struct.pack('<B', 0)
print struct.pack('<B', 1)
print struct.pack('<B', 64)
print struct.pack('<B', 255)
```

Well, the output is:
```
$ python test_struct_pack.py | od -t x1
0000000 00 0a 01 0a 40 0a ff 0a
```
Where the `unsigned char` numbers (0, 1, 64, and 255) were converted to binary little-endian string.

Note: `0x0a` stands for line feed as seen here:
http://www.theasciicode.com.ar/ascii-control-characters/line-feed-ascii-code-10.html

Let's look at some more examples.



