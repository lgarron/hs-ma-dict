# Haskell-Mathematica Dictionary

## Translations

- Creating lists
  - `[1..n]` <-> `Range[n]`
  - `[m, m+k..n]` <-> `Range[m, n, k]`
  - `[f x | x <- list]` <-> `Table[f[x], {x, list}]`
- List operations
  - `head` <-> `First`
  - `tail` <-> `Rest`
  - `init` <-> `Most`
  - `last` <-> `Last`
  - `list !! n` <-> `list[[n+1]]` (list indexing)
  - `take n list` <-> `Take[list, n]`
  - `takeWhile f list` <-> `TakeWhile[list, f]`
  - `drop n list` <-> `Drop[list, n]`
  - `reverse` <-> `Reverse`
  - `length` <-> `Length`
- List manipulation
  - `(++)` <-> `Join`
  - `filter f list` <-> `Select[list, f]`
  - `map f list` <-> `f /@ map` (or `Map[f, list]`)
  - `zipWith f x y` <-> `Inner[f, x, y, List]`
  - `concat lists` <-> `Flatten[lists, 1]`
  - `Data.List.intersperse list x` <-> `Riffle[list, x]`
  - `nub` <-> `DeleteDuplicates` (or `Union`)
- Functions
  - `\x -> f x` <-> `f[#] &` (or `Function[{x}, f[x]]`) (anonymous function)
  - `\x y -> f x y` <-> `f[#1, #2] &` (or `Function[{x, y}, f[x, y]]`) (multi-argument anonymous function)
  - `curry` <-> (see below)
  - `uncurry` <-> (see below)
- Folding
  - `foldl f z list` <-> `Fold[f, z, list]`
  - `scanl f z list` <-> `FoldList[f, z, list]`
  - `take (n + 1) $ iterate f list` <-> `NestList[list, n]`
- Grouping
  - `group` <-> `Split`
  - `groupBy` <-> `SplitBy`
- Notation
  - ``x `f` y`` <-> `x~f~y` (infix notation)
- Conventions
  - `adjective` or `isAdjective` <-> `AdjectiveQ` (boolean function naming)

## Memoization

### Haskell
Use [Data.Memocombinators](http://hackage.haskell.org/packages/archive/data-memocombinators/0.3/doc/html/Data-MemoCombinators.html)

### Mathematica

    Clear[f]; (* Necessary to clear the old memoized values. *)
    f[x_] := f[x] = (* Calculation using x. *)

## Easily curriable function in Mathematica

Although actual currying isn't that useful, this is sometimes a useful idiom:

    f[x_][y_] := x + y;
    f[2] /@ {1, 2, 3, 4}

## `curry`/`uncurry` in Mathematica

... but, just in case:

    Curry[f_  , x___][y___] := f[x, y]
    Curry[Plus, 2, 4][3, 5]

    Uncurry[f_][x_, y___] := f[x][y];
    f[x_][y_] := x + y;
    Uncurry[f][2, 3]