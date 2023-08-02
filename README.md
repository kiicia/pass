# pass

```
javascript:(function(){
function pass(input, iter_n, out_len) {
    var swap = (a, p, m) => [...a.keys()].forEach(i => {
      var t = (a.length - i + m + p[i % p.length]) % a.length;
      m = a[i] = a.splice(t, 1, a[i])[0];
    });
    var iter = (a, p, n) => [...Array(n).keys()].forEach(i => swap(a, p, 1));
    var nono = ['\'', '"', '`', '<', '>', '&', '/', '\\'];
    var idxs = [...Array(85).keys()];
    var dict = [...Array(idxs.length + nono.length).keys()]
      .map(i => String.fromCharCode('!'.charCodeAt(0) + i))
      .filter(c => !nono.includes(c))
      .join('');
    var patt = input.split('').map(c => dict.indexOf(c));
    iter(idxs, patt, iter_n);
	return [...Array(out_len).keys()].map(i => {
      iter(idxs, patt, 1);
      return dict[idxs[i]];
    }).join('');
}
if (pass('omgMONKEY!0', 666, 16) !== 'W|i-Z-IUOK{BOd($') alert('self test failed!');
prompt('!', pass(prompt('?'), 666, Number(prompt('len', 16))));
})()
```
