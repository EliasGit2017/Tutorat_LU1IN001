### Exercice 2 : Analyse de Code (RLE)

#### Question 1 :

```python
def myst(s : str) -> list[int]:
    """Précondition : s est composee de 0 et de 1"""
    x : list[int] = []
    y : str = "0"
    z : int = 0
    a : str
    for a in s:
        if a == y:
            z = z + 1
    	else:
            x.append(z)
    		z = 1
    		if y == "0":
    			y = "1"
    		else:
    			y = "0"
    x.append(z)
    return x
```

#### Question 2 :

`myst(‘00100011’)`

| Tour   | Variable a | Variable x | Variable z | Variable y |
| ------ | :--------: | :--------: | :--------: | :--------: |
| entrée |     -      |     []     |     0      |    '0'     |
| 1er    |    '0'     |     []     |     1      |    '0'     |
| 2ème   |    '0'     |     []     |     2      |    '0'     |
| 3ème   |    '1'     |    [2]     |     1      |    '1'     |
| 4ème   |    '0'     |   [2,1]    |     1      |    '0'     |
| 5ème   |    '0'     |   [2,1]    |     2      |    '0'     |
| 6ème   |    '0'     |   [2,1]    |     3      |    '0'     |
| 7ème   |    '1'     |  [2,1,3]   |     1      |    '1'     |
| 8ème   |    '1'     |  [2,1,3]   |     2      |    '1'     |
| Sortie |     -      | [2,1,3,2]  |     2      |    '1'     |

`la valeur retournée est bien [2,1,3,2]`

`‘00100011’`

#### Question 3 :

Pour obtenir [0,3,2,5,1] en résultat , il faut exécuter `myst('11100111110')` 

#### Question 4 :

```python
def repetition(c : str, k : int) -> str: 
	"""précondition : len(c) == 1 k >= 0
	Retourne k répétitions de c"""
    return c * k
```

#### Question 5 :

```python
>>> demyst([3,2, 1, 3])
’000110111’
>>> demyst([0,3, 2, 1, 3])
’111001000’
>>> demyst([4,4])
’00001111’
>>> demyst([4,0, 4])
’00000000’
```



```python
def demyst(L : List[int]) -> str:
    """Precondition : Tous les éléments de L sont positifs ou nuls
    Retourne la chaîne de caractères correspondant à L"""
    res : str = ""
    c : str = "0"
    k : int
    for k in L:
        res = res + repetition(c,k)
        if c == "0":
            c = "1"
        else:
            c = "0"
   	return res
```



### Exercice 4 : Image en noir et blanc

```python
>>> coupe(((0,0), 12, 2))
((0, 0), 9, 2)
>>> coupe(((8,19), 1, 2))
((0, 0), 0, 0)
>>> coupe(((3,2), 3, 4))
((3, 2), 3, 4)
>>> coupe(((8,9), 3, 10))
((8, 9), 1, 7)
```



```python
# Definition du type Rect
type Rect = tuple[tuple[int, int], int, int]

def coupe(r : Rect) -> Rect:
    """Retourne un rectangle `r` correspondant au plus grand rectangle inclus
    dans l'image"""
    coin_haut_gauche, nb_lignes, nb_colonnes = r
    lp, cp = coin_haut_gauche
    if (cp < 0 or cp >=16 or lp < 0 or lp >= 9):
        return ((0,0),0,0)
    else:
        return (coin_haut_gauche, min(nb_lignes, 9-lp), min(nb_colonnes, 16-cp))
```

