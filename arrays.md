PHP gyakorlófeladatok
=====================

is_assoc()
----------

Írj függvényt is_assoc() néven, mely megadja, hogy egy tömb asszociatív-e vagy nem.
Paraméterek
 * $arr: a vizsgált tömb
Visszatérési érték: boolean (true, ha $arr aszsociatív tömb, egyébként false)

batch_delete_keys()
-------------------

Írj függvényt batch_delete_keys() néven, mely egy tömbből kitörli a másik tömbben megadott kulcsokat
Paraméterek
 * $arr: az a tömb, melyből törölni kell, cím szerinti paraméter
 * $keys_to_be_deleted: a törlendő kulcsok numerikus tömbje

Példa:

	$arr = array(
		'hello' => 'world',
		'foo' => 'bar'
	);

	$keys = array('foo');
	batch_delete_keys($arr, $keys);
	// $arr értéke: array('hello' => 'world')

shiftcopy()
-----------

Írj függvényt shiftcopy() néven, mely cím szerint megkap két tömböt, az első tömb első N elemét átteszi a 2. tömb elejére.
Paraméterek:
 * $n: a másolandó elemek száma
 * $src: ebből a tömbből távolítjuk el az első N elemet
 * $dst: ennek a tömbnek az elejére írjuk $src első N elemét
Megjegyzés: array_shift() és array_unshift() függvényeket kell használni

Példa:

	$src = array(1, 2, 3, 4, 5);
	$dst = array(6, 7);
	shiftcopy($src, $dst, 3);
	// $src értéke array(4, 5)
	// $dst értéke array(1, 2, 3, 6, 7)

batch_call()
------------
	
Írj függvényt batch_call() néven, mely paraméterként megkap egy tömböt, az ebben található callable típusú értékeket meghívja, a függvény visszatérési értéke pedig egy tömb, mely a hívások eredményét tartalmazza
Paraméterek:
 * $arr: ebben a tömbben keressük a callable értékeket
Visszatérési érték: a hívások eredményét tartalmazó tömb. A kulcsok az $arr tömbben található kulcsok közül a callable-k kulcsai
Megjegyzés: használd az is_callable() beépített függvényt

Példa:

	$maybe_callables = array('hello' => 'world');
	$maybe_callables['fn'] = function() {
		return 2;
	};
	$maybe_callables []= 'rand';
	$results = batch_call($maybe_callables);
	// $results értéke: array('fn' => 2, 0 => <valami random szám>)


wrap_vals()
-----------

Írj függvényt wrap_vals() néven, mely paraméterként megkap egy tömböt, visszatérési értéke pedig egy olyan tömb, melyben a kulcsok a paraméter-tömb kulcsai, az értékek pedig olyan névtelen függvények, melyek visszaadják a paraméter-tömbnek a kulcshoz tartozó értékét
Paraméterek:
 * $arr: a tömb, melynek értékeit a névtelen függvénybe kell csomagolni
 
Példa:

	$arr = array('hello' => 'world', 'foo' => 'bar);
	$callables = wrap_vals($arr);
	echo $callables['hello'](); // kiírja, hogy world
	echo $callables['foo'](); // kiírja, hogy bar

section_sum()
-------------

Írj függvényt section_sum() néven, mely 2 tömböt kap paraméterként, mindkettő asszociatív, és az értékek számok. A függvény visszatérési értéke egy tömb, melyben csak azok a kulcsok szerepelnek, melyek mindkét paraméterként kapott tömbben szerepelnek, és az értékek a paraméter-tömbökben található értékek összege.

Megjegyzés: használd az array_intersect() függvényt

Példa:

	$arr1 = array('red' => 1, 'green' => 2, 'blue' => 3, 'yellow' => 4);
	$arr2 = array('blue' => 30, 'purple' => 45, 'green' => 22, 'black' => 11);
	$result = section_sum($arr1, $arr2);
	// $result értéke array('green' => 24, 'blue' => 33)
