# Codewars Haskell

#### Bitwise operations

```haskell
import Data.Word (Word32) -- instance of Data.Bits
import Data.Bits

-- 1 if any bit at an odd index is 1 else 0
anyOdd :: Word32 -> Int
anyOdd w = if (w .&. 0xaaaaaaaa)/=0 then 1 else 0
```

- prefix hexadecimal with`0x` 

- common bitwise operations: `.&.` `.|.` `xor` `complement` `shift` `rotate`  

#### Debugging

```haskell
import Debug.Trace
-- trace :: String -> a -> a
-- The trace function outputs the trace message given as its first argument, before returning the second argument as its result.
-- trace ("calling f with x = " ++ show x) (f x)
debug = flip trace -- allows to comment it out easily

-- A ray of light enters a rectangle of mirrors and can exit by any corner
-- True if it exits in the bottom-left or top-right corner, False if it exits in another corner
reflections :: Int -> Int -> Bool
reflections maxX maxY = bounce 1 1 1 1
  where 
    bounce x y sx sy 
      | elem (x,y) [(0, 0), (maxX, maxY)] = True
      | elem (x,y) [(0, maxY), (maxX, 0)] = False
      | otherwise = bounce (x+ssx) (y+ssy) ssx ssy -- `debug` ("calling bounce with = " ++ show (x, y))
      where ssx = if x==0 || x==maxX then -sx else sx
            ssy = if y==0 || y==maxY then -sy else sy
            
-- reflections x y = ((==) `on` odd . (`div` g)) x y where g = gcd x y
-- reflections = (==) `on` countTrailingZeros
```

#### Common sums

| Sum of                         | Formula        |
| ------------------------------ | -------------- |
| first cubes                    | (n(n+1)/2)²    |
| first squares                  | n(n+1)(2n+1)/2 |
| n first odd natural numbers    | n²             |
| n first even natural numbers   | n(n+1)         |
| n first natural numbers        | n(n+1)/2       |
| log of n first natural numbers | log(n!)        |

It is often useful to pair numbers to find patterns

```haskell
{-
n=99
  1   3   5 .. 99 |(n+1)/2 times
n-1 n-3 n-5 ..  1 |(n+1)/2 times
sum [1,3..n] = (n+1)^2/4 (n impair)

n=100
0     2   4   6 .. 100 |1+n/2 times
n + n-2 n-4 n-6 ..   0 |1+n/2 times
sum [0,2..n] = n^2/4+n/2 (n pair)
-}
```

#### Application, composition, evaluation order

| Flow                       | Base          |
| -------------------------- | ------------- |
| `x |> f`                   | `x & f`       |
| `f <| x`                   | `f $ x`       |
| `apply x f`                | `f x`         |
| `f .> g`                   | `f >>> g`     |
| `g <. f`                   | `g . f`       |
| `compose f g x`            | `g (f x)`     |
| `x !> f`                   | -             |
| `f              | `f $! x` |               |
| `apply' x f`               | `seq x (f x)` |

```haskell
module DivisibleByThree where

import Data.Char

divisibleByThree :: String -> Bool
divisibleByThree str = (map digitToInt str) |> sum |> (`rem` 3) |> (==0)
	where (|>) = &
--  where (►) = flip ($)
-- divisibleByThree str = (==0) $ (`rem` 3) $ sum $ (map digitToInt str)
```

