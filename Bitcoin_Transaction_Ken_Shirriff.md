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

Let's take a deep dive!

The steps are:
 - Generate Bitcoin address and keys
 - Create raw Bitcoin transaction from scratch
 - Sign raw Bitcoin transaction
 - Send signed transaction to Bitcoin network
 - Verify that transaction is excepted and processed


Generate Bitcoin address and keys
---------------------------------
First function to understand is `countLeadingChars`:
`
def countLeadingChars(s, ch):
    count = 0
    for c in s:
        if c == ch:
            count += 1
        else:
            break
    return count
`


