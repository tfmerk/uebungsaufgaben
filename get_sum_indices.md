# Aufgabe

Es soll eine Funktion geschrieben werden, welche eine Liste mit Ganzzahlen (integer) und eine weitere Ganzzahl (integer) entgegen nimmt und die beiden Indexe der Zahlen ausgibt, die zu der einzelnen Zahl (integer) im zweiten Parameter addieren.

# Lösungsansatz (PHP)

```PHP
<?php

// ----------------------------------------------------------------------------------------
// Setup
// ----------------------------------------------------------------------------------------

$list = [ 1, 2, 8, 12, 15 ];
$expected = [ 2, 3 ];
$target = 20;

// ----------------------------------------------------------------------------------------
// Function call and print output
// ----------------------------------------------------------------------------------------

$result = getIndicesBySum($list, $target);

var_dump($result, $expected);


// ----------------------------------------------------------------------------------------
// Function
// ----------------------------------------------------------------------------------------

/**
 * Searches the array $list for two indices that are summed up equal to $target.
 * 
 * @param array $list
 * @param int $target
 * 
 * @return array
 */
function getIndicesBySum(array $list, int $target): array
{
	$listLength = count($list);
	$result = [];
	
	for ($initialIndex = 0; $initialIndex < $listLength; $initialIndex++) {
		$initialValue = $list[$initialIndex];
		for ($i = $initialIndex + 1; $i < $listLength; $i++) {
			if ($initialIndex !== $i && $initialValue + $list[$i] === $target) {
				$result = [ $initialIndex, $i ];
				break;
			}
		}
	}
	
	return $result;
}
```

Die aufgerufene Methode `getIndicesBySum` bekommt die Liste/Array sowie die Ganzzahl übergeben.
In der Funktion gibt es zwei Schleifen, die jede Zahl mit jeder Zahl aufsummiert ohne dies zu doppeln.

```
1 + 2,  1 + 8,  1 + 12, 1 + 15  // Durchlauf 1
2 + 8,  2 + 12, 2 + 15          // Durchlauf 2
8 + 12, 8 + 15                  // Durchlauf 3 -> Treffer!
12 + 15                         // Durchlauf 4 -> wird nicht mehr durchlaufen
```

Sollte der gesuchte Wert aus `$target` gefunden werden  (8 + 12 = 20), so werden die beiden Indizes als neues Array zurückgegeben. Der Wert im dem dritten Schleifendurchlauf gefunden.