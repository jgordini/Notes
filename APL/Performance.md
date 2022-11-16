My performance heuristics: Flat is much faster than nested. Flat Boolean arrays, and primitive functions operating on them, are particularly fast. Avoid extending arrays, especially at the front. Prefer array techniques ahead of recursion and power.

[](https://chat.stackexchange.com/transcript/message/62384026#62384026 "click for message actions")

If you do need recursion or power, use external accumulators, not the function arguments if you're accumulating many items. Only use primitives, or optimised 'idioms' with operators, not your own functions. In RIDE, you can make offical idioms show in a different colour. Don't use Scan (unless with an idiom) on any sizeable array. Stencil is a performance super-massive black hole, with a thorny maze of rules for which operands perform, and which don't. Test, don't assume.

 talk on the U-net convolutional neural net from Dyalog '22 just published shows a point of picking an optimal operand for Stencil in order to make it go faster.

 In-place extension of arrays at the end should be fine.
https://www.youtube.com/watch?v=f0qhOKW0iw0

http://docs.dyalog.com/14.0/Dyalog%20APL%20Idioms.pdf
In apl.cart they're prefixed with "Fast:"

  
Preferences -> Colours -> Clone Theme
selected {⍵[⍋⍵]} and changed the drop down to idiom
