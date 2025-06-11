//zadanie 2
square :: Num a => a -> a
square x = x * x

cube :: Num a => a -> a
cube x = x * x * x

average :: Fractional a => a -> a -> a
average x y = (x + y) / 2

//zadanie3
quadraticRoots1 :: (Floating a, Ord a) => a -> a -> a -> String
quadraticRoots1 a b c =
  let d = b * b - 4 * a * c in
  if d < 0 then "Brak pierwiastków rzeczywistych"
  else if d == 0 then "x = " ++ show (-b / (2 * a))
  else
    let x1 = (-b + sqrt d) / (2 * a)
        x2 = (-b - sqrt d) / (2 * a)
    in "x1 = " ++ show x1 ++ ", x2 = " ++ show x2

quadraticRoots2 :: (Floating a, Ord a) => a -> a -> a -> String
quadraticRoots2 a b c
  | d < 0     = "Brak pierwiastków rzeczywistych"
  | d == 0    = "x = " ++ show (-b / (2 * a))
  | otherwise = "x1 = " ++ show x1 ++ ", x2 = " ++ show x2
  where
    d  = b * b - 4 * a * c
    x1 = (-b + sqrt d) / (2 * a)
    x2 = (-b - sqrt d) / (2 * a)

//zadanie4
factorial :: (Integral a) => a -> a
factorial 0 = 1
factorial n = n * factorial (n - 1)

//zadanie5
fibonacci :: (Integral a) => a -> a
fibonacci 0 = 0
fibonacci 1 = 1
fibonacci n = fibonacci (n - 1) + fibonacci (n - 2)

//zadanie6
minmax :: (Ord a, Num a) => a -> a -> a -> a
minmax a b c = maximum [a, b, c] - minimum [a, b, c]

//zadanie7
sumOfSquares :: Num a => a -> a -> a
sumOfSquares x y = x * x + y * y

//zadanie8
lastDigit :: Integral a => a -> a
lastDigit n = abs n `mod` 10


--1
rev :: [a] -> [a]
rev x = rev' x []

rev' :: [a] -> [a] -> [a]
rev' [] y = y
rev' (first:rest) y = rev' rest (first:y) 

--2
fun :: [(Int, Int, Int)] 
fun = [(x, y, x * y) | x<-[1..12], y<-[1..12]]

--3
colors = ["black", "white", "blue", "yellow", "red"]
colfn :: [String] -> [(String, String)]
colfn [x] = []
colfn (first:rest) = [(first, x) | x <- rest] ++ colfn rest 


--6
-- a) append
append :: [a] -> [a] -> [a]
append [] ys = ys
append (x:xs) ys = x : append xs ys

-- b) member
member :: Eq a => a -> [a] -> Bool
member _ [] = False
member x (y:ys)
  | x == y    = True
  | otherwise = member x ys

-- c) last
lastElem :: [a] -> a
lastElem [x] = x
lastElem (_:xs) = lastElem xs
lastElem [] = error "Pusta lista"

-- d) delete
deleteElem :: Eq a => a -> [a] -> [a]
deleteElem _ [] = []
deleteElem x (y:ys)
  | x == y    = ys
  | otherwise = y : deleteElem x ys

-- e) split
split :: Ord a => a -> [a] -> ([a], [a])
split _ [] = ([], [])
split x (y:ys)
  | y < x     = (y:l1, l2)
  | y > x     = (l1, y:l2)
  | otherwise = (l1, l2)
  where (l1, l2) = split x ys


--7
myFilter :: (a -> Bool) -> [a] -> [a]
myFilter _ [] = []
myFilter p (x:xs)
  | p x       = x : myFilter p xs
  | otherwise = myFilter p xs

-- Typ:
-- myFilter :: (a -> Bool) -> [a] -> [a]

--8
onlyEven :: [Int] -> [Int]
onlyEven = filter even

--9
doubleAll :: [Int] -> [Int]
doubleAll = map (*2)

--10
sumOfDigits :: Int -> Int
sumOfDigits n = sum $ map (read . (:[])) $ show $ abs n

